---
title: "Rust で推測ゲーム(The Book chapter 2)"
date: 2020-11-18T06:57:09+09:00
draft: false
tags:
  - Rust
  - Rust The Book
---

## 資料

- [Programming a Guessing Game - The Rust Programming Language](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html)

### プロジェクト作成

```bash
$ cargo new guessing_game
$ cd guessing_game
$ cargo run
   Compiling guessing_game v0.1.0 (/path/to/guessing_game)
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
    ![return type view](/blog/20201110-rust-guessing-game/return-type-view.png)


### パッケージのインストール

乱数生成部分を処理するパッケージをインストールする

`cargo.toml` に以下を追加

```toml
[dependencies]
rand = "0.5.5"
```

`cargo build` でパッケージのダウンロードとコンパイルが走る

バージョン指定の `0.5.5` は semver 指定で `^0.5.5` の短縮形（`^0.5.5` でも可）

```
$ cargo build
   Compiling rand_core v0.3.1
   Compiling rand_pcg v0.1.2
   Compiling rand_jitter v0.1.4
   Compiling rand_os v0.1.3
   Compiling rand_chacha v0.1.1
   Compiling rand_hc v0.1.0
   Compiling rand_xorshift v0.1.1
   Compiling rand_isaac v0.1.1
   Compiling rand v0.6.5
   Compiling guessing_game v0.1.0 (/path/to/guessing_game)
    Finished dev [unoptimized + debuginfo] target(s) in 2.17s
```

2回目以降はパッケージがダウンロード済みで、コードにも差分がなければ何も実行されずに終わる

```
$ cargo build
    Finished dev [unoptimized + debuginfo] target(s) in 0.04s
```

### 乱数生成部分の追加

```rust {hl_lines=[1,7]}
use rand::Rng;
use std::io;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("Please input your guess.");
```

- `rand::Rng` は rand のメソッド使う場合に必要（詳細は chapter 10）
- `gen_range(a, b)` は a <= n < b な整数 n を生成する
- 依存している crate のドキュメントは `cargo doc --open` でドキュメント生成してブラウザで見られる

### 入力と答えの比較


```rust {hl_lines=[3 19 23 24 25 26 27]}
use rand::Rng;
use std::io;
use std::cmp::Ordering;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1, 101);

    println!("The secret number is: {}", secret_number);

    println!("Please input your guess.");

    let mut guess = String::new();
    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed: {}", guess);

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```

- String の `parse` メソッドは数値型へのキャスト(`Result` を返す)
- guess は変数名がかぶるが前に宣言した変数を上書きできる(Shadowing)
- `Ordering` は `Result` 同様 Enum で `Less`, `Greater`, `Equal` からなる
- `cmp` メソッドは比較した結果を Ordering で返す
- `match` はパターンマッチ
    - パターンごとの処理を書くひとつひとつの行は `arm` と呼ぶ


### ループで複数の入力を受け取る

```rust {hl_lines=[1,9]}
loop {
        // 略

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
```

- `loop` は無限ループ
- 正解したら `break` でループを抜ける

### 不正な入力のハンドリング

数値以外の入力を受け取った際は無視するように変更する

```rust
        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };
```

- `_` は全ての条件が当てはまる
- `continue` で loop の次の iteration に進む
    - ここに `continue` 書けるの妙な感じ


ここまでで完成
