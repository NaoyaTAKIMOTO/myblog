---
title: "日本語の分散表現の計算方法まとめ"
description: ""
date: "2022-03-02T20:59:30+09:00"
thumbnail: ""
tags: [自然言語処理, T5,BERT,Sentece Transformers,SBERT,word2vec,fasttext]
---

## 単語単位の分散表現
- [Word2vec]({{<ref "/post/20200615google-colaboratory-word2vec/index.md">}})
  - 自然言語処理における分散表現の一つのオリジナル
  - 基本原理くらいは知っていてもいいかもしれない
- [Fasttext で文書分類問題までやったった]({{<ref "/post/20200613fasttext.md">}})
  - fastと名前がついているだけあってfacebookが公開しているモデルは高速に動作する
  - 分散表現とクラス分類に対応していたり、利便性が高い
  - 特にこのモデルで利用されている分かち書きの特徴から未知語に強いとされている
- [日本語Wikipediaで学習済みのBERTが公開されているので使い方メモ]({{<ref "/post/wikipediabert.md">}})
  - Google の検索エンジンにも採用されている、らしい
  - 自然言語処理の研究を大きく変えたモデル
  - 関連する技術であるTransformerは自然言語処理だけでなく、画像処理の界隈にも流用された
  - huggingfaceで日本語版のBERTも色々と公開されている
- [日本語に対応したT5]({{<ref "/post/20210701T5/index.md">}})
  - この日本語版のモデルの作者が公開しているサンプルがわかりやすい
  - また同じ作者がSBERTのモデルも公開している

## 文単位の分散表現
- [Universal Sentence Encoder]({{<ref "/post/universal-sentence-encoder.md">}})
  - 結構重宝する
  - そこそこ性能もよく使い勝手がいい
- [SBERT]({{<ref "/post/20210203SBERT.md">}})
  - GPUがないとしんどいかも
  - 性能自体は上のUSEよりも体感ではいい
