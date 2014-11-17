---
layout: page
title: "Clang UPC Portals4 runtime"
description: ""
---
{% include JB/setup %}

The Clang UPC toolset provides a compilation and execution environment for
programs written in the UPC (Unified Parallel C) language. The Clang UPC
compiler extends the capabilities of the Clang/LLVM compiler.

The Clang UPC for Portals 4.0 (Portals4, Portals) is an implementation
of Clang UPC that uses Portals interface for message passing between
UPC threads running on separate nodes in a system area network.

### Portals4 Configuration

As Portals4 runtime has been fully integrated into the Clang UPC, no
additional configuration description is needed besides the one in the
Clang UPC [configuration page](/clang-upc/config-options.html).  See section
related to the Portals 4 Runtime Options.

To enable running UPC programs on the Portals4 network, use the following
Clang UPC configuration switch:

    -DLIBUPC_RUNTIME_MODEL:=portals4

### Program Execution

Execution of the compiled program with Portals4 support requires the Portals 4
Reference Implementation Library. Both the Portals4 shared library and job
launcher are required to successfully run the GNU UPC program compiled for
Portals4.

See the [Portals4 Runtime Execution Options](/portals4/execution.html) page
for more information on all the available options when executing
Portals4 runtime based UPC programs. 

### More on Portals4 Library

* [UPC Runtime Design Utilizing Portals 4](http://www.gccupc.org/gnu-upc-documentation/upc-runtime-design-utilizing-portals-4)
  This document describes the design of a UPC runtime, which implements UPC
  (Unified Parallel C) semantics, and that makes use of the functions and
  operations provided by the Portals-4 API (Application Programming Interface)

* [Portals Network Prgramming Interface](http://www.cs.sandia.gov/Portals/)
  Portals is a message passing interface intended to allow scalable,
  high-performance network communication between nodes of a parallel computing
  system.

* [Portals 4.0](http://www.cs.sandia.gov/Portals/portals4.html)
  Portals version 4.0 ss substantially enhanced Portals interface to better
  support the various PGAS programming models. 

* [Portals 4 Reference Implementation](https://code.google.com/p/portals4/)
  The Portals 4 Reference Implementation is a complete implementation of
  Portals 4, with transport over InfiniBand VERBS and UDP.

