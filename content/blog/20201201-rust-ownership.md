---
title: "20201201 Rust の所有権とは（The Book Chapter 4.1）"
date: 2020-12-01T06:07:47+09:00
draft: true
tags:
  - Rust
  - Rust The Book
---

## 資料

- [What is Ownership? - The Rust Programming Language](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html)

## 所有権（Ownership）とは

- 全てのプログラムはメモリを管理する必要がある
    - 言語によってガベージコレクションや明示的 allocate/free といった方法がある
- Rust は所有権によってメモリを管理する
    - 所有権は実行速度を一切低下させない

## Stack と Heap

- Stack は固定長のデータしか置けない LIFO の領域、早い
- Heap は必要なだけの長さを保有できる領域、遅い
    - Heap にデータを置いたらその位置情報をポインタとして Stack に置く
- 所有権の目的は Heap 内のデータを管理しできるだけ無駄に使わないこと、使い終わったら解放すること

## 所有権のルール

以下の3つのルールがある:

- すべての値は「所有者」と呼ばれる変数を持つ
- 所有者は一度にひとつだけ存在する
- 所有者がスコープ外になると、値が破棄される

## 変数スコープ

普通に変数を宣言した場合はスコープの終わりまで有効

```rust
{                       // s は宣言されてないので無効
    let s = "hello";    // ここから s は有効
}                       // スコープが終わったので s は無効
```

