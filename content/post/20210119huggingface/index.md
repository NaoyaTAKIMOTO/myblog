---
title: "hugging face でBART(文章要約モデル)を使ってみた"
description: ""
date: "2021-01-19T03:03:11+09:00"
thumbnail: ""
tags: [技術系,自然言語処理,python,技術,分散表現,文生成]
---

- BARTは文書要約のためのモデル
- BERTと同じtransformerの派生
- BERTとは異なり、encoder-decoderの構造
    - これは文生成を目的とするため

このページではBARTのチュートリアルを実行する手順を示す。

## 手順
1. transformersのインストール

```sh
pip install transformers
```
2. 要約の実行

```py
from transformers import BartTokenizer, BartForConditionalGeneration, BartConfig

model = BartForConditionalGeneration.from_pretrained('facebook/bart-large')
tokenizer = BartTokenizer.from_pretrained('facebook/bart-large')

ARTICLE_TO_SUMMARIZE = "My friends are cool but they eat too many carbs."
inputs = tokenizer([ARTICLE_TO_SUMMARIZE], max_length=1024, return_tensors='pt')

# Generate Summary
summary_ids = model.generate(inputs['input_ids'], num_beams=4, max_length=5, early_stopping=True)
print([tokenizer.decode(g, skip_special_tokens=True, clean_up_tokenization_spaces=False) for g in summary_ids])
```

2021/01/18ではMyMy friendsと出力された。

面白い。

## ハマったところ
pytorchのバージョンがtransformersの指定と異なるとエラーが出た。
```
pip install -U torch
```
でpytorchをアップデートして解決した。

## コツ
max_lengthが単語列の長さ、num_beamsがビームサーチの幅を指定する。

max_lengthが生成される文の長さを調整する。

長い文を生成する場合にはより幅の広い探索をしないと局所解に陥って不自然な文が出力された。

二つのパラメータは計算時間とのトレードオフなので小さいものから試していくのがいい。

## 参考リンク
- [transformers 公式ドキュメント](https://huggingface.co/transformers/model_doc/bart.html)

## 分散表現の仕組みについて学ぶ

単語の意味を学習する分散表現について、
実際にプログラムを実行しながら仕組みを理解しませんか？

分散表現の学習のイメージをつかめるとBERT系で何をどのように学習しているのかについても理解が深まります。

詳しくは以下のリンク
> ### [Googlecolaboratory と pythonで学ぶ初めての 自然言語処理入門](https://subcul-science.booth.pm/items/1562211)
> 本ドキュメントを利用することで自然言語処理における分散表現の仕組みが理解でき、読者が新しい自然言語処理のサービスを開発する助けになる。

## 最後に
不明点などあればコメントお願いします！

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=subculturesci-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B084WPRT44&linkId=7f1720c9cca99ccf6b5daeb1270354fa"></iframe>