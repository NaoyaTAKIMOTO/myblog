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


<a href="//ck.jp.ap.valuecommerce.com/servlet/referral?sid=3563352&pid=887689136" rel="nofollow"><img src="//ad.jp.ap.valuecommerce.com/servlet/gifbanner?sid=3563352&pid=887689136" height="1" width="1" border="0">BTOパソコンならパソコンショップSEVEN</a>
