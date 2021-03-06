---
layout: page
title: "Clang UPC and OpenMP/Clang"
description: ""
---
{% include JB/setup %}

The goal of this project is to allow interoperability of Clang UPC and
OpenMP.  For this purpose an OpenMP/Clang branch has been merged into
the Clang UPC project.

Running the UPC code with OMP support requires
[Intel's OpenMP Runtime Library](http://openmp.llvm.org/).

### Getting Clang UPC with OpenMP support

Follow these instructions to build Clang UPC with OpenMP.

* Clone the following repositories
<pre>
git clone git://github.com/Intrepid/llvm-upc.git llvm
git clone git://github.com/Intrepid/clang-upc.git llvm/tools/clang
</pre>

* Additionally, clone the Clang compiler runtime library
<pre>
git clone https://github.com/clang-omp/compiler-rt_trunk llvm/projects/compiler-rt
</pre>

* Build the same way as building _Clang UPC_.

* build and install Intel's OpenMP Runtime Library.

#### UPC/OMP interoperability

The following restrictions apply when executing OMP code in UPC environment:

* OMP worker threads are not allowed to execute UPC code.  For example, code
accessing shared scalars and arrays, UPC barriers, UPC locks, and UPC
allocations is allowed on the OMP master thread only (UPC thread).

#### Configuration Options

There are no OpenMP specific options in Clang UPC.  However, special check for
UPC code inside the OMP code sections is added when compiler is built with
__-DLIBUPC_ENABLE_RUNTIME_OMP_CHECKS__ option enabled.

#### Compile Options

The following compile time option has been added:

* __-fopenmp__

  Generate OpenMP specific code.

Also, as required by OpenMP/Clang, add the following to your environment as Clang UPC
needs to fund _omp.h_, as well as OpenMP runtime library.

<pre>
export PATH=/install/prefix/bin:$PATH
export C_INCLUDE_PATH=/install/prefix/include:OpenMP include path:$C_INCLUDE_PATH
export LIBRARY_PATH=/install/prefix/lib:OpenMP library path:$LIBRARY_PATH
export LD_LIBRARY_PATH=/install/prefix/lib:OpenMP library path:$LD_LIBRARY_PATH
</pre>

### Current Status

All the work done on this project is on a special _clang-omp_ branch.

* 05/25/2015 - clang-omp branch merged into the main development branch
* 03/01/2015 - OpenMp/Clang branch merged into Clang UPC

### References

* [OpenMP/Clang](https://clang-omp.github.io/)
