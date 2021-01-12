---
title: 'Mac でpythonの環境構築'
date: 2020-06-16T04:58:00.010+09:00
draft: false
aliases: [ "/2020/06/mac-python.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }Mac でpythonの環境構築

Mac でpythonの環境構築[](#Mac_でpythonの環境構築 "Mac_でpythonの環境構築")
========================================================

Mac にpythonをどうやってインストールしたらいいのか悩んでいませんか？

目次[](#目次 "目次")
--------------

*   [目次](#目次)
*   [独立したpython の環境構築](#独立したpython_の環境構築)
*   [homebrew](#homebrew)
*   [pyenv](#pyenv)
*   [pyenv + virtualenv で環境構築](#pyenv_+_virtualenv_で環境構築)
*   [Mac でpythonの環境構築まとめ](#Mac_でpythonの環境構築まとめ)

独立したpython の環境構築[](#独立したpython_の環境構築 "独立したpython_の環境構築")
--------------------------------------------------------

python の実行環境をプロジェクトごとに管理する必要がある場合に以下の手順を行います。

利点としては、

1.  システムの環境を汚さないこと
2.  他人と合同で開発を進めるときに共通の環境を作成しやすいこと
3.  ディレクトリごとに環境が自動で変更されること

があげられます。

前提として多少のITスキル(コマンドライン、IPアドレスの設定など)が必要とされます。

それならばDockerを利用して環境構築を行う方が洗練されています。

そして、ITスキルが無いならば、Anacondaを利用する方が簡便です。

以上から、Dockerについて勉強する時間が無く、多少のコマンドラインは扱え、複数のプロジェクトに対応する必要がある人間を対象としています。

homebrew[](#homebrew "homebrew")
--------------------------------

以下のリンクに従ってhomebrewをセットアップします 。

[Homebrew](https://brew.sh/index_ja)

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"  

```

pyenv[](#pyenv "pyenv")
-----------------------

コマンドラインからpythonのバージョン管理をするために、homebrew でpyenvをinstallします。

```
brew install pyenv
```

pyenv + virtualenv で環境構築[](#pyenv_+_virtualenv_で環境構築 "pyenv_+_virtualenv_で環境構築")
--------------------------------------------------------------------------------

pyenv + virtualenv で名前を付けて、指定したバージョン(今回は3.6.3)のpythonをインストールします。

```
pyenv virtualenv 3.6.3 PROJECT-NAME 
```

指定のディレクトリで下記のコマンドを実行することで、特定のディレクトリ下で特定のpython環境を実行するようになります。

```
cd project-dir   
pyenv local PROJECT-NAME
```

Mac でpythonの環境構築まとめ[](#Mac_でpythonの環境構築まとめ "Mac_でpythonの環境構築まとめ")
-----------------------------------------------------------------

*   homebrew のセットアップ
*   pyenvのインストール
*   指定のディレクトリで指定のpython環境を設定

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); });