---
layout: page
title: "Downloads"
group: navigation
description: "Clang UPC Downloads"
---
{% include JB/setup %}

Clang UPC consists of two separate GitHub projects (components): llvm-upc
and clang-upc.  Optionally, you can also download the Clang upc2c translator.

### Clang UPC 3.4.1-1

#### Download all components together

For the end user convenience all three components (llvm-upc, clang-upc, and upc2c)
are put together in one downloadable file.

* [Clang UPC 3.4.1-1](https://github.com/Intrepid/clang-upc/archive/clang-upc-3.4.1-1/clang-upc-all-3.4.1-1.tar.gz)

- - - -

#### Download components separately

Each of the components can be downloaded separately.

* [llvm-upc 3.4.1-1](https://github.com/Intrepid/llvm-upc/archive/clang-upc-3.4.1-1.tar.gz)
* [clang-upc 3.4.1-1](https://github.com/Intrepid/clang-upc/archive/clang-upc-3.4.1-1.tar.gz)
* [upc2c 3.4.1-1](https://github.com/Intrepid/upc2c/archive/clang-upc-3.4.1-1.tar.gz)

Due to some issues related to the GitHub release files naming, follow these
steps to make sure that all the files are unpacked in their right places:

* Download all three components with your browser's "Save As" commands.  Save the
files as _llvm-upc-3.4.1-1.tar.gz_, _clang-upc-3.4.1-1.tar.gz_, and
_upc2c-3.4.1-1.tar.gz.

* Create source directory and unpack files

<pre>
mkdir src; cd src
tar --strip-components 1 xf /path/to/tar/llvm-upc-3.4.1-1.tar.gz
cd tools; mkdir clang; cd clang
tar --strip-components 1 xf /path/to/tar/clang-upc-3.4.1-1.tar.gz
cd tools; mkdir upc2c; cd upc2c
tar --strip-components 1 xf /path/to/tar/upc2c-3.4.1-1.tar.gz
cd ../../../..
</pre>

- - - -

#### Clone GitHub repositories

The other option for downloading is to simple clone all the necessary
directories.  Follow these steps to checkout all the necessary components:

<pre>
mkdir src; cd src
git clone -b clang-upc-3.4.1-1 https://github.com/Intrepid/llvm-upc.git .
mkdir tools/clang; cd tools/clang
git clone -b clang-upc-3.4.1-1 https://github.com/Intrepid/clang-upc.git .
mkdir tools/upc2c; cd tools/upc2c
git clone -b clang-upc-3.4.1-1 https://github.com/Intrepid/upc2c.git .
</pre>
