---
title: '文書分類問題の応用'
date: 2020-06-18T06:42:00.008+09:00
draft: false
aliases: [ "/2020/06/blog-post_54.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }文書分類問題の応用

文書分類問題の応用[](#文書分類問題の応用 "文書分類問題の応用")
===================================

機械学習について勉強したけど、その使い道が分からん！ってなってないですか？

勉強するときに強く意識してないと見落としがちですが、どうやって使うんだろう、とアンテナを常日頃から張らないと使い道が分からなくなります。

使われてこその道具ですから、新しく手に入れた道具だての使い道をメモしておきます。

*   [文書分類問題の適用範囲](#文書分類問題の適用範囲)
*   [文書分類問題とは](#文書分類問題とは)
    *   [教師有り](#教師有り)
    *   [教師無し](#教師無し)
    *   [特徴量](#特徴量)
*   [実際の利用例](#実際の利用例)

文書分類問題の適用範囲[](#文書分類問題の適用範囲 "文書分類問題の適用範囲")
-----------------------------------------

自然言語処理の文書分類について勉強をしたなら以下のことが出来るようになっています。

*   スパムメール検出
*   ニュースのトピック分類
*   重要箇所抽出
*   文書要約
*   ユーザーへのレコメンド
*   クラスタリング
*   感情分析など

意外と活用の範囲は広そうですね？

文書分類問題とは[](#文書分類問題とは "文書分類問題とは")
--------------------------------

一つの文書に対して、一つ以上のラベルを付けることです。機械学習ではラベルを予測するモデルを作ります。

ここで文書は短いものは単語、長いものはニュース記事までと、あまり長さは関係ありません。

ラベルとしては、重要かどうか(バイナリ)、トピック、感情(マルチクラス、マルチラベル)などを付けます。

教師有りの手法と教師無しの手法があります。

### 教師有り[](#教師有り "教師有り")

教師有りの場合はラベルを人間が用意する必要があります。

クラウドソーシングを利用したアノテーション作業を行ったり、SNSのタグやECサイトのレビューなどを収集したりします。

この場合、自力では十分な量のデータを用意できないこともままあります。そのため、機械学習の手法は有効でしょう。

### 教師無し[](#教師無し "教師無し")

教師無しは文書のデータだけがあればいいのでデータの準備が楽です。

ウィキペディアのデータを流用することなどが挙げられます。

### 特徴量[](#特徴量 "特徴量")

文書から特徴量を抽出する必要があります。

特徴量はTF-IDFや分散表現が用いられます。

最近の研究(2020年時点)では深層学習がおもなトピックです。

得られた特徴量を元に、教師有りの場合は、SVMなどの機械学習の手法を用いて分類することができます。

実際の利用例[](#実際の利用例 "実際の利用例")
--------------------------

実際の利用方法は以下のリンクにメモしています。

[Universal Sentence Encoder の使い方メモ](https://www.subcul-science.com/2020/06/universal-sentence-encoder.html)

[日本語Wikipediaで学習したBERTが公開されたので使い方のメモ](https://www.subcul-science.com/2020/06/wikipediabert.html)

[Google colaboratory を使ってWord2Vecの仕組みからモデルの学習まで](https://www.subcul-science.com/2020/06/google-colaboratory-word2vec.html)

[Fasttext で文書分類問題までやったった](https://www.subcul-science.com/2020/06/fasttext.html)

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); }); (function(b,c,f,g,a,d,e){b.MoshimoAffiliateObject=a; b\[a\]=b\[a\]||function(){arguments.currentScript=c.currentScript ||c.scripts\[c.scripts.length-2\];(b\[a\].q=b\[a\].q||\[\]).push(arguments)}; c.getElementById(a)||(d=c.createElement(f),d.src=g, d.id=a,e=c.getElementsByTagName("body")\[0\],e.appendChild(d))}) (window,document,"script","//dn.msmstatic.com/site/cardlink/bundle.js","msmaflink"); msmaflink({"n":"自然言語処理の基本と技術","b":"","t":"","d":"https:\\/\\/m.media-amazon.com","c\_p":"","p":\["\\/images\\/I\\/51V9d2v9Z9L.jpg"\],"u":{"u":"https:\\/\\/www.amazon.co.jp\\/dp\\/B01CGAPLLO","t":"amazon","r\_v":""},"aid":{"amazon":"2220302","rakuten":"2220301","yahoo":"2220303"},"eid":"Vza6T","s":"s"});

リンク