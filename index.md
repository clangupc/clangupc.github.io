---
layout: page
title: Clang UPC Tool Set
tagline: 
---
{% include JB/setup %}

The Clang UPC toolset provides a compilation and execution environment for
programs written in the UPC (Unified Parallel C) language.
The Clang UPC compiler extends the capabilities of the Clang front-end
for the LLVM compiler.

### Latest News
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; 
    <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

### Projects
- - -

#### Clang UPC

Clang UPC is the first implementation of the UPC language by using the Clang
and LLVM framework.  The current work is based on the LLVM 3.4 version of
Clang/LLVM.

Two GitHub repositories (https://github.com/Intrepid/llvm-upc and
https://github.com/Intrepid/clang-upc) are used for developing Clang UPC.

More info: [Clang UPC webpage](/clang-upc/)

- - -

#### UPC to C Translator

The UPC to C translator (https://github.com/Intrepid/upc2c) uses the
Clang UPC infrastructure to translate UPC into the C code.
[Berkeley UPC](http://upc.lbl.gov) is the framework for effective usage
of the UPC2C translator.

More info: [Clang UPC2C webpage](/clang-upc2c/)

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

- - -

#### Try it and get involved!

Once you have a chance to try it, consider getting involved in the Clang UPC
community.  <a href="mailto:info@intrepid.com">Drop us a message</a>
with your ideas and observations.

#### Other UPC projects

* [UPC Language](http://upc-lang.org)

  Main UPC language web site with tutorials and references.

* [UPC Specification](http://code.google.com/p/upc-specification/)

  UPC Specification group website.  Version 1.3 was recently released.

* [GNU UPC](http://www.gccupc.org)

  UPC compiler based on the GNU GCC.  All the GNU UPC features
  are also available in Clang UPC.

* [Berkeley UPC](http://upc.lbl.gov/)

  Berkeley UPC project page.  Clang UPC (both compiler and UPC2C translator)
  can be used together with the Berkeley UPC framework and runtime, allowing
  the execution of UPC programs on large-scale multiprocessors,
  PC clusters, and clusters of shared memory multiprocessors.

