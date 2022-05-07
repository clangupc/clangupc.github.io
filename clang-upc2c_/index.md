---
layout: page
title: Clang UPC2C Translator
group: none
tagline: 
---
{% include JB/setup %}

The Clang UPC2C Translator (aka cupc2c) is a source-to-source translator which
transforms a program written in [UPC](http://upc-lang.org) into ISO standard
C99.  The resulting output can be compiled and linked with a suitable UPC
runtime such as the one provided by [Berkeley UPC](https://upc.lbl.gov).  When
properly configured, Berkeley UPC's `upcc` compiler driver will invoke
Clang UPC2C transparently.

## Supported Platforms

While it is likely that Clang UPC2C can be built and used on any platform where
LLVM 9 builds, it is currently supported only on the following platforms (each
of which receives periodic regression testing):

+ Linux/x86-64
+ Linux/ppc64le
+ macOS/x86-64

## Downloads

The current release and its license file are available from GitHub:

+ [clang-upc2c-9.0.1-2.tar.gz](https://github.com/clangupc/upc2c/releases/download/clang-upc2c-9.0.1-2/clang-upc2c-9.0.1-2.tar.gz)
+ [LICENSE.TXT](https://raw.githubusercontent.com/clangupc/upc2c/clang-upc2c-9.0.1-2/LICENSE.TXT)

## Build Instructions

These instructions assume you begin from a source directory, such as from
unpacking a release tar archive (such as from the download link above) or
comprised of git sources (described in the next section: "Git Instructions").

### Prerequisites

+ CMake version 3.14 or newer
+ Either `gcc/g++` (5.1.0 or newer) or `clang/clang++` (4.0.0 or newer)
    + On macOS this typically means use of the Xcode Command Line Tools.
+ GNU Make or other standard `make` utility
    + CUPC2C has not been tested with other CMake generators, such as `Ninja`
+ Approximately 1GB to 2GB temporary disk space for the build
+ Approximately 300MB disk space for the installed CUPC2C

Disk space estimates assume you follow the configuration recommendations given
below.

### Instructions

There are four high-level steps involved in installing CUPC2C, described in
more detail in the paragraphs which follow.

1. Create a build directory
2. Configure CUPC2C
3. Build CUPC2C
4. Install CUPC2C

#### 1. Create a build directory

The LLVM infrastructure does not support builds in the source tree.
So, you must create a distinct directory for building CUPC2C.
This build directory is also distinct from the installation directory, and
therefore is normally deleted after the installation is complete.
Something like `/tmp/cupc2c-build` may be appropriate.  When configured
as recommended, you should expect to need no more than 2GB of disk space
for the build.  However, without the recommended options to `cmake` one
could need as much as 50GB.

In the following steps `[SRCDIR]` and `[BLDDIR]` will be used as placeholders
for the CUPC2C source directory and build directory, respectively.

#### 2. Configure CUPC2C

There are a mixture of required, recommended and optional arguments to pass to
`cmake`, to configure your build of CUPC2C.  They are described in detail on
the [CUPC2C CMake Options](./cmake-options.html) page.  However, in most cases
the following are sufficient with the appropriate substitutions for the
`[PREFIX]`, `[BLDDIR]` and `[SRCDIR]` placeholders.

On a Linux system:

```
$ cd [BLDDIR]
$ cmake \
        -DCMAKE_INSTALL_PREFIX=[PREFIX] \
        -DCMAKE_BUILD_TYPE=Release \
        -DLLVM_TARGETS_TO_BUILD=host \
        -DLLVM_BUILD_TOOLS=OFF \
        -DLLVM_INCLUDE_DOCS=OFF \
        -DLLVM_INCLUDE_UTILS=OFF \
        -DLLVM_INCLUDE_TESTS=OFF \
        -DLLVM_INCLUDE_EXAMPLES=OFF \
        -DLLVM_INSTALL_TOOLCHAIN_ONLY=ON \
        -DCLANG_ENABLE_ARCMT=OFF \
        -DCLANG_ENABLE_STATIC_ANALYZER=OFF \
        -S [SRCDIR]
```

For macOS, you should add the following to the Linux example above:

```
        -DCMAKE_CXX_FLAGS="-Wno-deprecated-declarations" \
        -DDEFAULT_SYSROOT=/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk \
        -DLLVM_ENABLE_LIBCXX=TRUE
```

On some systems, CMake version 3 may be installed as `cmake3` rather than
`cmake`.

#### 3. Build CUPC2C

This step consists of running `make` or `make -j[N]`, where `[N]` is the
number of concurrent processes to be used in building CUPC2C.
Generally, values of `[N]` as large as the system's CPU core count can be used
to speed up the build.  However, the link steps can be very memory-intensive
such that too-large `[N]` leads to running out of memory.

If your build fails when passing `-j[N]`, please retry without that option.
This should be attempted even without anything to suggest an out-of-memory
condition.  For instance, insufficient disk space in `/tmp` could also lead to
failures exclusive to parallel builds.

It is normal for this build step to generate many harmless warnings.

#### 4. Install CUPC2C

This step consists simply of running `make install`.

After this step, you may safely remove `[SRCDIR]` and `[BLDDIR]`.  The install
is self-contained, without dependencies on either of these directories.

### Troubleshooting a failed build

As noted earlier, _any_ build failure experienced with `make -j[N]` should be
retried with just `make`.  If that is not sufficient to recover, some known
failure modes and possible resolutions are described in the
[CUPC2C Troubleshooting](./troubleshooting.html) page.

## Git Instructions

The "Build Instructions" above assume you start from a complete source
directory.  The simplest means to obtain one (and our strong recommendation) is
to use the tar archive in the download section.  However, if there is a need,
it is also possible to construct such a directory from sources obtained using
`git`.

The development of CUPC2C is spread over three git repositories, with two of
them having distinct branches for the CUPC2C and CUPC products.  Therefore, you
should use the following steps to ensure a complete and consistent source tree.
With appropriate substitutions for `[SRCDIR]` and `[BRANCH]` (see below):

```
$ git clone -b [BRANCH] https://github.com/clangupc/llvm-upc  [SRCDIR]
$ git clone -b [BRANCH] https://github.com/clangupc/clang-upc [SRCDIR]/tools/clang
$ git clone -b [BRANCH] https://github.com/clangupc/upc2c     [SRCDIR]/tools/clang/tools/upc2c
```

Where the `[BRANCH]` placeholder should be replaced with one of the following:

+ For the current CUPC2C release: `main-cupc2c` (the default branch)
+ For a specific CUPC2C release: `clang-upc2c-[VERSION]`
    + Where `9.0.1-2` is an example substitution for `[VERSION]`
+ For the current CUPC2C development branch: `develop-cupc2c`

## Using the installed CUPC2C

Once CUPC2C has been installed, you should install
[Berkeley UPC](https://upc.lbl.gov), following its
[instructions for use of CUPC2C](https://upc.lbl.gov/download/dist/INSTALL.TXT)
as a source-to-source translator.  In doing so, you may configure for
use of a back-end C compiler of your choice, but should __not__ use the `clang`
(or `clang++`) built from the CUPC2C sources.  Those compilers are not
supported.

## Contact Information

### Bug Reports

Bugs in Clang UPC2C can be reported on the
[Clang UPC2C issues](https://github.com/clangupc/upc2c/issues) page.

Bugs in the Berkeley UPC driver or libraries can be reported in the corresponding
[Bugzilla server](https://upc-bugs.lbl.gov) under the "BerkeleyUPC" product.

If in doubt as to which to use, please use the Berkeley UPC Bugzilla.  
In either case, please search the bug database for a possible solution
to your problem before entering a new report.

### General Info

To reach the developers, free to drop us a note at
`upc-devel[non-robots should remove this part]@lbl.gov`.

