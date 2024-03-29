---
layout: page
title: "Clang UPC Libfabric Runtime"
description: ""
---
{% include JB/setup %}

[Libfabric](https://ofiwg.github.io/libfabric/) is
a high-performance fabric software library designed to provide
low-latency interfaces to fabric hardware.  

Clang UPC Libfabric Runtime is an implementation of Clang UPC that uses
Libfabric API for message passing between UPC threads running on separate
nodes in a system area network.

### Getting Clang UPC with Libfabric prerequisites 

Beside the regular Clang UPC prerequisites, the following is also required in
order to build libfabric support:

* Working libfabric implementation 

* SLURM job manager

* Add the location of the Libfabric library to the LD_LIBRARY_PATH
environment variable. For example,

<pre>
LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/libfabric/lib"
export LD_LIBRARY_PATH
</pre>

### Getting Clang UPC with Libfabric runtime support

Libfabric development is currently on the branch _libfabric_.  Follow the
this steps to build Clang UPC with the libfabric support:

* Follow the instructions on getting the
[Clang UPC sources](/clang-upc/install.html).

* Checkout the _libfabric_ branch of clang-upc

<pre>
cd llvm/tools/clang; git checkout libfabric
</pre>

* Follow the instructions on 
[configuring the Clang UPC](/clang-upc/config-options.html).

The following configuration options were added for Libfabric:

* __-DLIBUPC_RUNTIME_MODEL__:=fabric

Chose libfabric for the runtime support.

* __-DLIBUPC_FABRIC__:=_path/to/libfabric_

Select directory where libfabric is installed.

* __-DLIBUPC_FABRIC_DEVICE__:=_ib_device_

Select networking device to use.  Default is 'ib0'.

* __-DLIBUPC_FABRIC_PROVIDER__:=_fabric_provider_

Select fabric provider to use.  Default is 'sockets'.

* __-DLIBUPC_FABRIC_SHARED_CTX__:=_0/1_

Enable fabric check for shared endpoints.  Default is disabled.

* __-DLIBUPC_JOB_PMI_INCLUDE_DIR__:=_pmi_dir_path_

Specify directory where PMI include file is.  Default is '/usr/include/slurm'.

* __-DLIBUPC_MEMORY_ALIGNMENT__:=_4_

Alignment for local/target buffers.  Default is 4.

### Project status

* 11/13/2015 First RMA test passes on Cray GNI

* 07/01/2015 Added all remaining UPC functionality

* 01/01/2015 Added support for upc_global_exit()

* 12/26/2014 Added UPC barrier (no trigger funcs)

* 12/26/2014 Added broadcast capabilities

* 12/24/2014 Added UPC locks

* 10/28/2014 Upgrade to the latest libfabric API

* 10/17/2014 Added support for remote put/get

* 9/01/2014 Add libfabric configuration

### More information on Libfabric

* [Libfabric repository](https://github.com/ofiwg/libfabric)
