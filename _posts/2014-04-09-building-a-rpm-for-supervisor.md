---
layout: post
title: Building a RPM for Supervisor
summary: "A post explaining how to build an RPM for Supervisor"
---

Start with a skeleton specfile, which can be generated using `rpmdev-newspec`:

    rpmdev-newspec supervisor.spec

The example specfile used to write this post can be found [here](https://gist.github.com/borntyping/10252256).

## Package metadata

The basic package metadata can be extracted from Supervisors existing package metadata (`setup.py`) and it's website ([supervisord.org](http://supervisord.org/)).

```
Name: supervisor
Version: 3.0
Release: 1
Summary: A system for controlling process state under UNIX

Group: System Environment/Daemons
License: https://github.com/Supervisor/supervisor/blob/master/LICENSES.txt
URL: http://supervisord.org/

%description
Supervisor is a client/server system that allows its users to control a number
of processes on UNIX-like operating systems.
```

## Defining requirements

Supervisor requires Python 2.4 or above (excluding Python 3.0), Setuptools (a packaging library), and `meld3` (a library used inside Supervisor). In CentOS, these are packaged as `python`, `python-setuptools` and `python-meld3`, and so are added to the package requirements using their package names.

    Requires: python > 2.4
    Requires: python < 3
    Requires: python-meld3 >= 0.6.5
    Requires: python-setuptools

## Sources

Supervisor is developed on [GitHub](https://github.com/Supervisor/supervisor/), which provides source tarballs for repositories.

In the best case, the source url could be defined in the specfile, and `spectool` could be used to download the tarball into the `SOURCES` folder:

    Source0: https://github.com/Supervisor/supervisor/archive/3.0.tar.gz

    spectool --get-files --sourcedir supervisor.spec

Unfortunately, Github's tarball URLs use a series of redirects that result in a different name for the file, and so the files downloaded by `spectool` don't match the filenames `rpmbuild` expects.

Instead, I've used a Makefile that downloads the tarball (and ensures the filename is correct, which also makes it easy to checksum the sources before using them. The Makefile used to build the package is decribed later on in the article. For now, the specfile only has to know the name of the downloaded tarball:

    Source0: supervisor-%{version}.tar.gz

## Building from source

The package is built across three major steps: _prep_, _build_ and _install_.

The preparation step is simple, and does nothing but extract the source tarball. The `-n` option describes the name of the tarball to extract, though `%{name}-%{version}` is the default anyway:

    %prep
    %setup -q -n %{name}-%{version}

The build step uses setuptools to build the package, and then calls it again to install the package into the 'build root':

    %build
    %{__python} setup.py build

    %install
    %{__python} setup.py install --skip-build --root $RPM_BUILD_ROOT

Finally, the specfile has to define the files that will be included in the package:

    %files
    %defattr(-,root,root,-)
    %doc CHANGES.txt COPYRIGHT.txt LICENSES.txt PLUGINS.rst README.rst
    %{_bindir}/echo_supervisord_conf
    %{_bindir}/pidproxy
    %{_bindir}/supervisorctl
    %{_bindir}/supervisord
    %{python_sitelib}/*

This declares that the files should be owned by root, that Supervisors documentation should be placed in a automatic documentation directory, that each of the scripts Supervisor provides should be included, and that all of the Python modules that were installed should be included.

This should result in a directory tree like this:

    └── usr
        ├── bin
        │   ├── echo_supervisord_conf
        │   ├── pidproxy
        │   ├── supervisorctl
        │   └── supervisord
        ├── lib
        │   └── python2.6
        │       └── site-packages
        │           ├── supervisor
        │           ├── supervisor-3.0-py2.6.egg-info
        │           └── supervisor-3.0-py2.6-nspkg.pth
        └── share
            └── doc
                └── supervisor-3.0
                    ├── CHANGES.txt
                    ├── COPYRIGHT.txt
                    ├── LICENSES.txt
                    ├── PLUGINS.rst
                    └── README.rst

## Including configuration

As well as Supervisor itself, including distribution specific information is useful, and one of the primary reasons to build an RPM for it. Firstly, an init script to mange the service is needed, and that requires default configuration so that Supervisor can be started.

Two additional sources are used, containing an init script and a Supervisor configuration file.

    Source0: supervisor-%{version}.tar.gz
    Source1: supervisor.init
    Source2: supervisor.conf

The Supervisor configuration used is a simple as possible, only overriding the options needed to run Supervisor as a system service (by default, most of Supervisors files are placed in `/tmp`):

```
[unix_http_server]
file=/var/run/supervisor.sock

[supervisord]
pidfile=/var/run/supervisord.pid
logfile=/var/log/supervisor/supervisord.log
childlogdir=/var/log/supervisor

[rpcinterface:supervisor]
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface

[supervisorctl]
serverurl=unix:///var/run/supervisor.sock

[include]
files = /etc/supervisor.d/*.conf
```

These files are added to the install step, along with the directories they need:

    %install
    mkdir -p %{buildroot}/%{_initrddir}
    install -p -m 755 %{SOURCE1} %{buildroot}/%{_initrddir}/supervisord
    mkdir -p %{buildroot}/%{_sysconfdir}
    mkdir -p %{buildroot}/%{_sysconfdir}/supervisord.d
    install -p -m 644 %{SOURCE2} %{buildroot}/%{_sysconfdir}/supervisord.conf
    mkdir -p %{buildroot}/%{_localstatedir}/log/%{name}
    %{__python} setup.py install --skip-build --root $R

Finally, the package needs to be configured to add the `supervisord` service to chkconfig using the post-install step:

    %post
    /sbin/chkconfig --add %{name}d || :

And to then remove it in the pre-uninstall step:

    %preun
    if [ $1 = 0 ]; then
        /sbin/service supervisord stop >/dev/null 2>&1 || :
        /sbin/chkconfig --del %{name}d || :
    fi

The `$1 = 0` statement [checks that the package is being removed](http://docs.fedoraproject.org/en-US/Fedora_Draft_Documentation/0.1/html/RPM_Guide/ch09s04s05.html).

With these changes, the specfile should be complete, and the directory tree should now include files in `/etc` and `/var`:
```
.
├── etc
│   ├── rc.d
│   │   └── init.d
│   │       └── supervisord
│   ├── supervisord.conf
│   └── supervisord.d
├── usr
│   ├── bin
│   │   ├── echo_supervisord_conf
│   │   ├── pidproxy
│   │   ├── supervisorctl
│   │   └── supervisord
│   ├── lib
│   │   └── python2.6
│   │       └── site-packages
│   │           ├── supervisor
│   │           ├── supervisor-3.0-py2.6.egg-info
│   │           └── supervisor-3.0-py2.6-nspkg.pth
│   └── share
│       └── doc
│           └── supervisor-3.0
└── var
    └── log
        └── supervisor
```

## Automating the build with make

Since `rpmbuild` requires all sources to be placed in `~/rpmbuild/SOURCES`, I've used a makefile to automate the collecting the sources, and building the RPM:

```
specfile=supervisor.spec

version=$(shell grep Version ${specfile} | awk '{ print $$2 }')
release=$(shell grep Release ${specfile} | awk '{ print $$2 }')

package=supervisor-${version}-${release}.x86_64.rpm
rpmbuild_package=${HOME}/rpmbuild/RPMS/x86_64/${package}

tarball=supervisor-${version}.tar.gz
tarball_url=https://github.com/Supervisor/supervisor/archive/${version}.tar.gz

${package}: ${rpmbuild_package}
    cp ${rpmbuild_package} ${package}

${rpmbuild_package}: sources
    rpmbuild -ba ${specfile}

sources: ${tarball}
    spectool --list-files ${specfile} | awk '{ print $$2 }' | xargs -i cp "{}" ${HOME}/rpmbuild/SOURCES/

${tarball}:
    wget ${tarball_url} --output-document ${tarball}
    md5sum -c sources

.PHONY: sources
```

The version and release are read from the specfile, the used to work out the package name. `spectool` is used to list the sources required and copy them into `rpmbuild`s directories, and wget is used to fetch the source tarball due to the previously mentioned issues with redirects.