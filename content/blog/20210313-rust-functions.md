---
title: "Rust の関数（The Book Chapter 3.3）"
date: 2021-03-14T08:15:05+09:00
draft: false
tags:
  - Rust
  - Rust The Book
---

## 資料

- [Functions - The Rust Programming Language](https://doc.rust-lang.org/book/ch03-03-how-functions-work.html)

## 関数の書き方

```rust
fn main() {
    println!("{}", add_two_values(4, 5));
    another_function();
}

fn add_two_values(x: i32, y: i32) -> i32 {
    x + y
}

fn another_function() {
  println!("another");
}
```

- 関数名・変数名はスネークケース
- 返り値は式だけ書く(セミコロンを書かない)
- 返り値がない場合省略できる

## 関数本体

- 関数本体は複数の文（statement）と末尾の式（expression）からなる（式はなくてもよい）
    - 変数宣言と関数定義は文、それ以外はだいたい式
    - 式の末尾に `;` を置くと文になる

ブロックも式:

```rust
let y = {
  let x = 3;
  x + 1
}; // -> y == 4
```

