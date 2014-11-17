---
layout: page
title: "Clang UPC Compiling"
description: ""
---
{% include JB/setup %}

Clang UPC is invoked by the running the _clang-upc_ driver (or a
convenience symbolic link _upc_). _clang-upc_ must be used
for linking to automatically include the UPC runtime on the command line
(Just as clang++ is used for C++).

Clang UPC has a number of UPC specific options, in addition to those supported
by Clang.  The following options are available.

* **-fupc-threads-N**<br />Compiles under the static threads environment with N
threads. N must be a positive decimal integer. Different values of this option
are not binary compatible except that translation units compiled under the
dynamic threads environment may be combined with translation units compiled
under the static threads environment.

* **-x upc**<br />
  Forces sources to be treated as UPC.

* **-fno-upc-inline-lib**<br />
  Disable inlining of UPC runtime calls

* **-fno-upc-pre-include**<br />
  Disable pre-include of UPC specific include files

* **-fupc-debug**<br />
  Generate UPC runtime calls that include debugging information

* **-fupc-packed-bits=\<value\>**<br />
  Specify the UPC packed pointer-to-shared representation (e.g. 20,10,34)

* **-fupc-pts-vaddr-order=\<value\>**<br />
  Specify the UPC pointer-to-shared address field order (first or last)

* **-fupc-pts=\<value\>**<br />
  Specify the UPC pointer-to-shared representation (packed or struct)

