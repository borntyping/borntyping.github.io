---
layout: post
title: Advanced Tox usage
summary: "This article explains the Tox configuration used by several of my Python projects, which both tests the module on multiple versions of python and runs testing-related tools for style guides, static code checking and coverage reports."
---

This article explains the [Tox](http://tox.readthedocs.org/en/latest/) configuration used by several of my Python projects, which both tests the module on multiple versions of python and runs testing-related tools for style guides, static code checking and coverage reports.

The `tox.ini` used here is taken from [Supermann](http://borntyping.github.io/supermann/), and the source can be found [here](https://github.com/borntyping/supermann/blob/master/tox.ini).

### Running pytest to find and run tests

`py.test` is used to discover, run and write tests. It uses `tox.ini` as a configuration file by default, and the two tools work very well in combination. The first two sections tell Tox to use the default Python 2.6 and 2.7 environments, to install `pytest` and `mock` as test dependancies, and to uses `py.test` to run the modules tests.

    [tox]
    envlist=py26,py27

    [testenv]
    commands=py.test supermann
    deps=
        pytest
        mock

    [pytest]
    addopts=-qq --strict --tb=short

### Running flake8 to check code

`flake8` wraps several Python tools for static checking of code - `pep8` for style, and `pyflakes` for static error checking. This configures it to use `tox.ini` for it's configuration - reducing the number of configuration files in the repo.

    [testenv:py26-flake8]
    commands=flake8 --config=tox.ini supermann
    basepython=python2.6
    deps=flake8

    [flake8]
    exclude=supermann/riemann/riemann_pb2.py
    max-complexity=10

### Running coverage to show untouched code

Coverage is by far the most verbose tool configured in my `tox.ini`, but the HTML reports it generates are very useful for working out which parts of my code aren't being run by my tests. This does several new things with `tox`: it runs two commands (one to generate the data, and another to render a HTML report), and uses the dependencies from the existing `testenv` configuration.

Coverage itself is told to use `tox.ini` for it's configuration, and is configured to ingnore various parts of the codebase (the tests folder, and lines of code that should never run). The coverage files are placed in `.tox` to keep the repository tidy while working.

    [testenv:py26-coverage]
    basepython=python2.6
    commands=
        coverage run --rcfile tox.ini --source supermann -m py.test
        coverage html --rcfile tox.ini
    deps=
        {[testenv]deps}
        coverage

    [run]
    data_file=.tox/py26-coverage/data
    omit=supermann/tests/*

    [report]
    exclude_lines=
        def __repr__
        raise NotImplementedError
        class NullHandler

    [html]
    title=Supermann coverage report
    directory=.tox/py26-coverage
