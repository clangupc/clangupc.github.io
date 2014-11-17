---
layout: page
title: Clang UPC Installation
tagline:
categories: [clang-upc]
---
{% include JB/setup %}

## 1.1. Requirements

Clang UPC is know to work on the following platforms
(with LInux/x86_64 being the main development and
test platform):

**OS**|**Architecture**
Linux    | x86_64/amd64 |
Linux    | x86          |
Linux    | PowerPC      |
FreeBSD  | x86_64       |
Mac OS X | x86_64       |

<br/>
Building Clang UPC requires [CMake](http://www.cmake.org/)
or [GNU Autoconf](https://www.gnu.org/software/autoconf/)
tools (configure).  Please see the [LLVM
documentation](http://llvm.org/docs/GettingStarted.html#requirements)
for a list of any further system requirements.

## 1.2 Downloading Sources

Clang UPC sources are managed in the git repositories on
[GitHub](http://github.com/Intrepid).  At minimum, two
repositories (llvm-upc and clang-upc) must be acquired
(cloned).  For example, if _src_ is a directory for Clang
UPC source, the following commands can be used to clone
Clang UPC sources:

<pre>
 git clone git://github.com/Intrepid/llvm-upc.git src
 cd src/tools; git clone git://github.com/Intrepid/clang-upc.git clang
</pre>

Optionally you can also choose to install Clang based 
UPC to C translator:

<pre>
 cd src/tools/clang/tools; \
 git clone git://github.com/Intrepid/upc2c upc2c
</pre>

The maintainer of Clang UPC also provides stable releases
of the Clang UPC.  Please visit the [download](/download) page
for the list of available downloads.

## 1.3 Configure and Build Sources

Follow these simple steps to configure Clang UPC:

<dl>
<dt>By using cmake:</dt><dd>
<pre>
mkdir bld; cd bld; cmake [options] path/to/src
</pre></dd>
<dt>By using configure:</dt><dd>
<pre>
mkdir bld; cd bld; path/to/src/configure [options]
</pre></dd>
</dl>

NOTE: _bld_ is a directory that holds the intermediate build products.
The _bld_ directory needs to be outside of the llvm source tree, but other
than that, it’s arbitrary.

One of the common configuration options is directory prefix of
the installed compiler.  For example, cmake prefix option:

<pre>
 -DCMAKE_INSTALL_PREFIX:PATH=/usr/local
</pre>
And configure prefix option:
<pre>
 --prefix=/usr/local
</pre>

Run _make_ in the build directory to create Clang UPC executables
and libraries, and install the compiler in the desired place (by default
_/usr/local_).

<pre>
 make; make install
</pre>

<p class="note"><b>Note:</b> Adding <i>make</i> option for parallel build
(e.g. <i>make -j8</i>) speeds up the build process.</p>

Please see the [configuration options](/clang-upc/config-options.html) for more
configuration options.

