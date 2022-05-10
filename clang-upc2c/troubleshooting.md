---
layout: page
title: CUPC2C Troubleshooting
group: none
tagline: 
---

### Troubleshooting a failed build

As noted in the [CUPC2C build instructions](./#build-instructions)
_any_ build failure experienced with `make -j[N]` should be retried with just
`make`.  If that is not sufficient to recover, the following are some known
failure modes and possible resolutions:

#### Out-of-memory when linking

Even without parallel `make`, it is possible that the link steps may require
excessive memory on some systems.  On a Linux system, failure mode can often be
distinguished by messages similar to either of the following:

```
collect2: fatal error: ld terminated with signal 9 [Killed]
compilation terminated.
```
OR
```
clang: error: unable to execute command: Killed
clang: error: linker command failed due to signal (use -v to see invocation)
```

Possible work-arounds include:

+ Retry `make` after attempting to maximize resource limits as follows.  
  For `bash` or `zsh`:
  ```
  $ ulimit -d hard
  $ ulimit -m hard
  $ ulimit -f hard
  $ ulimit -s hard
  $ ulimit -t hard
  $ ulimit -v hard  # omit on macOS
  ```
  For `tcsh`:
  ```
  $ unlimit
  ```
+ On systems where they are available, use of the `gold` or `lld` linkers may
  dramatically reduce the memory required to link.  You can try running the
  following in `[BLDDIR]` to modify the configuration, where `[LINKER]` is
  either `gold` or `lld`, followed by `make` to resume the build from the point
  at which it had previously failed.
  ```
  $ cmake -S [SRCDIR] \
        -DCMAKE_EXE_LINKER_FLAGS=-fuse-ld=[LINKER] \
        -DCMAKE_SHARED_LINKER_FLAGS=-fuse-ld=[LINKER]
  $ make
  ```
  If the chosen linker is _not_ supported, this command will just result in
  _different_ link failures.  One can restore the default behavior by giving
  empty values for the `CMAKE_*_LINKER_FLAGS` settings:
  ```
  $ cmake -S [SRCDIR] \
        -DCMAKE_EXE_LINKER_FLAGS= \
        -DCMAKE_SHARED_LINKER_FLAGS=
  ```
+ If passing the recommended `-DCMAKE_BUILD_TYPE=Release` to `cmake`, try using
  the `MinSizeRel` build type instead.  This results in smaller code, at a
  slight cost in the performance of source-to-source translation.  However, this
  has *no* impact on the quality or performance of translated UPC code.  This
  can be done by modifying the configuration without starting over.
  ```
  $ cmake -S [SRCDIR] -DCMAKE_BUILD_TYPE=MinSizeRel
  $ make
  ```
+ If passing a `-DCMAKE_BUILD_TYPE` other than `Release` or `MinSizeRel` to
  `cmake`, consider using the build type with the least debugging and greatest
  optimization which can meet your needs.  Description of the build types
  supported by CMake and the LLVM infrastructure is beyond the scope of this
  document.
