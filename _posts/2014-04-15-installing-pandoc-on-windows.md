---
title: Installing Pandoc on Windows
summary: How to install Pandoc on Windows
category: Development
layout: post
---

Install [pandoc](http://johnmacfarlane.net/pandoc/) using the Windows installer from [here](http://code.google.com/p/pandoc/downloads/list). Install pandoc globally using this command (using the path to the version of pandoc you downloaded):

    msiexec /i pandoc-1.12.3.msi ALLUSERS=1

Install [miktex](http://miktex.org/) from [here](http://miktex.org/download).

Run these commands to check that pandoc and miktex are installed:

    "C:\Program Files (x86)\Pandoc\pandoc.exe" --version
    "C:\Program Files (x86)\MiKTeX 2.9\miktex\bin\pdflatex.exe" --version
