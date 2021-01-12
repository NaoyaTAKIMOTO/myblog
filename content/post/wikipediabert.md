---
title: '日本語Wikipediaで学習したBERTが公開されたので使い方のメモ'
date: 2020-06-17T07:34:00.013+09:00
draft: false
aliases: [ "/2020/06/wikipediabert.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }日本語Wikipediaで学習したBERTが公開されたので使い方のメモ

日本語Wikipediaで学習したBERTが公開されたので使い方のメモ[](#日本語Wikipediaで学習したBERTが公開されたので使い方のメモ "日本語Wikipediaで学習したBERTが公開されたので使い方のメモ")
=================================================================================================================

*   [前準備:mecabのインストール](#前準備:mecabのインストール)
*   [transformersのインストール](#transformersのインストール)
*   [BERT の利用方法については下記の例を参考にします。](#BERT_の利用方法については下記の例を参考にします。)
*   [応用範囲](#応用範囲)

huggingface がBERTの日本語モデルを公開しました。

日本語モデルはtransformersに含まれています。

しかし、Mac 環境で実際に動かすまでにいくつか躓いたので、メモを残しておきます。

前準備:mecabのインストール[](#前準備:mecabのインストール "前準備:mecabのインストール")
--------------------------------------------------------

形態素解析エンジンであるmecabが BERT の日本語モデルを利用する際に必要になります。おそらくトークナイザがmecabを要求する仕組みになっています。

以下のサイトを参考にmecabをインストールします。

MecabをPythonで使うまで - QiitaMecabとは 形態素解析エンジンです。 形態素解析については他の方の記事がすごくわかりやすいので割愛します。 なお qiita.com

homebrew を利用して、Mecab とipadicをインストールします。

```
brew install mecab mecab-ipadic
```

辞書を更新するために、適当な辞書用のディレクトリを作成し、以下のコマンドを実行します。

```
git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git  
./bin/install-mecab-ipadic-neologd -n -a
```

python のmecabラッパーをインストールします。

```
pip install mecab-python3
```

transformersのインストール[](#transformersのインストール "transformersのインストール")
-----------------------------------------------------------------

[huggingface/transformers](https://github.com/huggingface/transformers)

公式のドキュメントに従ってtransformersをインストールします。

```
pip install transformers
```

BERT の利用方法については下記の例を参考にします。[](#BERT_の利用方法については下記の例を参考にします。 "BERT_の利用方法については下記の例を参考にします。")
-----------------------------------------------------------------------------------------

[clｰtohoku](https://github.com/cl-tohoku/bert-japanese)

```
import torch  
from transformers.tokenization_bert_japanese import BertJapaneseTokenizer  
from transformers.modeling_bert import BertForMaskedLM  
tokenizer = BertJapaneseTokenizer.from_pretrained('bert-base-japanese-whole-word-masking
```

bert-base-japanese-whole-word-maskingは学習時に用いたトークナイズの方法(単語区切りか文字区切り)を指定しています。

```
model = BertForMaskedLM.from_pretrained('bert-base-japanese-whole-word-masking')
```

タスクに対応したBERTモデルを読み込みます。

今回はMLM(Masked Language Model )となります。マスクトークンが存在する位置に入る単語の確率を返します。

```
input_ids = tokenizer.encode(f'''  
   青葉山で{tokenizer.mask_token}の研究をしています。  
''', return_tensors='pt')
```

トークナイザを利用して、トークンを対応する辞書番号に変換します。

```
print(input_ids)  
print(tokenizer.convert_ids_to_tokens(input_ids[0].tolist()))
```

id番号を対応する辞書のトークンに置き換えます。

```
masked_index = torch.where(input_ids == tokenizer.mask_token_id)[1].tolist()[0]  
print(masked_index)  
result = model(input_ids)  
pred_ids = result[0][:, masked_index].topk(5).indices.tolist()[0]  
for pred_id in pred_ids:  
   output_ids = input_ids.tolist()[0]  
   output_ids[masked_index] = pred_id  
   print(tokenizer.decode(output_ids))
```

マスクトークンが入っている位置に入る確率が高いトークンをk=5個表示します。

BERT のモデルを指定することで、単語の確率だけでなく、分散表現も計算できます。

応用範囲[](#応用範囲 "応用範囲")
--------------------

単語の分散表現の応用範囲は以下のリンク

[文書分類問題の応用は何がある？](https://www.subcul-science.com/2020/06/blog-post_54.html)

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); }); 参考資料 機械学習・深層学習による自然言語処理入門　scikit-learnとTensorFlowを使った実践プログラミング

[](//af.moshimo.com/af/c/click?a_id=2220302&p_id=170&pc_id=185&pl_id=4062&s_v=b5Rz2P0601xu&url=https%3A%2F%2Fwww.amazon.co.jp%2Fexec%2Fobidos%2FASIN%2F4839966605)![](//i.moshimo.com/af/i/impression?a_id=2220302&p_id=170&pc_id=185&pl_id=4062)

[](//af.moshimo.com/af/c/click?a_id=2220302&p_id=170&pc_id=185&pl_id=4062&s_v=b5Rz2P0601xu&url=https%3A%2F%2Fwww.amazon.co.jp%2Fexec%2Fobidos%2FASIN%2F4839966605)![](//i.moshimo.com/af/i/impression?a_id=2220302&p_id=170&pc_id=185&pl_id=4062)

posted with [ヨメレバ](https://yomereba.com)

[Amazonで購入](//af.moshimo.com/af/c/click?a_id=2220302&p_id=170&pc_id=185&pl_id=4062&s_v=b5Rz2P0601xu&url=https%3A%2F%2Fwww.amazon.co.jp%2Fexec%2Fobidos%2FASIN%2F4839966605)![](//i.moshimo.com/af/i/impression?a_id=2220302&p_id=170&pc_id=185&pl_id=4062)

[Kindleで購入](//af.moshimo.com/af/c/click?a_id=2220302&p_id=170&pc_id=185&pl_id=4062&s_v=b5Rz2P0601xu&url=https%3A%2F%2Fwww.amazon.co.jp%2Fgp%2Fsearch%3Fkeywords%3D%26__mk_ja_JP%3D%2583J%2583%255E%2583J%2583i%26url%3Dnode%253D2275256051)![](//i.moshimo.com/af/i/impression?a_id=2220302&p_id=170&pc_id=185&pl_id=4062)

[楽天ブックスで購入](//af.moshimo.com/af/c/click?a_id=2220301&p_id=56&pc_id=56&pl_id=637&s_v=b5Rz2P0601xu&url=http%3A%2F%2Fbooks.rakuten.co.jp%2Frb%2F16190713%2F)![](//i.moshimo.com/af/i/impression?a_id=2220302&p_id=170&pc_id=185&pl_id=4062)

[楽天koboで購入](//af.moshimo.com/af/c/click?a_id=2220301&p_id=56&pc_id=56&pl_id=637&s_v=b5Rz2P0601xu&url=https%3A%2F%2Fbooks.rakuten.co.jp%2Frk%2F350e869d324d356eb91b3b52d00d0e36%2F)![](//i.moshimo.com/af/i/impression?a_id=2220301&p_id=56&pc_id=56&pl_id=637)

[7netで購入](//af.moshimo.com/af/c/click?a_id=2317554&p_id=932&pc_id=1188&pl_id=12456&s_v=b5Rz2P0601xu&url=http%3A%2F%2F7net.omni7.jp%2Fsearch%2F%3FsearchKeywordFlg%3D1%26keyword%3D9784839966607)