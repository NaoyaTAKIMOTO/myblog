---
title: 'Fasttext で文書分類問題までやったった'
date: 2020-06-13T07:29:00.016+09:00
draft: false
aliases: [ "/2020/06/fasttext.html" ]
tags : [技術系]
---
Fasttext で文書分類問題までやったった



## Fasttext で文書分類問題までやったったのまとめ[](#Fasttext_で文書分類問題までやったったのまとめ "Fasttext_で文書分類問題までやったったのまとめ")

*   Facebook research がFasttextを使った文書分類ライブラリを公開してる
*   Fasttext のpython 環境でのinstall 方法は簡単
*   実行時間は早い
    
## 前振り[](#前振り "前振り")

    

文書分類のタスクに取り組むことになり、当初は、

> NeuralClassifier: An Open-source Neural Hierarchical Multi-label Text Classification Toolkit

を使っていました。ですが、あまり精度が出ませんでした。

上司に教えてもらったのが、

> \[2\] A. Joulin, E. Grave, P. Bojanowski, T. Mikolov, Bag of Tricks for Efficient Text Classification

でした。

## Fasttext ライブラリの特徴[](#Fasttext_ライブラリの特徴 "Fasttext_ライブラリの特徴")


これはFasttextを用いて文書分類問題をend-to-endで解いてくれるライブラリになります。

そのため、文書ベクトルを分類タスク様に最適化できる仕様になっています。

学習にかかる時間も数秒以内と非常に速く、たたき台としては有効です。

また、性能も悪くありません。[ハイパーパラメータチューニング](https://fasttext.cc/docs/en/autotune.html)もできます。

基本は上記の通りです。

固定したいパラメータ(分散表現の次元数など)だけ指定し以下のように実行します。

```
model = fasttext.train_supervised(input='cooking.train', autotuneValidationFile='cooking.valid')
```

ここで'cooking.train'と 'cooking.valid'は指定の形式のテキストファイルとなります。

## Fasttext ライブラリの使い方[](#Fasttext_ライブラリの使い方 "Fasttext_ライブラリの使い方")


```
pip install fasttext
```

上のコマンドだけで、2020年6月時点ではpython用のfastText環境が整います。 非常に簡単です。

## 文書分類問題での使い方[](#文書分類問題での使い方 "文書分類問題での使い方")


教師データとして'data.train.txt'を作成する必要があります。

データの形式は"**label**"とトークナイズされた文書を各行に持つテキストファイルです。

```
train.txt   
  
__label__1  愛 が 重 い  
__label__2  愛 し て ます
```

同様にして教師データと同じ形式でテストデータ等を作成します。

モデルの訓練は以下のコードを実行します。

```
import fasttext  
  
model = fasttext.train_supervised('train.txt')
```

学習時間は教師データの量に依存するが、CPUで対応可能であり、手元のデータ(約1000件)では数秒で学習が終了しました。

学習したモデルを用いた推定結果は以下のようにして得られます。

```
model.predict("あなた は 愛 を 信じ ます か ？")
```

この時、分類されるクラスと予測確率の配列が返されます。

以上によって、fastTextを用いた文書分類問題が解かれます。

評価

sklearnを用いて混合行列や精度比較が出来ます。

以下はscikit-learnの公式サイトからの引用です。

```
from sklearn.metrics import confusion_matrix  
  
y_true = ["cat", "ant", "cat", "cat", "ant", "bird"]  
y_pred = ["ant", "ant", "cat", "cat", "ant", "cat"]  
confusion_matrix(y_true, y_pred, labels=["ant", "bird", "cat"])  
array([[2, 0, 0],  
      [0, 0, 1],  
      [1, 0, 2]])
```
```
from sklearn.metrics import classification_report  
y_true = [0, 1, 2, 2, 2]  
y_pred = [0, 0, 2, 2, 1]  
target_names = ['class 0', 'class 1', 'class 2']  
print(classification_report(y_true, y_pred, target_names=target_names))  
             precision    recall  f1-score   support  
<BLANKLINE>  
    class 0       0.50      1.00      0.67         1  
    class 1       0.00      0.00      0.00         1  
    class 2       1.00      0.67      0.80         3  
<BLANKLINE>  
   accuracy                           0.60         5  
  macro avg       0.50      0.56      0.49         5  
weighted avg       0.70      0.60
```

## まとめ[](#まとめ "まとめ")


fastText とscikit-learnを利用することで、

python 環境下で、

簡単に文書分類問題に取り組むことが出来ます。

python はデータセット作成時にも便利なので、ひとまず文書分類を試したいという場合には有効な選択肢の一つです。

実応用については下記のリンクを参考にしてください。

[文書分類問題の応用はなにがある？](https://www.subcul-science.com/2020/06/blog-post_54.html)

参考資料 
機械学習・深層学習による自然言語処理入門　scikit-learnとTensorFlowを使った実践プログラミング
- [amazon](https://amzn.to/3igk8Mh)
- [楽天](https://hb.afl.rakuten.co.jp/ichiba/1b0a2d31.d22da597.1b0a2d32.91386760/?pc=https%3A%2F%2Fitem.rakuten.co.jp%2Fbook%2F16190713%2F&link_type=hybrid_url&ut=eyJwYWdlIjoiaXRlbSIsInR5cGUiOiJoeWJyaWRfdXJsIiwic2l6ZSI6IjI0MHgyNDAiLCJuYW0iOjEsIm5hbXAiOiJyaWdodCIsImNvbSI6MSwiY29tcCI6ImRvd24iLCJwcmljZSI6MSwiYm9yIjoxLCJjb2wiOjEsImJidG4iOjEsInByb2QiOjAsImFtcCI6ZmFsc2V9)
