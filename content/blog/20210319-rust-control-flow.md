---
title: "20210319 Rust Control Flow"
date: 2021-03-19T06:29:13+09:00
draft: false
tags:
  - Rust
  - Rust The Book
---

## 資料

- [Control Flow - The Rust Programming Language](https://doc.rust-lang.org/book/ch03-05-control-flow.html)

## 概要

- 条件分岐は `if` 式（と `else`, `else if` 式）
- 繰り返しは `loop` 式、 `while` 式、 `for` 式がある

## if 式

記法は以下

```rust
let number = 3;

if number < 5 {
    println!("more than five");
} else if number == 5 {
    println!("five");
} else {
    println("less than five");
}

let condition = true;
let number2 = if condition { 5 } else { 6 };
```

- 条件部分( `number < 5` )は boolean にする必要がある（自動でキャスト等はない）
- `else` で終わる if 式は各条件のブロックの値に評価される
    - `else` で終わらない場合 `()` に評価される
    - 各ブロックの値の型が揃う必要がある

## loop 式

- `loop` は単独では無限ループを実行する
- ループを抜けるための `break` と一緒に使う
- `break` の後ろに書いた式が loop 式の結果として扱われる

```rust
let mut counter = 0;

let result = loop {
    couner += 1;
    if counter == 10 {
        break counter * 2;
    }
}; // -> 20
```

## while 式

```rust
let mut number = 3;

while number != 0 {
    println!("{}!", number);

    number -= 1;
}

println!("LIFTOFF!!!");
```

## for 式

```rust
let a = [10, 20, 30, 40, 50];

for element in a.iter() {
    println!("the value is: {}", element);
}
```

- `iter()` についてはこの時点では説明がないが [slice のメソッド](https://doc.rust-lang.org/std/primitive.slice.html#method.iter)っぽい

