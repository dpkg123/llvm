# The LLVM Compiler Infrastructure

## Introduction

Obfuscator-LLVM is an open-source extension project based on the LLVM compiler framework, mainly used for program code obfuscation and protection.

OLLVM is based on LLVM's Pass plugin mechanism, adding code obfuscation functions during the optimization stage, thereby increasing the difficulty of reversing binary programs.

One of the goals of this repository is to provide relatively good code obfuscation support while building a toolchain that is infinitely close to the [AOSP prebuilt C/C++ toolchain](https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86).

## Source
- [AOSP llvm-project](https://android.googlesource.com/toolchain/llvm-project/)
- [upstream llvm-project](https://github.com/llvm/llvm-project)
- [AOSP llvm_android](https://android.googlesource.com/toolchain/llvm_android)
- [ARKARI](https://github.com/KomiMoe/Arkari) on clang21+ or [ollvm-adaplite-clang](https://github.com/ollvm-adaplite/ollvm-clang) on clang 21 for obfuscation support

## Status
- [x] Build with GCC(clang + lld)
- [x] Build self(with same)
- [ ] Build Rust(see rust part)
- [x] Build simpile program and run normally
- [ ] Build kernel and run normally
- [ ] Build Rust program with this toolchain(not tested yet)
- [ ] Run LLVM testsuite(with same)

## Branch for building
use ollvm* branch to build llvm

## Rust support
Build failed for rustc stage1 compiler artifacts with ollvm-adaplite-clang:
```
Building stage1 compiler artifacts (stage0 -> stage1, x86_64-unknown-linux-gnu)
...
Compiling unwind v0.0.0 (/workspace/llvm/llvm/out/src/rust/library/unwind)
std::mt19937_64 seeded with current timestamp: 1772943110852
Initializing Hikari Core with Revision ID:e8b3b881f0e5103a11ddb6eb0a3ea7b9e78fa657
Running Hikari On memchr.3c5f4c5b136ccbdf-cgu.0
Doing Post-Run Cleanup
Hikari Out
Spend Time: 0.0005970s
rustc exited with signal: 6 (SIGABRT) (core dumped)
```

Arkari can not compiler-rt yet:
```
[8/4939] Building C object projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/truncsfhf2.c.o
FAILED: projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/truncsfhf2.c.o
CCACHE_CPP2=yes CCACHE_HASHDIR=yes CCACHE_SLOPPINESS=pch_defines,time_macros /usr/bin/ccache /usr/bin/cc -DVISIBILITY_HIDDEN -D_GLIBCXX_USE_CXX11_ABI=1 -D_GNU_SOURCE -D__STDC_CONSTANT_MACROS -D__STDC_FORMAT_MACROS -D__STDC_LIMIT_MACROS -I/workspace/llvm/llvm/out/projects/compiler-rt/lib/builtins -I/workspace/llvm/compiler-rt/lib/builtins -I/workspace/llvm/llvm/out/include -I/workspace/llvm/llvm/include -I/workspace/llvm/compiler-rt/lib/builtins/../../../third-party/siphash/include -fPIC -fno-semantic-interposition -Werror=date-time -w -fdiagnostics-color -ffunction-sections -fdata-sections -Wall -Wno-unused-parameter -O3 -DNDEBUG -m32 -fno-lto -Werror=array-bounds -Werror=uninitialized -Werror=shadow -Werror=empty-body -Werror=sizeof-pointer-memaccess -Werror=sizeof-array-argument -Wformat -nostdinc++ -Werror=builtin-declaration-mismatch -Wno-c2y-extensions -DCOMPILER_RT_HAS_FLOAT16 -std=gnu11 -MD -MT projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/truncsfhf2.c.o -MF projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/truncsfhf2.c.o.d -o projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/truncsfhf2.c.o -c /workspace/llvm/compiler-rt/lib/builtins/truncsfhf2.c
cc1: warning: command-line option ‘-nostdinc++’ is valid for C++/ObjC++ but not for C
In file included from /workspace/llvm/compiler-rt/lib/builtins/fp_trunc_impl.inc:39,
                 from /workspace/llvm/compiler-rt/lib/builtins/truncsfhf2.c:11:
/workspace/llvm/compiler-rt/lib/builtins/fp_trunc.h:107:35: error: ‘dst_t’ undeclared here (not in a function); did you mean ‘dstBits’?
  107 | static const int dstBits = sizeof(dst_t) * CHAR_BIT;
      |                                   ^~~~~
      |                                   dstBits
/workspace/llvm/compiler-rt/lib/builtins/fp_trunc.h:166:21: error: expected ‘=’, ‘,’, ‘;’, ‘asm’ or ‘__attribute__’ before ‘dstFromRep’
  166 | static inline dst_t dstFromRep(dst_rep_t x) {
      |                     ^~~~~~~~~~
/workspace/llvm/compiler-rt/lib/builtins/fp_trunc_impl.inc:45:23: error: expected ‘=’, ‘,’, ‘;’, ‘asm’ or ‘__attribute__’ before ‘__truncXfYf2__’
   45 | static __inline dst_t __truncXfYf2__(src_t a) {
      |                       ^~~~~~~~~~~~~~                                                                          /workspace/llvm/compiler-rt/lib/builtins/truncsfhf2.c:15:32: error: expected ‘=’, ‘,’, ‘;’, ‘asm’ or ‘__attribute__’ before ‘__truncsfhf2’
   15 | COMPILER_RT_ABI NOINLINE dst_t __truncsfhf2(float a) {
      |                                ^~~~~~~~~~~~
/workspace/llvm/compiler-rt/lib/builtins/truncsfhf2.c:28:17: error: unknown type name ‘dst_t’
   28 | COMPILER_RT_ABI dst_t __gnu_f2h_ieee(float a) { return __truncsfhf2(a); }
      |                 ^~~~~                                                                                         cc1: note: unrecognized command-line option ‘-Wno-c2y-extensions’ may have been intended to silence earlier diagnostics
[9/4939] Building C object projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/extendhfxf2.c.o
FAILED: projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/extendhfxf2.c.o
CCACHE_CPP2=yes CCACHE_HASHDIR=yes CCACHE_SLOPPINESS=pch_defines,time_macros /usr/bin/ccache /usr/bin/cc -DVISIBILITY_HIDDEN -D_GLIBCXX_USE_CXX11_ABI=1 -D_GNU_SOURCE -D__STDC_CONSTANT_MACROS -D__STDC_FORMAT_MACROS -D__STDC_LIMIT_MACROS -I/workspace/llvm/llvm/out/projects/compiler-rt/lib/builtins -I/workspace/llvm/compiler-rt/lib/builtins -I/workspace/llvm/llvm/out/include -I/workspace/llvm/llvm/include -I/workspace/llvm/compiler-rt/lib/builtins/../../../third-party/siphash/include -fPIC -fno-semantic-interposition -Werror=date-time -w -fdiagnostics-color -ffunction-sections -fdata-sections -Wall -Wno-unused-parameter -O3 -DNDEBUG -m32 -fno-lto -Werror=array-bounds -Werror=uninitialized -Werror=shadow -Werror=empty-body -Werror=sizeof-pointer-memaccess -Werror=sizeof-array-argument -Wformat -nostdinc++ -Werror=builtin-declaration-mismatch -Wno-c2y-extensions -DCOMPILER_RT_HAS_FLOAT16 -std=gnu11 -MD -MT projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/extendhfxf2.c.o -MF projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/extendhfxf2.c.o.d -o projects/compiler-rt/lib/builtins/CMakeFiles/clang_rt.builtins-i386.dir/extendhfxf2.c.o -c /workspace/llvm/compiler-rt/lib/builtins/extendhfxf2.c
cc1: warning: command-line option ‘-nostdinc++’ is valid for C++/ObjC++ but not for C
In file included from /workspace/llvm/compiler-rt/lib/builtins/fp_extend_impl.inc:38,
                 from /workspace/llvm/compiler-rt/lib/builtins/extendhfxf2.c:11:
/workspace/llvm/compiler-rt/lib/builtins/fp_extend.h:57:9: error: ‘_Float16’ is not supported on this target             57 | typedef _Float16 src_t;                                                                                             |         ^~~~~~~~                                                                                              cc1: note: unrecognized command-line option ‘-Wno-c2y-extensions’ may have been intended to silence earlier diagnostics
```

## License
follow upstream
