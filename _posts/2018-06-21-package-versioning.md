---
title: Package versioning
category: Development
layout: post
---

This post descibes my approach to versioning packaged applications, using version numbers that look like this: `3.2.0-2109.12272`.

The first part (`3.2.0`) is a **manually incremented version number**. It's incremented for changes that need to be communicated and talked about - "our new feature will be in version 4, which will be deployed next week".

The second part (`2109.12272`) is an **automatically incremented release number**. It's entirely managed by the CI/CD process that packages the software. In my case, that's done using GitLab, and the number is composed from the pipeline and job identifiers.

Both of these numbers increase monotonically, so that a each time the CI/CD process runs it builds a package with a higher version and release number without a human needing to remember to manually increase it. The automatic release number also ensures that you never build a package with the same version number as an existing one, and so as long as you keep older packages around you can always downgrade to a previous version.

The approach works very neatly with packaging tools like RPM, which have seperate version and release fields. My build process uses a `version.txt` and `release.txt` file, the latter of which is created at build time. Both are included in the package name and in the package itself, allowing the application to read them at runtime to display it's own version number.

You could quite easily remove the manually incremented version number and loose no technical capability. However, I find simple, easy to remember numbers much easier to communicate than the long digit sequences an automatic release number will provide. Asking someone to check if they are running "version 4 or above" is much simpler than asking if the version number is "12034 or above" - people remember small numbers much more easily. You can also still use familiar [SemVer](https://semver.org/) like semantics to describe the scale of change - "we're upgrading from version 9034 to 9725" says very little about the changes involved, whereas "we're upgading from version 4.1 to 5.3" implies multiple large changes, or "we're upgading from version 4.1.0 to 4.1.1" implies a small fix. I find this is especially useful when communicating with non-technical people who use the application.

However, a downside to this is that humans will likely end up being very lax about changing the version number. This is fine for me - I only use it to commuicate major changes and not small patches - but is unlikely to work for all cases. It's particually unsuited for libraries or APIs, where tracking API changes is important and strictly following [SemVer](https://semver.org/) may be important.

## Managing version numbers in Python

_The rest of this post goes describes an implementation of the above approach that I use for Python packages._

A `release.txt` file includes the manually updated version number, and an optional `release.txt` file includes the CI/CD pipeline and job number. The `__version__` attribute in my Python module is set by reading from these files instead of being statically defined.

##### `__init.py__`

```python
"""An example package."""

import example.version

__author__ = 'Sam Clements'
__version__ = example.version.read_version(__file__)

```

##### `version.py`

```python
"""Read version numbers from an embedded text file."""

import pathlib


def read_version(relative_path):
    version_path = pathlib.Path(relative_path).with_name('version.txt')
    release_path = pathlib.Path(relative_path).with_name('release.txt')

    version = version_path.read_text().strip()

    if release_path.exists():
        release = release_path.read_text().strip()
        version = "{}-{}".format(version, release)

    return version
```

This is included in the Python package metadata by using the [`attr:` directive](https://setuptools.readthedocs.io/en/latest/setuptools.html#configuring-setup-using-setup-cfg-files) in the [setuptools](https://setuptools.readthedocs.io/) `setup.cfg` file (a relatively recent feature that allows package metadata to be set by reading values from a Python module). For this to work properly, the `__init__` file has to import as little as possible, so that it's not including dependencies that may not be installed when you first build or install the package. For my projects, the `__init__.py` file normally only includes metadata and absolute essentials (e.g. exit handlers with no dependencies).

```ini
[metadata]
name = example
version = attr: example.__version__
...
```

With everything setup to build the application as a Python package, I also use this in a Makefile that builds an RPM with the Python package using [fpm](https://github.com/jordansissel/fpm).

```makefile
CI_PIPELINE_ID?=0
CI_JOB_ID?=0

NAME=$(shell python setup.py --name)
VERSION=$(shell cat odyssey/version.txt)
RELEASE=$(CI_PIPELINE_ID).$(CI_JOB_ID)

example/release.txt:
	echo "$(RELEASE)" > "$@"
	
$(NAME)-$(VERSION)-$(RELEASE).x86_64.rpm:
	fpm -s dir -t rpm \
	--name "$(NAME)" \
	--depends "python" \
	--version "$(VERSION)" \
	--iteration "$(RELEASE)" \
	--maintainer "Sam Clements" \
	.
```

