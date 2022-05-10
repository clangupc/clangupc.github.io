---
layout: page
title: Clang UPC Tool Set
tagline: 
---
{% include JB/setup %}

The Clang UPC toolset provides a compilation and execution environment for
programs written in the [UPC language](http://upc-lang.org).
The Clang UPC compiler extends the capabilities of the Clang front-end
for the LLVM compiler.

## Latest News

+ Jan 21, 2022: Clang UPC2C 9.0.1-2 released
+ Jan 21, 2022: Clang UPC 3.9.1-2 released

## Projects
- - -

#### Clang UPC to C Translator (Clang UPC2C)

The Clang UPC to C translator uses the Clang UPC infrastructure to
translate UPC into C code.  Development of Clang UPC2C is hosted at GitHub
([https://github.com/clangupc/upc2c](https://github.com/clangupc/upc2c)).

[Berkeley UPC](https://upc.lbl.gov) provides a compiler driver and UPC
runtime library for effective usage of the Clang UPC2C translator, including
for distributed UPC applications.

More info: [Clang UPC2C webpage](/clang-upc2c/)

- - -

#### Clang UPC

Clang UPC is an implementation of the UPC language using the Clang and LLVM
framework.  Two GitHub repositories
([https://github.com/clangupc/llvm-upc](https://github.com/clangupc/llvm-upc)
and
[https://github.com/clangupc/clang-upc](https://github.com/clangupc/clang-upc))
are used for development of Clang UPC.

As with Clang UPC2C, [Berkeley UPC](https://upc.lbl.gov) provides a compiler
driver and UPC runtime library which can be used with Clang UPC for distributed
environments.  However, Clang UPC can also be used alone for single-node
application runs.

More info: [Clang UPC webpage](/clang-upc/)

- - -

#### Past Projects

Info on past projects related to the Clang UPC infrastructure is available
[here](/legacy/)

- - -

#### Other UPC Links

* [UPC Language](https://upc-lang.org)

  Main UPC language web site with tutorials and references.

* [UPC Specification](https://upc.lbl.gov/publications/upc-spec-1.3.pdf)

  This link downloads version 1.3 of the UPC language and library specifications.

* [Berkeley UPC](https://upc.lbl.gov/)

  Berkeley UPC project page.  Clang UPC2C and Clang UPC can both
  be used together with the Berkeley UPC compiler driver and runtime, allowing
  the execution of UPC programs on large-scale multiprocessors,
  PC clusters, and clusters of shared memory multiprocessors.

* [GNU UPC](https://github.com/Intrepid/GUPC)

  UPC compiler based on the GNU GCC.  All the GNU UPC features
  are also available in Clang UPC.

