---
title: "poetry環境でstreamlitを実行する方法"
description: ""
date: "2022-02-24T16:01:29+09:00"
thumbnail: ""
tags: [python,poetry,streamlit]
---
## 症状
- streamlitをpoetryを使ってインストールした場合に、streamlitが実行できない
- ```poetry add streamlit```でstreamlitを追加した場合、通常のシェルからはstreamlitのパスが通っていない
- ```which streamlit```の実行結果でなにもでてこない 

## 対処
- poetry からシェルを実行する
- ```poetry shell```
- ```streamlit run sample.py```
- streamlitコマンドが実行できるようになる
- 仮想環境にstreamlitをインストールした場合には通常のシェルからはstreamlitを実行できない
- その場合の対処法は公式サイトに載っている


## 参考リンク
- [streamlit 公式サイト](https://streamlit.io/)
- [poetry 公式サイト](https://python-poetry.org/)


<a href="//af.moshimo.com/af/c/click?a_id=2274112&p_id=1386&pc_id=2364&pl_id=48429&guid=ON" rel="nofollow" referrerpolicy="no-referrer-when-downgrade"><img src="//image.moshimo.com/af-img/0598/000000048429.png" width="640" height="640" style="border:none;"></a><img src="//i.moshimo.com/af/i/impression?a_id=2274112&p_id=1386&pc_id=2364&pl_id=48429" width="1" height="1" style="border:none;">