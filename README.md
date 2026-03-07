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

## Rust support
Not tested yet

## Status
- [x] Build with GCC(some project not testedvyet)
- [x] Build self
- [ ] Build with Rust(some thing is wrong)
- [x] Build simpile program and run normally
- [ ] Build kernel and run normallt

## Branch for building
use ollvm* branch to build llvm

## License
follow upstream
