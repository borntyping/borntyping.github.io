---
title: Tox and Travis CI
summary: Using Tox and Travis side-by side
category: Development
layout: post
---

Until recently, my approach to building python projects that used [Tox](http://testrun.org/tox/latest/) on [Travis CI](http://travis-ci.org/) was simply to have two separate configuration files, each duplicating the others settings.

This would normally work okay, with both Tox and Travis defining a set of python runtimes to use and a command to run on them. However, when it came to the more complex `tox.ini` file I'm using for [python-dice](https://github.com/borntyping/python-dice/blob/master/tox.ini), recreating this in the Travis configuration would have difficult to do, and require a lot of maintenance when the Tox settings changed.

The solution? Using Travis to run Tox, using it's matrix feature and the `TOXENV` environment variable to create a different build for each of several Tox environments, like so:

    :::yaml
    language: python
    env:
    - TOXENV=py26
    - TOXENV=py27
    - TOXENV=py32
    - TOXENV=py33
    - TOXENV=pypy
    install:
    - pip install tox
    script:
    - tox
