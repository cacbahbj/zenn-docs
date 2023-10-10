---
title: "Atom後継のPulsarを使う"
emoji: "🗂"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["mac", "atom", "エディタ"]
published: true
---
# はじめに

2022年に開発の終了したAtomエディタですが、以下の後継エディタが出ています
https://pulsar-edit.dev/
https://atom-community.github.io/

方向性の違いでコミュニティが分裂したようですが、
GitHubでスター数の多いPulsarを使ってみます

# インストール

dmgファイルをDLしても良いですが、brewを使ってインストールします
https://brew.sh/ja/

```
% brew install --cask pulsar
```

# パッケージ管理

## ppm

Atomと同様にパッケージマネージャがあります
https://github.com/pulsar-edit/ppm

`ppm`コマンドはPulsarをインストールすると同時にインストールされます

## Atomからパッケージ一覧を取得してインストール

大体のパッケージはそのまま使えるそうなのでコマンドで移行します
（新規にインストールの場合は次項参照）
```
apm list -bi | sed -E "s/@.+//g" > atom_packages.txt
ppm install --packages-file atom_packages.txt --verbose
```

## パッケージをまとめてインストール

以下のようにパッケージ名を並べて`pulsar_packages.txt`ファイルを作成します
```
atom-beautify
file-icons
highlight-selected
japanese-menu
minimap
minimap-bookmarks
minimap-cursorline
minimap-find-and-replace
minimap-git-diff
minimap-highlight-selected
minimap-selection
pretty-json
show-ideographic-space
```

※それぞれの詳細はこちらで検索できます
https://web.pulsar-edit.dev/packages

コマンドで実行
```
ppm install --packages-file pulsar_packages.txt --verbose
```
