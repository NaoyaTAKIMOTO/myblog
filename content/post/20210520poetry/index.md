---
title: "mac os でpoetryによるpythonの環境構築"
description: ""
date: "2021-05-20T20:53:52+09:00"
thumbnail: "/img/man-593333_1920.jpg"
tags: [環境構築,python]
---
pythonのライブラリをインストールする方法としてメジャーなpip

より開発環境のバージョン管理に特化した高機能なpoetry

pyenvとの連携は公式でサポートしているっぽい。

mac os での導入方法とハマったところをメモしておく
## poetry の利点
- ライブラリの依存関係を整理できる
  - 意外とライブラリのバージョンによって良からぬ副作用が起こることがある
  - 環境を再現しようとしてライブラリのバージョンやインストールの順番でエラーがでる
  - 環境構築は人間が頭を悩ませてもしょうなない部分なのでできれば自動化したい
  - また依存関係に考慮してライブラリのバージョンをアップデートできるっぽい
  - そしてその状態を記録してくれる
- git のbranchによって依存関係の記録を切り分けられる？
- pip　とインストールできるライブラリに遜色がない
  - pypyとかの参照先が一緒なのか？
- 使い勝手がpipと大差ない
  - pip install の代わりにpoetry add

## 導入方法
mac os の場合、下記のコマンドを実行する。

    curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -

.zprofile へ下記の行を追記してzshへのパスを通す。
```sh
export PATH="HOME/.poetry/bin:$PATH"
```

下記のコマンドでインストールが成功していることを確認する。

    poetry --version

## 使い方
- プロジェクトの作成

    poetry new projec_name

なんか色々のものが生成される

- ライブラリのインストール

    poetry add library_name

- 環境の再現
poetry.lockがあるディレクトリで下記のコマンドを実行する

    poetry install

## ハマったところ
- homebrew でインストール
  - よくわからんが上手く動かなかった
  - pyenvでの仮想環境ではなく、システムデフォルトのpythonに紐付いているようだった
- zshへのパスを手動で通す必要がある
  - poetryのインストール時に環境変数通しといたで！みたいな表示が出た気がしたが、自動では設定されないものらしい

## requirements.txtに手を焼く必要がなくなるのならよいのでは？
- poetryの導入自体はそんなに難しくない
- poetryの運用自体も簡単そう
- 依存関係を考慮した環境再現ができるのでよさげ
- パスはちゃんと通す

