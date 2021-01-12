---
title: 'Re:VIEW の始め方メモ'
date: 2020-07-16T20:46:00.002+09:00
draft: false
aliases: [ "/2020/07/review.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }Re:VIEW の始め方メモ

Re:VIEW の始め方メモ[](#Re:VIEW_の始め方メモ "Re:VIEW_の始め方メモ")
==================================================

mac でのRe：VIEW を導入した時のメモ。

目次

*   [作業用ディレクトリの作成](#作業用ディレクトリの作成)
*   [Docker を用意](#Docker_を用意)
*   [Dockerfileとdocker-compose.ymlの作成](#Dockerfileとdocker-compose.ymlの作成)
*   [文章の編集](#文章の編集)
*   [文章ファイルの作成](#文章ファイルの作成)
*   [参考文献](#参考文献)

作業用ディレクトリの作成[](#作業用ディレクトリの作成 "作業用ディレクトリの作成")
============================================

適当なディレクトリをつくる。

```
mkdir “project_name”
```

Docker を用意[](#Docker_を用意 "Docker_を用意")
======================================

Docker のインストールは各自でされたし。

[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

詳しくはググるといい。

Dockerfileとdocker-compose.ymlの作成[](#Dockerfileとdocker-compose.ymlの作成 "Dockerfileとdocker-compose.ymlの作成")
========================================================================================================

作業用ディレクトリに以下の二つのファイルを作成する。

```
Dockerfile  
  
FROM vvakame/review
``````
docker-compose.yml  
  
version: '3'  
services:  
 review:  
   volumes:  
     - .:/work  
   build: .  
   working_dir: /work  
   ports:  
     - "127.0.0.1:18000:18000"
```

以下のコマンドで雛形の作成を行う。

```
docker-compose run --rm review review-init "project_name"
```

作成されたディレクトリにDockerfile とdocker-compose.ymlをコピーする。

```
cp Dockerfile docker-compose.yml "project_name"
```

文章の編集[](#文章の編集 "文章の編集")
=======================

実際の文書は"project\_name".reを編集する。

エディターはなんでもいいけども、今回はVS code を用いた。

Visual Studio Code は.reに対応したプラグインがある。

.reの詳しい書式は公式サイトをみる。

扉の編集の仕方はまだ分からん。

文章ファイルの作成[](#文章ファイルの作成 "文章ファイルの作成")
===================================

作成されたプロジェクトディレクトリでdocker-composeを実行する。

rakeのあとにpdfでpdfが作れる。同様にしてEPUBも作れる。

```
cd "project_name"  
docker-compose run --rm review rake pdf
```

あとは文章の中身を作っていく。

参考文献[](#参考文献 "参考文献")
====================

詳しくは以下のリンクを参照する。

面倒くさい場合に本記事を読む。

*   [WindowsでDocker+Re:VIEWを使う](https://github.com/vvakame/docker-review/blob/master/doc/windows-review.md)
    
*   [Re:VIEWクイックスタートガイド](https://github.com/kmuto/review/blob/master/doc/quickstart.ja.md)
    

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); });