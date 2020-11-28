---
title: "Rust の変数と定数(The Book chapter 3.1)"
date: 2020-11-18T07:09:31+09:00
draft: false
tags:
  - Rust
  - Rust The Book
---

## 資料

- [Variables and Mutability - The Rust Programming Language](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)

## 変数

```rust
fn main() {
    let x = 5;
    println!("The value of x is: {}", x);
    x = 6;
//  ^^^^^ cannot assign twice to immutable variable
    println!("The value of x is: {}", x);
}
```

- `let` で immutable な変数宣言できる
    - 書き換えようとするとコンパイルエラー
- `let mut` で mutable な変数宣言できる


## 定数

```rust
const MAX_POINTS: u32 = 100_000;
```

- `const` で定数宣言できる
    - 型の明示が必須
    - 名前は upper snake
    - `const mut` は不可
- グローバルスコープ含めどこにでも書ける
- ランタイムで決定される値は使えない


## Shadowing

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    let x = x * 2;

    println!("The value of x is: {}", x);
}
```

- 同じ名前で再度変数宣言することで前の変数を参照できないようにできる
    - mutable になるわけではない
- mutable 変数とは違って型の変更ができる
    - キャストする際に変数名変える必要がない

```rust
// OK
let spaces = "   ";
let spaces = spaces.len();
```

```rust
// NG
let mut spaces = "   ";
spaces = spaces.len();
//       ^^^^^^^^^^^^ expected `&str`, found `usize`
```
