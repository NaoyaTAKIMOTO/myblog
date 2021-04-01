---
title: 'Google colaboratory を使ってWord2Vec の仕組みからモデルの学習まで'
date: 2020-06-15T02:13:00.006+09:00
draft: false
aliases: [ "/2020/06/google-colaboratory-word2vec.html" ]
tags : [技術系,技術]
---

   
## Google colaboratory を使ってWord2Vec の仕組みからモデルの学習まで[](#Google_colaboratory_を使ってWord2Vec_の仕組みからモデルの学習まで "Google_colaboratory_を使ってWord2Vec_の仕組みからモデルの学習まで")


## Word2Vec から始めよう[](#Word2Vec_から始めよう "Word2Vec_から始めよう")


word2vec はラベル無しの文章から単語の意味ベクトルを学習することが出来るモデルです。

単語のベクトルを扱うことで、単語の類似度の計算やクラスタリングといった応用が可能になります。そしてその技術の延長であるBERTはGoogleの検索サービスにも用いられています。

## 概念の理解が難しい[](#概念の理解が難しい "概念の理解が難しい")


しかし、皆さんはword2vec について勉強しようとして、苦戦していませんか？なかなかその概念を理解することは、馴染みが無いものですから、難しいです。

word2vec について解説している資料はすでにあります。しかし、図解だけでは仕組みを理解して扱うレベルに至るのは難しいでしょう。そして実際に動くプログラムで記述されると、解説のコメントがあっても、その一行が何をしているのか飲み込みづらいものです。

## Google Colaboratory を使おう[](#Google_Colaboratory_を使おう "Google_Colaboratory_を使おう")


そこで一行単位でプログラムを実行できるGoogle Colaboratoryを利用することをおすすめします。

Google Colaboratory を使うメリットとして、

Gmail のアカウントを取得していれば無料であること、

一行単位で実行できること、

word2vec以外の機械学習にも応用が効くことが挙げられます。

実際に多くの方がGoogle Colaboratory を利用して機械学習の学習や実験に取り組んでいます。

アルゴリズムの仕組みを理解するには実際に手を動かしてみるのが一番です。

私も実際にword2vecを動かして遊びながら、理解を深めていきました。

そこで皆さんの学習の助けとなるように、Google Colaboratoryのプログラムと解説を用意しました。

以下のリンクからどうぞ。

[https://subcul-science.booth.pm/items/1562211](https://subcul-science.booth.pm/items/1562211)
