---
title: 'python でmlflow使うメモ'
date: 2020-07-18T16:24:00.000+09:00
draft: false
aliases: [ "/2020/07/python-mlflow.html" ]
tags : [技術系,python,devops,mlflow]
---

## python でmlflow使うメモ[](#python_でmlflow使うメモ "python_でmlflow使うメモ")


実験結果を比較するために便利っぽいので使ってみた。使う際の手順をメモしておく。

## mlflow のインストール[](#mlflow_のインストール "mlflow_のインストール")


```
pip install mlflow
```

## クイックスタート[](#クイックスタート "クイックスタート")


pythonで以下のような記述を用いる。

```python
with mlflow.start_run():  
   mlflow.log_param("a", 1)  
   mlflow.log_metric("b", 2)  
   mlflow.log_artifact("output.txt")
```

log\_paramにはパラメータを入れる。

log\_metricには損失関数や評価指標を入れる。valueには数値しか受け付けない。

log\_params({"example":hoge，“example2”：True})の方が便利。 同様にlog\_metricsもある。

log\_artifact でファイルを保存できる(csvやjsonなど)。metricの書式に当てはまらないものをこちらで保存する。

## 実験の種類ごとに枠を作る[](#実験の種類ごとに枠を作る "実験の種類ごとに枠を作る")


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

## 実験結果の比較[](#実験結果の比較 "実験結果の比較")


CLIでサーバーを立ち上げる。

```
mlflow ui
```

表示されたアドレスをブラウザで開く。

サーバーを落とす時はctrl＋c。

