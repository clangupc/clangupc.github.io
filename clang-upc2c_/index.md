---
layout: page
title: Clang UPC2C Translator
group: none
tagline: 
---
{% include JB/setup %}

The Clang UPC2C Translator (aka cupc2c) is a source-to-source translator which
transforms a program written in [UPC](http://upc-lang.org) into ISO standard
C99.  The resulting output can be compiled and linked with a suitable UPC
runtime such as the one provided by [Berkeley UPC](https://upc.lbl.gov).  When
properly configured, Berkeley UPC's `upcc` compiler driver will invoke
Clang UPC2C transparently.

## Supported Platforms

While it is likely that Clang UPC2C can be built and used on any platform where
LLVM 9 builds, it is currently supported only on the following platforms (each
of which receives periodic regression testing):

+ Linux/x86-64
+ Linux/ppc64le
+ macOS/x86-64

## Downloads

The current release and its license file are available from GitHub:

+ [clang-upc2c-9.0.1-2.tar.gz](https://github.com/clangupc/upc2c/releases/download/clang-upc2c-9.0.1-2/clang-upc2c-9.0.1-2.tar.gz)
+ [LICENSE.TXT](https://raw.githubusercontent.com/clangupc/upc2c/clang-upc2c-9.0.1-2/LICENSE.TXT)

## Build Instructions

#### Coming Soon:
Instructions for building Clang UPC2C from a release (.tar.gz) file.

## Git Instructions

#### Coming Soon:
Instructions for building Clang UPC2C from the repositories on GitHub.

## Contact Information

### Bug Reports

Bugs in Clang UPC2C can be reported on the
[Clang UPC2C issues](https://github.com/clangupc/upc2c/issues) page.

Bugs in the Berkeley UPC driver or libraries can be reported in the corresponding
[Bugzilla server](https://upc-bugs.lbl.gov) under the "BerkeleyUPC" product.

If in doubt as to which to use, please use the Berkeley UPC Bugzilla.  
In either case, please search the bug database for a possible solution
to your problem before entering a new report.

### General Info

To reach the developers, free to drop us a note at
`upc-devel[non-robots should remove this part]@lbl.gov`.

