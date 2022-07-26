---
title: "pycharmからpoetryで環境の作成ができない"
description: ""
date: "2022-02-24T11:56:49+09:00"
thumbnail: ""
tags: [環境構築,python,poetry]
---
## 症状
pycharmでinterpreterの指定にエラーが出た。
改めてpoetryの環境構築を行おうとしたところ、以下のエラーが出た。
```py
ModuleNotFoundError No module named 'virtualenv.activation.xonsh' at <frozen importlib._bootstrap>:984 in _find_and_load_unlocked
```
## 解決方法
```
pip3 uninstall virtualenv
```

## 原因
- anyenvのアップデートをかけたのが悪かったか？

## 反省
- 不用意なアップデートは不具合の原因になる

<a href="//af.moshimo.com/af/c/click?a_id=2274112&p_id=1386&pc_id=2364&pl_id=48429&guid=ON" rel="nofollow" referrerpolicy="no-referrer-when-downgrade"><img src="//image.moshimo.com/af-img/0598/000000048429.png" width="640" height="640" style="border:none;"></a><img src="//i.moshimo.com/af/i/impression?a_id=2274112&p_id=1386&pc_id=2364&pl_id=48429" width="1" height="1" style="border:none;">