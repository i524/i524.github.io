---
title: "20201109 Hugo で github pages にコンテンツを公開する"
date: 2020-11-09T09:48:13+09:00
draft: false
tags:
  - hugo
---

## 資料

- [Hugo + GitHub Pages + 無料で洒落たブログを30分で作る - Qiita](https://qiita.com/yotsak/items/017734d5f873f4f194d4)
- [Quick Start | Hugo](https://gohugo.io/getting-started/quick-start/)
- [Host on GitHub | Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

## 手順

### Hugo のインストール

```bash
brew install hugo
```

### サイト作成

```bash
hugo new site $USER.github.io
cd $USER.github.io
```

#### テーマ設定

今回は [Simpleness | Hugo Themes](https://themes.gohugo.io/simpleness/) を使う

```bash
echo 'theme = "pickles"' >> config.toml
git submodule add https://github.com/mismith0227/hugo_theme_pickles themes/pickles
```

#### プロジェクト設定

必要に応じて書き換える

publishDir は github pages の対象ディレクトリなので `docs` 固定

```
baseURL = "https://i524.github.io/"
languageCode = "ja-jp"
title = "1日1時間"
theme = "simpleness"
publishDir = "docs"
```

#### コンテンツ追加


```bash
hugo new blog/20201109-hugo-github-pages.md
```

動作確認は以下で

```bash
hugo server -D
```

#### デプロイ

```bash
hugo
```

これで docs ディレクトリに html 等が生成されるので push する
