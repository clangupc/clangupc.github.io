---
layout: page
title: "Clang UPC Configuration Options"
description: ""
categories: clang-upc
---
{% include JB/setup %}

The first step of building Clang UPC is the configuration of the source code
to better suite the user.  As mentioned before, _cmake_ (preferred fo Clang
UPC) or _configure_ is used for this purpose.  Beside the regular [Clang/LLVM
configuration options[(http://llvm.org/docs/CMake.html#llvm-specific-variables),
Clang UPC provides some additional options that can be used to configure
UPC language as well as the selected runtime.

### 1.1 General Options

* __-DCMAKE_INSTALL_PREFIX:PATH__:=_directory_

  Sets the installation prefix. This follows the standard
  convention. Executables are placed in _directory/bin_,
  library files go in _directory/lib_ and so on. The default
  is _/usr/local_.

* __-DCMAKE_BUILD_TYPE__:=[__Debug__\|__Release__]

  Possible values are empty (no optimization, no debug info),
  _Debug_ (No optimization, debug info), _Release_ (optimization,
  no debug info), _RelWithDebInfo_ (optimization, debug info),
  _MinSizeRel_ (_-Os_, no debug info). Defaults to None.

* __-DLLVM_TARGETS_TO_BUILD__:=_semicolon-separated-list_

  Specifies a list of architectures for which Clang will be able
  to generate code. Clang UPC supports _x86_ and _PowerPC_.
  Other targets supported by LLVM can be built, but they may or
  may not work. Defaults to _all_.

* __-DCMAKE_C_COMPILER__:=_path-to-c-compiler_

  Specify the C compiler used by the build process.

* __-DCMAKE_CXX_COMPILER:=_path-to-c++-compiler_

  Specify the C++ compiler used by the build process.

### 1.2 UPC Language Options

The following options control the UPC compiler generated code.

* __-DUPC_PTS__:=[__packed__\|__struct__]

  Default UPC pointer to shared representation. Defaults to _packed_.

* __-DUPC_PACKED_BITS__:=_comma-separated-list_

  Default UPC packed pointer to shared bits per field
  (phase,thread,addr). Defaults to '20,10,34'.

* __-DUPC_PTS_VADDR_ORDER__:=[__first__\|__last__]

  Default UPC pointer to shared field order.  Defaults to first.

* __-DLIBUPC_CONFIGURATIONS__:=_semicolon-separated-list_

  Controls the library variants that will be built. Each
  representation of UPC pointers requires a separate library.

  p
   : Indicates the packed representation. (default)

  s
   : Use the struct representation.

  f
   : Put the virtual address field last. (default)

  l
   : Put the virtual address field last.

  phase-thread-address
   : Specify the bits in the packed representation. (default 20-10-34)

  Thus, _p;s;p-l-18-14-32_ would build three library variants.
  _p` is the default, _s_ is for _-fupc-pts=struct_, and
  _p-l-18-14-32_ is for
  _-fupc-packed-bits=18,14,32 -fupc-pts-vaddr-order=last_.

  The default is to build 4 library variants, _p;s;p-l;s-l_,
  corresponding to _-fupc-pts=[packed\|struct]_ and
  _-fupc-pts-vaddr-order=[first\|last]_.

### 1.3 Linking Options

* __-DLIBUPC_ENABLE_LINK_SCRIPT__:=[TRUE\|FALSE]

  Enable UPC's use of a custom linker script. This option must
  turned of for systems without the GNU LD (e.g. Mac OS X).

### 1.4 Runtime Debugging Options

* __-DLIBUPC_ENABLE_BACKTRACE__:=[__TRUE__\|__FALSE__]

  Enable stack frame backtrace report when UPC runtime fatal
  errors occur or by user request (via signal) (TRUE by default).

* __-DLIBUPC_ENABLE_BACKTRACE_ADDR2LINE__

  Enable usage of addr2line for program backtrace on fatal
  errors or on user's request.

* __-DLIBUPC_BACKTRACE_ADDR2LINE__:=_path-to-addr2line_

  Path of the addr2line for program backtrace on fatal
  errors or on user's request.

* __-DLIBUPC_ENABLE_BACKTRACE_GDB__

  Enable usage of GDB for program backtrace on fatal errors.

* __-DLIBUPC_BACKTRACE_GDB__:=_path-to-gdb_

  Path to gdb executable used for program backtrace on fatal events.

* __-DLIBUPC_ENABLE_BACKTRACE_SIGNAL__

  Enable usage of signals for backtrace on user's request (SIGUSR1 by default).

* __-DLIBUPC_BACKTRACE_SIGNAL__:=_signal_

  Specify signal name used of backtrace on user's request.
  Defauls to _SIGUSR1_.

### 1.5 Runtime Options

* __-DLIBUPC_MAX_LOCKS__:=_count_

  The maximum number of locks that can be held by a single UPC thread.

* __-DLIBUPC_MEMORY_PAGE_SIZE__=_number-of-bytes_

  Select target memory page size (4096 by default)

* __-DLIBUPC_TREE_FANOUT__=_count_

  The maximum number of children in each sub-tree used to implement
  UPC collectives operations (e.g. upc_barrier) (4 by default).

* __-DLIBUPC_RUNTIME_MODEL__:=[__smp__\|__portals4__]`

  Specify the runtime implementation model for UPC, where model may be:
  'smp' for symmetric multiprocessing or 'portals4' for Infiniband with
  Portals4 package.

### 1.6 SMP Runtime Options

* __-DLIBUPC_ENABLE_AFFINITY__:=[True\|False]

  Enable UPC thread process affinity.

* __-DLIBUPC_ENABLE_NUMA__:=[True\|False]

  Enable UPC thread processor/memory NUMA affinity.

### 1.7 Portals 4 Runtime Options

Some of the configuration options are included to support the
Infiniband (Portals4) based runtimes:

* __-DLIBUPC_POTALS4__:=_path-to-portals-package-install_

  Directory path for installed Portals4 package (e.g. /usr/local/portals4).

* __-DLIBUPC_JOB_LAUNCHER__:=[__slurm__\|__yod__]`

  Specify the job launcher for Infiniband based runtime (slurm by default)

* __-DLIBUPC_BOUNCE_BUFFER_SIZE__:=_size_`

  The size (in bytes) of the bounce buffer that is used by the UPC
  runtime to buffer network data (256Kb by default).

* __-DLIBUPC_GLOBAL_EXIT_TIMEOUT__:=_seconds_

  upc_global_exit() time to wait for other threads to exit
  (2 seconds by defualt).

* __-DLIBUPC_PTE_BASE__:=_number_

  Base index of the first Portals4 PTE used by the UPC runtime
  (16 by default)

* __-DLIBUPC_ENABLE_TRIGGERED_OPS__:=[__0__\|__1__]

  Enable UPC runtime support for Portals4 triggered operations
  (enabled by default)

* __-DLIBUPC_MAX_OUTSTANDING_PUTS__:=_count_

  Maximum number of outstanding Portals 4 put operations (256 by default)

* __-DLIBUPC_LOCAL_MEM__:=[__posix__\|__mmap__\|__none__]`

  Specify type of shared memory used for node local memory accesses
  (posix by default). Option _none_ disables node local memory accesses.

* __-DLIBUPC_ENABLE_RUNTIME_CHECKS__:=[0\|1]
   
  Enable internal UPC runtime checks that validate arguments,
  and check for inconsistent runtime state (off (0) by default).

* __-DLIBUPC_ENABLE_RUNTIME_DEBUG__:=[0\|1]

  Enable UPC runtime debugging mode (off (0) by default).

* __-DLIBUPC_ENABLE_RUNTIME_STATS__:=[0\|1]

  Enable internal UPC runtime statistics collection support;
  these statistics count the number of various significant
  internal operations, and dump those counts into a per-process
  statistics file (off (0) by default).

* __-DLIBUPC_ENABLE_RUNTIME_TRACE__:=[0\|1]

  Enable internal UPC runtime trace collection support;
  a runtime trace is a time stamped log that records
  various significant internal events; this trace is written
  to a per-process log file (off (0) by default).

