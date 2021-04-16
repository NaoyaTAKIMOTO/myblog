---
title: 'Universal Sentence Encoder の使い方メモ'
date: 2020-06-22T18:29:00.006+09:00
draft: false
aliases: [ "/2020/06/universal-sentence-encoder.html" ]
tags : [技術系,自然言語処理,universal sentence encoder,技術,python,分散表現]
---

Universal Sentence Encoder を使って文書のベクトルが得られる。

## 特徴

多言語に対応している。

日本語にも対応している。

日本語の文章をベクトルで扱える

## 使い道

クラスタリング、類似度の計算、特徴量の抽出

## 使い方

準備として以下のコマンドを実行する。

```sh
pip install tensorflow tensorflow_hub numpy tf_sentencepiece   
```

学習済みのモデルが公開されている。

具体的な利用方法は以下のpythonの記述を参照

```py
import tensorflow_hub as hub  
import numpy as np  
# for avoiding error  
import ssl  
ssl._create_default_https_context = ssl._create_unverified_context  

def cos_sim(v1, v2):  
   return np.dot(v1, v2) / (np.linalg.norm(v1) * np.linalg.norm(v2))  
  
embed = hub.load("https://tfhub.dev/google/universal-sentence-encoder-multilingual/3")  
  
texts = ["昨日、お笑い番組を見た。", "昨夜、テレビで漫才をやっていた。", "昨日、公園に行った。", "I saw a comedy show last night.", "Yesterday, I went to the park."]  
vectors = embed(texts)  
```

より詳細は以下のリンクを参照

[Universal Sentence Encoderを日本語で試す](https://qiita.com/kenta1984/items/9613da23766a2578a27a)

得られた分散表現の利用方法は以下を参照

> #### [文書分類問題の応用はなにがある？]({{<ref "post/20200618blog-post_54.md" >}})
> 
> 機械学習について勉強したけど、その使い道が分からん！ってなってないですか？
