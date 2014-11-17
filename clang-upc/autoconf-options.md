---
layout: page
title: Clang UPC Autconf Options
tagline:
---
{% include JB/setup %}

Calng UPC can also be configured by using the GNU autoconf tools (configure).
In most of the cases there is no difference between _cmake_ configuration and
autoconf, except in the following areas:

* While _cmake_ configuration is capable of configuring and building multiple
  instances of the runtime, _autoconf_ is building only one of them, as
  specified by the configuration options.


### 1.1 General Options
* __--prefix__=PREFIX

  Install architecture-independent files in PREFIX [/usr/local]

* __--exec-prefix__=EPREFIX

  Install architecture-dependent files in EPREFIX [PREFIX]

* __--enable-optimized__

  Compile with optimizations enabled (default is NO)

* __--enable-profiling__

  Compile with profiling enabled (default is NO)

* __--enable-assertions__

  Compile with assertion checks enabled (default is YES)

* __--enable-werror__

  Compile with -Werror enabled (default is NO)

* __--enable-expensive-checks__

  Compile with expensive debug checks enabled (default is NO)

* __--enable-debug-runtime__

  Build runtime libs with debug symbols (default is NO)

* __--enable-debug-symbols__

  Build compiler with debug symbols (default is NO if
  optimization is on and YES if it's off)

* __--enable-keep-symbols__

  Do not strip installed executables)

### 1.2 Optional Features

* __--enable-clang-upc2c__

  Enable building of clang upc2c (default is YES)

* __--enable-clang-upc-runtime__

  Enable building of clang upc runtime (default is YES)

* __--enable-upc-link-script__

  Enable UPC's use of a custom linker script; this
  will define the UPC shared section as a no load
  section on targets where this feature is supported
  (requires GNU LD)

* __--enable-upc-backtrace__

  Enable UPC backtrace; Enable stack frame backtrace
  report when UPC run-time fatal errors occur or by
  user request (via signal)

* __--enable-upc-numa__

  Enable UPC runtime NUMA support [default='yes']

### 1.3 Optional Packages

* __--with-execinfo-lib-path__

  Specify path for execinfo library

* __--with-execinfo-inc-path__

  Specify path for execinfo include

* __--with-upc-pts__

  UPC packed or struct pointer representation.

* __--with-upc-pts-packed-bits__

  UPC packed pointer representation.

* __--with-upc-pts-vaddr-order__

  UPC vaddr first or last.

* __--with-upc-runtime__=MODEL

  Specify the runtime implementation model for UPC,
  where MODEL may be: 'SMP' (Symmetric
  Multiprocessing) or 'Portals4'. [default='SMP']

* __--with-portals4__=PATH

  Specify prefix directory for installed portals4 package

* __--with-upc-job-launcher Select UPC Portals4 job launcher [default=slurm]

### 1.4 Some influential environment variables

* __CC__

  C compiler command

* __CFLAGS__

  C compiler flags

* __LDFLAGS__

  linker flags, e.g. -L<lib dir> if you have libraries in a
  nonstandard directory <lib dir>

* __CPPFLAGS__

  C/C++/Objective C preprocessor flags, e.g. -I<include dir> if
  you have headers in a nonstandard directory <include dir>

* __CXX__

  C++ compiler command

* __CXXFLAGS__

  C++ compiler flags

* __CPP__

  C preprocessor

* __CXXCPP__

  C++ preprocessor

Use these variables to override the choices made by `configure' or to help
it to find libraries and programs with nonstandard names/locations.
