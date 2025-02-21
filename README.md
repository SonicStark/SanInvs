# SanitizerInvariants

A friend of [SanitizerCoverage](https://clang.llvm.org/docs/SanitizerCoverage.html), but for invariants to Daikon.

## Introduction

[Daikon](http://plse.cs.washington.edu/daikon/), an implementation of dynamic detection of likely invariants, provides [Kvasir](https://plse.cs.washington.edu/daikon/download/doc/daikon.html#Kvasir) as the front end for C and C++. And *Kvasir* uses [Valgrind](https://valgrind.org/) which is a framework for heavyweight DBI as its infrastructure. 

Years have been passed and nowadays people prefer to use [sanitizers](https://github.com/google/sanitizers) as an alternative to *Valgrind*. So perhaps it's the right time to try detecting invariants with state-of-the-art ﻿techniques from LLVM compiler infrastructure now, e.g. [AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer) and [MemorySanitizer](https://github.com/google/sanitizers/wiki/MemorySanitizer). And [Daikon Developer Manual - 2.7.2 Instrumenting C programs](https://plse.cs.washington.edu/daikon/download/doc/developer.pdf) also holds a positive attitude towards this:

> You may wish to infer invariants over C programs running on other platforms;
for instance, you want a robust C front end that works under Microsoft Windows.
This section will help you to either write such a front end or to hand-instrument your program to produce output that Daikon can process.

> We welcome additions and corrections to this part of the manual. And, if you write a C instrumenter
that might be of use to others, please contribute it back to the Daikon project.

> The problem of tracking C memory may seem daunting, but it is not insurmountable.
There exist many tools for detecting or debugging memory errors in C,
and they need to perform exactly the same memory tracking as a Daikon front end must perform.
Therefore, a Daikon front end can use the same well-known techniques, and possibly can even be built on top of such a tool.

> There are two basic approaches to instrumenting a C program (or a program in any other language):
instrument the source code, or instrument a compiled binary representation of the program.
In each case, additional code that tracks all memory allocations, deallocations, writes, and reads must be executed at run time.
Which approach is most appropriate for you depends on what tools you use when building your C instrumentation system.

## *SanInvs* versus *SanCov*

*SanitizerInvariants* (abbr. *SanInvs*) is designed almost same as *SanitizerCoverage* (abbr. *SanCov*), and they are friends naturally:
 - Walk and insert callbacks on LLVM IR, as a module pass.
 - Runtimes that give a default implementation of these callbacks.
 - Provide explicit identifier for callbacks, such as guard or pc.

*TODO*
