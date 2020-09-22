---
toc: false
layout: post
description: install a fortran compiler for msc.marc
categories: [markdown]
comments: true
title: How to install a Fortran Compiler for MSC.Marc
---

# How to install a Fortran Compiler for MSC.Marc

In this post I'll discuss all the necessary steps to install the Intel Fortran compiler for MSC.Marc. At first we have to find out the necessary tools to compile fortran subroutines on Windows. In every Release Guide of MSC.Marc there is a table which versions of the Intel Compiler are compatible. Make sure to download this specific versions as even newer compiler versions may lead to problems. For MSC.Marc 2016 the Fortran Version is **Intel XE2015** and **Microsoft Visual Studio 2013**. Be sure to uninstall *all* versions of MSC.Marc before continuing with the following steps.

## Installation
It is important to install the software tools in the following order. In this way we avoid problems that software B is not finding the required software A inside the registry.

### Visual Studio 20xx
We start with installing Microsft Visual Studio 20xx. Go to the [Visual Studio Download Page](https://my.visualstudio.com/Downloads) and search for *visual studio community 20xx* (older versions are easier to find with the exact search string). Download the installer and choose the *Custom* install option. As noted by [Intel](https://software.intel.com/en-us/articles/installing-visual-studio-2015-for-use-with-intel-compilers) it is necessary to install *Common Tools for Visual C++ 2015* which is not activated by default. Restart your Computer.

### Intel XE20xx Composer
After the installation of Visual Studio is completed we proceed with the Fortran compiler by Intel. Search for the Intel Download Page (or, if you're student visit [this site](https://software.intel.com/en-us/qualify-for-free-software/student)) and download **Intel Parallel Studio XE** for Windows. Once again: use exact the same version as noted inside the Document *MSC.Marc Release Guide*. Restart your Computer again to make sure all environmental variables are updated in your system.

### MSC.Marc Mentat 20xx
Now you may install MSC.Marc without any special considerations regarding Fortran compiling support. All necessary paths are set and detected automatically by Marc.
