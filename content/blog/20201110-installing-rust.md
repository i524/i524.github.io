---
title: "Rust のインストール(The Book chapter 1)"
date: 2020-11-10T05:54:36+09:00
draft: false
tags:
  - Rust
  - Rust The Book
---

## 資料

- [Installation - The Rust Programming Language](https://doc.rust-lang.org/book/ch01-01-installation.html)

```bash
brew install rustup-init
rustup-init
```

```
rustup-init                                                                                                                                                                                                              [20:20:26]

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /Users/$USER/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory located at:

  /Users/$USER/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /Users/$USER/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /Users/$USER/.profile
  /Users/$USER/.zprofile

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-apple-darwin
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with installation (default)
2) Customize installation
3) Cancel installation
>
```

デフォルトのインストールを選択

色々ログが出て最終的に

```
  stable installed - rustc 1.47.0 (18bf6b4f0 2020-10-07)


Rust is installed now. Great!

To get started you need Cargo's bin directory ($HOME/.cargo/bin) in your PATH
environment variable. Next time you log in this will be done
automatically.

To configure your current shell run source $HOME/.cargo/env
```

言われたとおり source する

```bash
source $HOME/.cargo/env
```

rustc や cargo が使えるので OK

```bash
$ rustc --version                                                                                                                                                                                                                                           [5:35:43]
rustc 1.47.0 (18bf6b4f0 2020-10-07)
$ cargo --version                                                                                                                                                                                                                                           [5:35:51]
cargo 1.47.0 (f3c7e066a 2020-08-28)
```
