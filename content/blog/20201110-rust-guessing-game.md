---
title: "Rust で推測ゲーム(The Book chapter 2)"
date: 2020-11-10T05:57:09+09:00
draft: false
tags:
  - rust
---

## 資料

- [Programming a Guessing Game - The Rust Programming Language](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html)

### プロジェクト作成

```bash
$ cargo new guessing_game
$ cd guessing_game
$ cargo run
   Compiling guessing_game v0.1.0 (/Users/$USER/code/others/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 4.29s
     Running `target/debug/guessing_game`
Hello, world!
```

### 入力を受け付ける部分の作成

資料通りコードを書いていく

```rust
use std::io;

fn main() {
    println!("Guess the number!");
    println!("Please input your guess.");

    let mut guess = String::new();
    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

- `println!` は文字列を出力するマクロ
    - マクロは末尾に `!` がつく
- `let mut` は mutable な変数の作成（ `let` は immutable）
- `String::new` の `new` は String の associated function
    - 一部言語で言う static method
    - `new` は新しい値を作るときによく使う名前
        - コンストラクタとかはないのかな？
- `.read_line()` `.expect()` はメソッド呼び出し
- `read_line` は標準入力を引数の文字列に書き出す
- `&mut guess` の `&` は参照(reference)渡し
    - 何もつけないと値渡し
- `&mut guess` の `mut` は参照を mutable にするもの
    - 何もつけないと immutable
- [`expect`](https://doc.rust-lang.org/std/result/enum.Result.html#method.expect) は `Result` のメソッド
    - `Result` は `Ok` `Err` からなる Enum で Rust の標準ライブラリではよく使われる
    - `expect` は `Ok` なら単にその値を返し `Err` なら引数の文字列を出力してクラッシュする
    - このプログラムで `expect` を呼ばない場合コンパイル時警告になる（エラーハンドリングがないため）
- `println!` 内の　`{}` は変数を埋め込むプレースホルダ（複数可）
- メソッド呼び出しは1つ1つ改行するのが推奨
    - エディタでもその形に合わせてフォーマット & メソッドごとに返り値の型を表示してくれる（以下は VSCode + [rust-analyzer](https://marketplace.visualstudio.com/items?itemName=matklad.rust-analyzer) の表示）
    ![return type view](/20201110-rust-guessing-game/return-type-view.png)


### 乱数生成部分の作成
