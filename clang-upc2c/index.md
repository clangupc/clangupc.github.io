---
layout: page
title: Clang UPC2C Translator
tagline: 
---
{% include JB/setup %}

This project translates a program written in [UPC](http://upc-lang.org)
(Unified Parallel C) program into the C language program.  It is built at the
top of the [Clang UPC](https://github.com/Intrepid/clang-upc/wiki) and is
compatible with the [Berkeley UPC](http://upc.lbl.gov) translator.

## Installing Clang UPC to C Translator

### 1.1 Requirements

Clang UPC to C translator (upc2c) requires Clang UPC.

### 1.2 Build and Install

Get sources for llvm-upc and clang-upc projects:

<pre>
mkdir [path/to/src]; cd [path/to/src]
git clone https://github.com/Intrepid/llvm-upc.git llvm
cd llvm/tools; git clone https://github.com/Intrepid/clang-upc.git clang
</pre>

Get sources for upc2c project:

<pre>
cd clang/tools; git clone https://github.com/Intrepid/upc2c.git upc2c
</pre>

<p class="note">Note: clang is installed as a llvm's tool, while upc2c is installed as a
clang's tool.</p>

Build the translator:

<pre>
mkdir [path/to/build]; cd [path/to/build]
cmake path/to/llvm [options]
</pre>

_build_ is a directory that holds the intermediate build products. The
build directory needs to be outside the llvm tree, but other than that, it’s
arbitrary.

See [ClangUPC](https://github.com/Intrepid/clang-upc/wiki) documentation
for additional build options.

### Running UPC to C translator

Clang upc2c is invoked by the running the _upc2c_ driver.

<pre>
upc2c -o out.c program.upc
</pre>

By default, the output file name has an extension _trans.c_.

## Supported Platforms

The UPC2C translator works on all the platforms where Clang UPC is supported.

## More on Clang UPC2C translator

* [Berkeley UPC](http://upc.lbl.gov)

