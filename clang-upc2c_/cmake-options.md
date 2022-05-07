---
layout: page
title: CUPC2C CMake Options
tagline: 
---
{% include JB/setup %}

There are a mixture of required, recommended and optional arguments you can or
should pass to `cmake`, to configure your build of CUPC2C:

```
$ cmake \
        -DCMAKE_INSTALL_PREFIX=[PREFIX] \
        [RECOMMENDED OPTIONS] \
        [COMPILER SELECTION] \
        [TARGET-SPECIFIC SETTINGS] \
        [PTS SETTINGS] \
        -S [SRCDIR]
```

Placeholders (designated by square brackets) are described in the following
paragraphs.

### [SRCDIR] (required)

This should be the full or relative path the CUPC2C source directory.

### [PREFIX] (required)

The `[PREFIX]` placeholder must be replaced by the full path to an installation
directory.  The "Install" step will copy the built CUPC2C software to
directories below this prefix, such as `[PREFIX]/bin` and `[PREFIX]/lib`.  
We recommend choosing an initially empty location as the prefix, and strongly
discourage choices such as `/usr` and `/usr/local`.  This ensures that you
can reliably remove the entirety of a CUPC2C installation at a later time.

### [RECOMMENDED OPTIONS] (strongly recommended)

The following are recommended to omit unnecessary portions of the LLVM and Clang
infrastructures from the build process (saving time and temporary disk space)
and from the install (saving persistent disk space).

```
        -DCMAKE_BUILD_TYPE=Release \
        -DLLVM_TARGETS_TO_BUILD=host \
        -DLLVM_BUILD_TOOLS=OFF \
        -DLLVM_INCLUDE_DOCS=OFF \
        -DLLVM_INCLUDE_UTILS=OFF \
        -DLLVM_INCLUDE_TESTS=OFF \
        -DLLVM_INCLUDE_EXAMPLES=OFF \
        -DLLVM_INSTALL_TOOLCHAIN_ONLY=ON \
        -DCLANG_ENABLE_ARCMT=OFF \
        -DCLANG_ENABLE_STATIC_ANALYZER=OFF
```

Omitting certain of these options can increase the disk space required by the
build directly from under 2GB to over 50GB, and the size of the install from
under 1GB to over 15GB.

Under some conditions, omitting some of these options may even result in a
failed `make` or `make install` step.

In the future these may become the defaults.  
If you are aware of additional time/space saving options which might be added to
this list, please use the contact info under "Bug Reports" to let us know.

### [COMPILER SELECTION] (optional)

By default, CUPC2C will be compiled using the C and C++ compilers named by the
`CC` and `CXX` environment variables, if set.  If those are not set, then `cc`
and `c++` found in `$PATH` will be used.  If this search does not result in use
of satisfactory compilers, then you can set `CC` and `CXX` or use the following
arguments to `cmake`:

```
        -DCMAKE_C_COMPILER=[YOUR C COMPILER] \
        -DCMAKE_CXX_COMPILER=[YOUR C++ COMPILER]
```

The placeholders for "YOUR" compilers accept only an executable name.  If there
is a need for arguments, such as to set the ABI, you may use the following:

```
        -DCMAKE_C_FLAGS="[YOUR C COMPILER FLAGS]" \
        -DCMAKE_CXX_FLAGS="[YOUR C++ COMPILER FLAGS]"
```

### [TARGET-SPECIFIC SETTINGS] (required, when applicable)

On macOS the following are typically required, and when they are not required
they are harmless.  So, the following should be used on macOS:

```
        -DCMAKE_CXX_FLAGS="-Wno-deprecated-declarations" \
        -DDEFAULT_SYSROOT=/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk \
        -DLLVM_ENABLE_LIBCXX:BOOL=TRUE
```

Note: if you are already passing `-DCMAKE_CXX_FLAGS="..."` then
`-Wno-deprecated-declarations` should be added to the quoted string, rather
than having multiple `CMAKE_CXX_FLAGS` settings.

There are currently no target-specific settings for other targets.

### [PTS SETTINGS] (optional)

CUPC2C is used to translate UPC source code to C source code with calls to a
runtime library. The runtime library can use a choice of different C data types
to represent a UPC pointer-to-shared (PTS).  The default representation is
suitable for most uses, but can be overridden in the `cmake` step.  Guidance in
choosing a PTS representation is beyond the scope of this document.  If you
wish to use a non-default representation the following arguments should be
passed to `cmake`:

For a "packed" PTS representation with field widths given by the placeholders:

```
        -DUPC_PTS=packed -DUPC_PACKED_BITS=[PHASE],[THREAD],[ADDR]
```

For the "struct" PTS representation:

```
        -DUPC_PTS=struct
```
