---
layout: page
title: Legacy Projects
tagline: 
---
{% include JB/setup %}


This page gives brief descriptions of projects which are no longer actively
developed.  The *current* projects, [Clang UPC2C](/clang-upc2c/) and [Clang
UPC](/clang-upc/), are available in the navigation bar at the top of this page.

- - -

#### Clang OMP Support

The goal of this project is to allow interoperability between UPC and Open MP
code.  For this purpose an OpenMP/Clang branch (https://clang-omp.github.io/)
has been merged into the Clang UPC.

More information on the [UPC/OMP Project](/clang-omp/)

- - -

#### LLVM IR Remote Access

The goal of this project is to allow UPC
pointers-to-shared (or some other remote pointer) to be expressed in the LLVM
IR and to in turn gain the benefits of LLVM optimizations that operate on
memory references.

More information on the [UPC IR Project](/clang-upc-ir/)

- - -

#### Portals 4 Runtime

The Clang UPC for Portals 4.0 (Portals4, Portals) is an implementation
of Clang UPC that uses Portals interface for message passing between
UPC threads running on separate nodes in a system area network.

More information on the [Portals4 Runtime](/portals4/index.html).

- - -

#### Libfabric Runtime

Clang UPC Libfabric Runtime is an implementation of Clang UPC that uses
Libfabric API for message passing between UPC threads running on
separate nodes in a system area network.

More information in the [Libfabric Runtime](/libfabric/index.html).

