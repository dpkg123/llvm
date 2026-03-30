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
- [x] Build Rust(see rust part)
- [x] Build simpile program and run normally
- [ ] Build kernel and run normally(not tested yet)
- [x] Build Rust program with this toolchain(test some samples with Arkari)
- [ ] Run LLVM testsuite(not tested yet)

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

Arkari need [drop i386 detect](https://github.com/dpkg123/llvm/commit/2a5ca93c9bce1f5d920a4e650ceb85d37cbec959) in compiler-rt to bootstrap rust.

## License
follow upstream
