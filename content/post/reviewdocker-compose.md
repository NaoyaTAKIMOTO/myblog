---
title: 'Re:VIEW+docker-composeでの手順'
date: 2020-12-24T14:33:00.007+09:00
draft: false
aliases: [ "/2020/12/reviewdocker-compose.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }docker composeとreview

docker composeとreview[](#docker_composeとreview "docker_composeとreview")
=======================================================================

Mac環境でのdocker-composeでRe:VIEWを扱う方法のメモ。

基本的には

[https://github.com/vvakame/docker-review/blob/master/doc/windows-review.md](https://github.com/vvakame/docker-review/blob/master/doc/windows-review.md)を辿ればいい。

目次

*   [作業ディレクトリの作成](#作業ディレクトリの作成)
*   [Dockerfileとdocker-compose.ymlの作成](#Dockerfileとdocker-compose.ymlの作成)
*   [作業ディレクトリでRe:VIEWの初期化](#作業ディレクトリでRe:VIEWの初期化)
*   [テキストの編集](#テキストの編集)
*   [PDFの作成](#PDFの作成)

作業ディレクトリの作成[](#作業ディレクトリの作成 "作業ディレクトリの作成")
-----------------------------------------

```
mkdir work
```

workは任意の名前に変更可能

Dockerfileとdocker-compose.ymlの作成[](#Dockerfileとdocker-compose.ymlの作成 "Dockerfileとdocker-compose.ymlの作成")
--------------------------------------------------------------------------------------------------------

下記のworkは作業ディレクトリの名前に合わせること。

Dockerfile

```
FROM vvakame/review
```

docker-compose.yml

```
  
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

作業ディレクトリでRe:VIEWの初期化[](#作業ディレクトリでRe:VIEWの初期化 "作業ディレクトリでRe:VIEWの初期化")
--------------------------------------------------------------------

```
cd work  
  
docker pull vvakame/review  
  
docker-compose run --rm review review-init sampledoc  
  
cp docker-compose.yml Dockerfile sampledoc  

```

sampledocは任意の名前に変更可能

テキストの編集[](#テキストの編集 "テキストの編集")
-----------------------------

.reファイルを編集する。

文法は [https://github.com/kmuto/review/blob/master/doc/format.ja.md](https://github.com/kmuto/review/blob/master/doc/format.ja.md) を参照する。

PDFの作成[](#PDFの作成 "PDFの作成")
--------------------------

sampledocディレクトリで下記のコマンドを実行する。

```
  
docker-compose run --rm review rake pdf  

```

成功すればbook.pdfが作成される。

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); });