---
title: "iOS の簡単な UI 作成"
date: 2020-11-28T17:19:00+09:00
draft: true
tags:
  - Swift
  - iOS
  - Xcode
---

## 資料

- [Start Developing iOS Apps (Swift): Build a Basic UI](https://developer.apple.com/library/archive/referencelibrary/GettingStarted/DevelopiOSAppsSwift/BuildABasicUI.html)
    - アプリ作成の公式ドキュメントだが情報が古い（Storyboard前提）ので使わない
- [iOS アプリの View 実装方法の関係 (SwiftUI、Storyboard、Xib、UIKit) - Qiita](https://qiita.com/os1ma/items/a8b946dba891f01ccc4e)
    - Apple のドキュメントでは Storyboard 前提だが Xcode12.2 ではデフォルトは SwiftUI （今回は SwiftUI）
- [Creating and Combining Views — SwiftUI Tutorials | Apple Developer Documentation](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views)
    - これを進めていく

## 目標

## やること

### プロジェクト作成

- Xcode 上で `Create a New Xcode Project`
- iOS, App を選択
- `Product Name`, `Organization Identifier` だけ適当に埋めて Next
- ディレクトリを選択

### View ファイルの構成

デフォルトでは以下のような `ContentView.swift` ファイルが作られる


```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, world!")
            .padding()
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

- `ContentView` の方は View 自体（表示内容とレイアウト）の定義
- `ContentView_Previews` は [preview](https://developer.apple.com/jp/news/?id=8vkqn3ih) (Xcode 上で View の表示を確認するもの)の定義
- preview 上では View 要素を ⌘ + クリックでメニューが開き、 View に対して色々設定できる
    - `Show SwiftUI Inspector...` から View の内容を変更できる（コードの方も書き換わる）
