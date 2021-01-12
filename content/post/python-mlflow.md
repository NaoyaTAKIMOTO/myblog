---
title: 'python でmlflow使うメモ'
date: 2020-07-18T16:24:00.000+09:00
draft: false
aliases: [ "/2020/07/python-mlflow.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }python でmlflow使うメモ

python でmlflow使うメモ[](#python_でmlflow使うメモ "python_でmlflow使うメモ")
==============================================================

実験結果を比較するために便利っぽいので使ってみた。使う際の手順をメモしておく。

目次

*   [mlflow のインストール](#mlflow_のインストール)
*   [クイックスタート](#クイックスタート)
*   [実験の種類ごとに枠を作る](#実験の種類ごとに枠を作る)
*   [実験結果の比較](#実験結果の比較)
*   [今回のはまりどころ](#今回のはまりどころ)

mlflow のインストール[](#mlflow_のインストール "mlflow_のインストール")
--------------------------------------------------

```
pip install mlflow
```

クイックスタート[](#クイックスタート "クイックスタート")
--------------------------------

pythonで以下のような記述を用いる。

```
with mlflow.start_run():  
   mlflow.log_param("a", 1)  
   mlflow.log_metric("b", 2)  
   mlflow.log_artifact("output.txt")
```

log\_paramにはパラメータを入れる。

log\_metricには損失関数や評価指標を入れる。valueには数値しか受け付けない。

log\_params({"example":hoge，“example2”：True})の方が便利。 同様にlog\_metricsもある。

log\_artifact でファイルを保存できる(csvやjsonなど)。metricの書式に当てはまらないものをこちらで保存する。

実験の種類ごとに枠を作る[](#実験の種類ごとに枠を作る "実験の種類ごとに枠を作る")
--------------------------------------------

CLI で以下を実行してexperimentを作成する。

```
mlflow experiments create --experiment-name fraud-detection
```

CLI でexperimentが作成されたことを確認。

experiment \_idをメモしておく。

```
mlflow experiments list  

```

以下のようにpythonで記述して、experimentを指定する。

```
mlflow.set_experiment('experiment_name')  
  
with mlflow.start_run():  
   mlflow.log_param("a", 1)  
   mlflow.log_metric("b", 2)  
   mlflow.log_artifact("output.txt")  

```

実験結果の比較[](#実験結果の比較 "実験結果の比較")
-----------------------------

CLIでサーバーを立ち上げる。

```
mlflow ui
```

表示されたアドレスをブラウザで開く。

サーバーを落とす時はkillする。(あんまりスマートじゃないなぁ？)

今回のはまりどころ[](#今回のはまりどころ "今回のはまりどころ")
-----------------------------------

experiment を新しく作成して、 新たにサーバーを立ち上げようとするときにエラーが出るときは、 既にサーバーが立ち上がってるのかも。

kill して対応した。

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); });