---
title: '文書分類問題を解くモデルを提供するNeuralClassifier の使い方メモ'
date: 2020-06-15T02:11:00.007+09:00
draft: false
aliases: [ "/2020/06/neuralclassifier.html" ]
tags : [技術系]
---

  

[![](https://1.bp.blogspot.com/-YlMb8v77MN4/XurdQSzS1yI/AAAAAAAAg6Y/oSZrJ0c9yxYbzQnNNTynRvZnEp-xGE7NwCK4BGAsYHg/s320/AFE90C8A-A49C-4475-9F05-50E2D56D5B63.jpeg)](https://1.bp.blogspot.com/-YlMb8v77MN4/XurdQSzS1yI/AAAAAAAAg6Y/oSZrJ0c9yxYbzQnNNTynRvZnEp-xGE7NwCK4BGAsYHg/s1920/AFE90C8A-A49C-4475-9F05-50E2D56D5B63.jpeg)

NeuralClassifier: An Open-source Neural Hierarchical Multi-label Text Classification Toolkit はTencentが公開しているマルチラベルな文書分類問題用のpythonライブラリです。  

詳しくは

  

> #### [Tencent/NeuralNLP-NeuralClassifier](https://github.com/Tencent/NeuralNLP-NeuralClassifier)
> 
> NeuralClassifier is designed for quick implementation of neural models for hierarchical multi-label classification task, which is more challenging and common in real-world scenarios. A salient feature is that NeuralClassifier currently provides a variety of text encoders, such as FastText, TextCNN, TextRNN, RCNN, VDCNN, DPCNN, DRNN, AttentiveConvNet and Transformer encoder, etc.

を参照しましょう。

さて、以下ではこのライブラリの使い方を開設します。

#### 目次

1.  環境設定
2.  実行方法
3.  conf/train.json の設定
4.  入力データの形式

環境設定
----

pytorch に依存しているライブラリなので、あらかじめ以下のコマンドでinstallしておきます。

```
pip install torch
```

また、作業用のディレクトリにレポジトリをcloneします。今回はzipをダウンロードして用いました。

実行方法
----

コマンドラインから.pyファイルをそれぞれ実行することで、学習、評価、予測を行います。

```
python train.py conf/train.json
```

conf/train.json に実行時の設定が記述されています。必要に応じて変更します。

```
python eval.py conf/train.json
```

で学習済みのモデルを評価できます。

各ラベルに対してprecision、 recall 、f value をまとめたものと混合行列を、それぞれ.txt形式で出力します。

conf/train.json の設定
-------------------

各種モデルのハイパーパラメータや学習、評価時に利用されるモデルの選択について記述されています。  

主に必要なのは、cpuかgpuの指定、入力データの情報、学習と評価に用いるモデルの選択に関しての記述になります。

  

num＿workerで警告が出たので0に変更すると解消した。

入力データは指定の形式を守って作成し、パスを指定します。

モデルの指定は学習用のモデルの指定と評価用のモデルの指定が独立して別に存在するので、注意すること。

入力データの形式
--------

```
JSON example:  
  
{  
   "doc_label": ["Computer--MachineLearning--DeepLearning", "Neuro--ComputationalNeuro"],  
   "doc_token": ["I", "love", "deep", "learning"],  
   "doc_keyword": ["deep learning"],  
   "doc_topic": ["AI", "Machine learning"]  
}  
{  
   "doc_label": ["Computer--MachineLearning--DeepLearning"],  
   "doc_token": ["I", "love", "deep", "learning"],  
   "doc_keyword": ["deep learning"],  
   "doc_topic": ["AI", "Machine learning"]  
}
```

この形式で作成すること！

厳密にはjsonの形式を守ってはいないので、pythonでデータを作成する際にはdictデータをjsonで出力する方法は取れません。諦めて、ファイルに一行ずつ書き込むのがよいです。

またこの例ではマルチラベルの例を示しているが、シングルラベルの場合にも要素数が1のリスト形式とすることに注意しましょう。私はそこでハマりました。

**文書分類問題の応用について**
-----------------

  

> #### [文書分類問題の応用はなにがある？](https://www.subcul-science.com/2020/06/blog-post_54.html)
> 
> 機械学習について勉強したけど、その使い道が分からん！ってなってないですか？ …

(function(b,c,f,g,a,d,e){b.MoshimoAffiliateObject=a; b\[a\]=b\[a\]||function(){arguments.currentScript=c.currentScript ||c.scripts\[c.scripts.length-2\];(b\[a\].q=b\[a\].q||\[\]).push(arguments)}; c.getElementById(a)||(d=c.createElement(f),d.src=g, d.id=a,e=c.getElementsByTagName("body")\[0\],e.appendChild(d))}) (window,document,"script","//dn.msmstatic.com/site/cardlink/bundle.js","msmaflink"); msmaflink({"n":"自然言語処理の基本と技術","b":"","t":"","d":"https:\\/\\/m.media-amazon.com","c\_p":"","p":\["\\/images\\/I\\/51V9d2v9Z9L.jpg"\],"u":{"u":"https:\\/\\/www.amazon.co.jp\\/dp\\/B01CGAPLLO","t":"amazon","r\_v":""},"aid":{"amazon":"2220302","rakuten":"2220301","yahoo":"2220303"},"eid":"Vza6T","s":"s"});

リンク