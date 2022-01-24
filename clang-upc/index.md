---
layout: page
title: Clang UPC Compiler
tagline: Unified Parallel C
group: navigation
---
{% include JB/setup %}

Clang UPC toolset provides a compilation and
execution environment for programs written in the UPC 
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
* Optional LLVM remote pointer generation to gain benefits of LLVM
  optimizations

## Supported Platforms

At this time, Clang UPC is supported on the following platforms:

<dl>
<dt>Intel x86_64</dt>
<dd>
<ul><li>Linux 64 bit uniprocessor or multiprocessor systems
        (RHEL, SUSE, Fedora, CentOS, Ubuntu)</li>
    <li>Apple macOS systems</li>
</ul>
</dd>
<dt>Intel x86</dt>
<dd>Linux 32-bit systems</dd>
<dt>IBM PowerPC and Power (big- and little-endian)</dt>
<dd>Linux 64-bit systems</dd>
</dl>

### More on Clang UPC


