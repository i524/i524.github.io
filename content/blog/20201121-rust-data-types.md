---
title: "Rust のデータ型"
date: 2020-11-22T07:57:00+09:00
draft: false
tags:
  - rust
---

## 資料

- [Data Types - The Rust Programming Language](https://doc.rust-lang.org/book/ch03-02-data-types.html)

## Rust の型

Rust の型は `Scalar` と `Compound` に分類される

### Scalar Types

- Scalar は単一の値
- Integer
    - signed/unsigned の 8, 16, 32, 64, 128 bit + システム（32bit OS なら 32bit, 64bit OS なら 64bit）
    - signed 8bit なら `i8`, unsigned 64bit なら `u64`, システムは `isize/usize`
    - リテラルの書き方:
        - 数値の末尾に型を明記できる(`57u8`, `-120i32`)
        - `_` を間に入れて良い(`1_000`)
        - 16進数(`0xff`)
        - 8進数(`0o77`)
        - 2進数(`0b1111_0000`)
        - バイト（`u8`のみ）(`b'A'`)
    - 迷ったら Rust デフォルトの i32 を使おう（64bitOS でも i32 のほうが高速）
        - `isize/usize` はコレクションのインデックス等で使う
    - オーバーフロー時の挙動はコンパイル時のモードで異なる
        - debug モードではその場で異常終了（`panic`）
        - release モード（`--release` オプション）では wrap される:最大値を超えると最小値になる（`u8` なら `255 + 1` は `0` になる）
            - 明示的にこの挙動が欲しい場合は標準ライブラリの [Wrapping](https://doc.rust-lang.org/std/num/struct.Wrapping.html) を使おう
- Float
    - `f32` `f64` がありデフォルトは `f64`
        - 今のシステムでは計算速度はそれほど変わらず、 `f64` のほうが精度高いため
- Boolean
    - `bool` `true/false`
- Character
    - `char`
    - シングルクォートで囲う(`'z'`)（ダブルクォートは文字列）
    - Rust の Character は4バイトなので emoji 等も表現できる
    - `U+0000` ~ `U+D7FF`, `U+E000` ~ `U+10FFFF` に対応

### Compound Types

- Compound は複数の値を１つの型で表現するもの
- Tuple
    - 複数の値をひとつの型としてまとめたもの
    - それぞれ異なる型でも良い
    - 長さを増やしたり減らしたりはできない
    - destructuring ができる（以下）
    - `x.0` のように `.` とインデックスで値を参照することも可能

```rust {hl_lines=[4]}
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("tup.0 and x has same value?: {}", tup.0 == x); // tup.0 and x has same value?: true
    println!("The value of y is: {}", y); // The value of y is: 6.4
}
```

- Array
    - Array 内の値は全て同じ型
    - 長さを増やしたり減らしたりはできない
    - データを heap より stack に置きたいときに使う（詳細は[4章](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html)）
    - 固定長以外が必要な場合は標準ライブラリの vector を使おう

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5]; // 型情報に長さを含む

let threes = [3; 5]; // [3, 3, 3, 3, 3] と等価

let first = a[0];

let tenth = a[10]; // コンパイルエラー
```
