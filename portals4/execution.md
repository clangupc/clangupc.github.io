---
layout: page
title: "Clang UPC Portals4 Runtime Execution Option"
description: ""
---
{% include JB/setup %}

     NOTE: SLUM job luncher is required to run Clang UPC Portals4 runtime
     compiled programs.

Execution of the compiled program with Portals4 support requires the Portals 4
Reference Implementation Library. Both the Portals4 shared library and job
launcher (slurm) are required to successfully run the Clang UPC
program compiled for Portals4.

By default the Portals 4 Reference Implementation Library installs in the
/usr/local directory. For most of the systems /usr/local/bin and
/usr/local/lib are already added by the system to the user’s execution and
library paths.  However, if the Portals4 library is installed in a 
different place (e.g.  /usr/local/gupc-p4) access to the shared libraries
and job launcher must be provided. There are two recommended methods for
identifying the location of the Portals4 library, prior to running a
linked UPC program:

* Add the location of the Portals4 library to the LD_LIBRARY_PATHenvironment
variable. For example,

    LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/gupc-p4/lib"
    export LD_LIBRARY_PATH

* As system administrator add an entry into the system’s shared library
configuration directory. For example (Fedora Core x86_64):

    su root
    echo '/usr/local/gupc-p4/lib' > /etc/ld.so.conf.d/portals4-x86_64.conf
    chmod a-w /etc/ld.so.conf.d/portals4-x86_64.conf
    ldconfig
    exit

Also, make sure that the yod job launcher is on your PATH. For example if your
default shell is bash:

    export PATH="/usr/local/gupc-p4/bin:$PATH"

## SLURM Launcher

Even though, Portals4 programs can be launched with the Portals4's provided
_yod_ manager, SLURM (Simple Linux Utility for Resource Management) is the
default job launcher.

For example:

    srun -n 8 upc_program

spwans 8 UPC threads over the Portals4 based network.  All the other SLURM
options should work as expected on Portals4 based UPC programs.  More info
on the [SLUM](http://slurm.schedmd.com/) option can be found on the
SPURM development webpage.

### Environment Variables

The following environment variables will affect UPC program execution.

UPC_SHARED_HEAP_SIZE
:    UPC_SHARED_HEAP_SIZE sets the maximum amount of shared heap (per UPC
thread) for the program. The default is 256MB per UPC thread. The provided heap
size value is optionally multiplied by a scaling factor. Valid scaling factor
suffixes are: K (Kilobytes), M (Megabytes), G (Gigabytes), and T(Terabytes).
For example, to allocate the heap size of one (1) Gigabyte:

    bash
      export UPC_SHARED_HEAP_SIZE=1G

    csh
      setenv UPC_SHARED_HEAP_SIZE 1G

TMP | TMPDIR
:    A path to use for file based mmap-ed node local memory access optimization.
By default /tmp is used.

UPC_NODE_LOCAL_MEM
:    Disable node local memory access optimization by setting this environment
variable to OFF. Useful for debugging purposes only.

UPC_FORCETOUCH
:    Disable startup page by page access of the local shared memory by setting
this environment variable to _0_. Page by page memory touch ensures the correct
memory affinity among threads running on the same node. Useful for faster
startup time on systems with only one thread per node.

UPC_BACKTRACE
:    Enable backtrace generation if a fatal error occurs in the UPC program. Set
this environment variable to 1 to enable backtrace. [default: disabled]

UPC_BACKTRACEFILE
:    Template for the backtrace files if explicitly requested by the user.
[default: stderr]

UPC_BACKTRACE_GDB
:    The file path of the GDB debugger that will be used to generate a
backtrace. [default: gdb]

### Node Local Memory Access Optimization

The GUPC for Portals4 runtime supports node local memory access optimization.
Access to shared memory of threads on the same node is performed via direct
memory access instead of Portals4 PUT/GET routines. Portals4 library is used to
determine which threads reside on the same node.

The node local memory access supports the following options:

POSIX
:    POSIX shared memory is used to map and access other threads shared
memories. POSIX shared objects are named as upc-mem-THREADID-PID. This is the
default configuration.

MMAP
:    File based mmap-ed memory is used to map and access other threads shared
memories. To activate this option specify --with-upc-node-local-mem=mmap as the
GUPC configuration option. By default files are created under /tmp directory.
This can be changed in the execution time by specifying the desired path with
TMP or TMPDIR environment variables. Files are named in a similar fashion as
POSIX shared objects.

Node local memory access optimization can be disabled in the configuration time
by specifying --disable-upc-node-local-mem option or by setting the environment
variable UPC_NODE_LOCAL_MEM=OFF in the execution time.

