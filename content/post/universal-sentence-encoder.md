---
title: 'Universal Sentence Encoder の使い方メモ'
date: 2020-06-22T18:29:00.006+09:00
draft: false
aliases: [ "/2020/06/universal-sentence-encoder.html" ]
tags : [技術系]
---

Universal Sentence Encoder を使って文書のベクトルが得られる。

#### 目次

1.  特徴
2.  使い道
3.  使い方

### 特徴

多言語に対応している。

日本語にも対応している。

  

日本語の文章をベクトルで扱える

### 使い道

クラスタリング、類似度の計算、特徴量の抽出

### 使い方

準備として以下のコマンドを実行する。

```
pip install tensorflow tensorflow_hub numpy tf_sentencepiece   

```

学習済みのモデルが公開されている。

具体的な利用方法は以下のpythonの記述を参照

```
import tensorflow_hub as hub  
import numpy as np  
# for avoiding error  
import ssl  
ssl._create_default_https_context = ssl._create_unverified_context  
  

``````
import ssl  
ssl._create_default_https_context = ssl._create_unverified_context  
def cos_sim(v1, v2):  
   return np.dot(v1, v2) / (np.linalg.norm(v1) * np.linalg.norm(v2))  
  
embed = hub.load("https://tfhub.dev/google/universal-sentence-encoder-multilingual/3")  
  
texts = ["昨日、お笑い番組を見た。", "昨夜、テレビで漫才をやっていた。", "昨日、公園に行った。", "I saw a comedy show last night.", "Yesterday, I went to the park."]  
vectors = embed(texts)  
  
print(texts[0], texts[1], cos_sim(vectors[0], vectors[1]), sep="\t")  
print(texts[0], texts[2], cos_sim(vectors[0], vectors[2]), sep="\t")  
print(texts[0], texts[3], cos_sim(vectors[0], vectors[3]), sep="\t")  
print(texts[0], texts[4], cos_sim(vectors[0], vectors[4]), sep="\t"
```

詳細は以下のリンクを参照

[Universal Sentence Encoderを日本語で試す - QiitaUniversal Sentence Encoderとは その名の通り、文をエンコード、すなわち文をベクトル化する手qiita.com](https://qiita.com/kenta1984/items/9613da23766a2578a27a)[](https://qiita.com/kenta1984/items/9613da23766a2578a27a)

得られた分散表現の利用方法は以下を参照

> #### [文書分類問題の応用はなにがある？](https://www.subcul-science.com/2020/06/blog-post_54.html)
> 
> 機械学習について勉強したけど、その使い道が分からん！ってなってないですか？

(function(b,c,f,g,a,d,e){b.MoshimoAffiliateObject=a; b\[a\]=b\[a\]||function(){arguments.currentScript=c.currentScript ||c.scripts\[c.scripts.length-2\];(b\[a\].q=b\[a\].q||\[\]).push(arguments)}; c.getElementById(a)||(d=c.createElement(f),d.src=g, d.id=a,e=c.getElementsByTagName("body")\[0\],e.appendChild(d))}) (window,document,"script","//dn.msmstatic.com/site/cardlink/bundle.js","msmaflink"); msmaflink({"n":"自然言語処理の基本と技術","b":"","t":"","d":"https:\\/\\/m.media-amazon.com","c\_p":"","p":\["\\/images\\/I\\/51V9d2v9Z9L.jpg"\],"u":{"u":"https:\\/\\/www.amazon.co.jp\\/dp\\/B01CGAPLLO","t":"amazon","r\_v":""},"aid":{"amazon":"2220302","rakuten":"2220301","yahoo":"2220303"},"eid":"Vza6T","s":"s"});

リンク