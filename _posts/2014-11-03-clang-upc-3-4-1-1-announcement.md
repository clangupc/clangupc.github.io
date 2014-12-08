---
layout: post
title: Clang UPC 3.4.1-1 Release
---

Intrepid Technology announces the availability of the Clang UPC
version 3.4.1-1 compiler.  Clang UPC is a Unified Parallel C compiler
that extends the capability of the Clang/LLVM compiler and tool set.

For further information on the UPC language and this implementation consult
[http://intrepid.github.io](http://intrepid.github.io).

This release is based on Clang/LLVM 3.4 and provides the following
components:

* __Clang UPC__<br />
UPC language compiler.

* __Clang UPC2C__<br />
UPC to C translator compatible with the [Berkeley UPC](http://upc.lbl.gov)
toolset.

It has been tested on the following configurations:

  - Intel (Xeon) (64 bit)
  - AMD (Opteron) (64/32 bit)
  - Intel i686 (32 bit)
  - PowerPC (Power7) (64 bit)

More information on Clang UPC configuration and install can be found at
the [Clang UPC](http://intrepid.github.io/clang-upc/) web page.

Runtime Environments
--------------------

Clang UPC provides two runtime environments:

* SMP<br />Shared memory symmetric multiprocessing

* Portals4<br />Infiniband networking with Portals 4.0 reference
library support

The SMP runtime is the default configuration.  To use the Portals4 runtime
please use the _-DLIBUPC_RUNTIME_MODEL:=[smp\|portals4]_ option when
configuring with cmake.

More information on the Portals4 based runtime can be found on its
[project web page](http://intrepid.github.io/portals4).

Downloads
---------

The following three source code components of Clang UPC are available
for download: llvm-upc, clang-upc, and upc2c at
[GitHub download page](http://intrepid.github.io/download.html).

For convenience a tarball release of all three components is also provided.

