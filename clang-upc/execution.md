---
layout: page
title: "Clang UPC Program Execution"
description: ""
---
{% include JB/setup %}

To execute a UPC program that has been compiled and linked with Clang UPC SMP
runtime simply invoke it with appropriate options. There are several options
that are recognized and used by the UPC runtime; these options are specified on
the command line when you invoke a UPC program. Before calling the "main()"
function of a UPC program, the UPC runtime removes all options that begin with
the prefix -fupc- and that immediately follow the UPC program name on the
command line.

    UPC_program [number of threads] [heap size] [affinity options] [program arguments]

### Execution (Runtime) Options

The following runtime options are available:

* **-fupc-threads-N** \| **-n N**<br />
Specifies, at runtime, the number of parallel execution threads as N. If
the UPC program was not compiled with the _-fupc-threads-N_ option, either the
_-fupc-threads-N_ or _-n N_ command-line option is required when you invoke the UPC
program.

* **-fupc-heap-HEAPSIZE**<br />
Specifies the size of the heap available to each thread as HEAPSIZE. A
suffix of K indicates that HEAPSIZE is expressed in kilobytes (210 bytes). A
suffix of M indicates that HEAPSIZE is expressed in megabytes (220 bytes). A
suffix of G indicates that HEAPSIZE is expressed in gigabytes (230 bytes). If a
suffix is not present, HEAPSIZE is expressed in bytes. If the
_-fupc-heap-HEAPSIZE_ option is not supplied, the runtime system will use a
default heap size of 16 megabytes per thread.

The following options specify thread scheduling and Non-Uniform Memory Access
(NUMA) policies:

* **-sched-policy** [**cpu**\|**strict**\|**node**\|**auto**]<br />
Specifies the scheduling policy for threads. Default is auto.

    cpu
     :  specifies that threads are evenly scheduled over available CPUs.
        (A CPU is a processor with a single core or a core unit in a
        multicore processor.)

    strict
     :  similar to cpu scheduling except that one to one mapping of threads
        and CPUs is required.

    node
     : specifies that threads are scheduled on nodes if a NUMA-aware kernel
       is available.

    auto
     : specifies that the UPC runtime should not manage scheduling of UPC
       threads.

* **-sched-cpu-avoid n1,n2,..**<br />
Specifies the availability of CPUs for UPC thread scheduling. The UPC
runtime will not schedule any thread on the specified CPUs.

* **-mem-policy** [**node**\|**strict**\|**auto**]<br />
Specifies the memory allocation policy if a NUMA-aware kernel is available.
Default is auto.

    node
     :  allocates memory first from the node on which a thread is scheduled to run.

    strict
     :  allocates memory only from the node on which a thread is scheduled to run.

    auto
     :  lets the kernel decide the memory allocation policy.

### Environment Variables

The following environment variables will affect UPC program execution.

TMP | TMPDIR
 :  Temporary directory for file based memory mapped shared space. Ideally on a
    Linux based system this should point to tempfs file system. [default: /tmp]

UPC_BACKTRACE
 :  Enable backtrace generation if a fatal error occurs in the UPC program. Set
    this environment variable to 1 to enable backtrace. [default: disabled]

UPC_BACKTRACEFILE
 :  Template for the backtrace files if explicitly requested by the user.
    [default: stderr]

UPC_BACKTRACE_GDB
 :  The file path of the GDB debugger that will be used to generate a
    backtrace. [default: gdb]

### Program Termination

The Clang UPC compiled program completes execution in several ways:

Normal completion
 :  All UPC threads execute a call to the exit procedure or return from the
main procedure. The exit code from the last UPC thread to exit is reported as
the UPC programs exit code. Conflicting exit codes from various UPC threads
are reported.

UPC global exit
 :  Upon detecting a UPC thread that exited via upc_global_exit, the monitor
thread terminates all other UPC threads. The exit code passed as an argument to
upc_global_exit is returned as the programs exit code.

Abort
 :  Upon detecting a UPC thread that exited via abort, the monitor thread
terminates all other UPC threads and aborts the UPC program.

Unhandled Signals
 :  Unhandled signal (e.g. SIGTERM, SIGINT) immediately terminates the UPC
program. Additionally, sending the SIGTERM signal individually to the monitor
thread or any of the UPC threads also terminates the UPC program.

