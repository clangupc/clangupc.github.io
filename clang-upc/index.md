---
layout: page
title: Clang UPC
tagline: Unified Parallel C
---
{% include JB/setup %}

Clang Unified Parallel C (Clang UPC) toolset provides a compilation and
execution environment for programs written in the UPC (Unified Parallel C)
language. The Clang UPC compiler extends the capabilities of the Clang LLVM
C compiler.

- - - -
* [Clang UPC Installation](/clang-upc/install.html)

* [Cmake Configuration Options](/clang-upc/config-options.html)
  ([Autoconf Configuration Options](/clang-upc/autoconf-options.html))

* [Compile Options](/clang-upc/compile.html)

* [Execution Options](/clang-upc/execution.html)

* [Sample Session](/clang-upc/sample.html)

- - - -

## Features

* UPC Language Specification version 1.3 compliant
* LLVM licensed
* Fast bit packed pointer-to-shared support
* Configurable pointer-to-shared representation
* Support for uniprocessor and symmetric multiprocessor systems
* Runtime support for Infiniband based clusters with
  Portals 4.0 library support.
* Support for many large scale machines and clusters in conjunction
  with [Berkeley UPC runtime](http://upc.lbl.gov) 
* Runtime support for UPC collectives
* Runtime support for UPC thread affinity via Linux scheduling affinity
  and NUMA package
* Runtime support for UPC thread backtrace 

## Supported Platforms

At this time, Clang UPC is available on the following platforms:

<dl>
<dt>Intel x86_64</dt>
<dd>
<ul><li>Linux 64 bit uniprocessor or multiprocessor systems
        (RHEL, SUSE, Fedora, CentOS, Ubuntu)</li>
    <li>Apple Mac OS X system (Snow Leopard, Lion, and Mountain Lion)</li>
    <li>Free BSD, Open BSD, and Net BSD platforms</li>
</ul>
</dd>
<dt>Intel x86</dt>
<dd>Linux 32 bit systems (Redhat based distributions)</dd>
<dt>IBM PowerPC</dt>
<dd>IBM Power6/Power7 Linux based systems (including PERCS)</dd>
</dl>

If you would like to learn of future ports to other platforms, or
would like to discuss the feasibility of implementing Clang UPC
on a platform of interest to you, please
[send us a note](mailto:upc@intrepid.com).

### More on Clang UPC
