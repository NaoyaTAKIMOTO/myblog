---
title: 'vue.jsでtodoリスト作成'
date: 2020-10-13T02:03:00.000+09:00
draft: false
aliases: [ "/2020/10/vuejstodo.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }vue.jsでtodoリスト作成

目次

\[TOC\] #　vue.jsでtodoリスト作成

開発環境[](#開発環境 "開発環境")
--------------------

macOS

firebase cli　のインストール[](#firebase_cli_のインストール "firebase_cli_のインストール")
--------------------------------------------------------------------

```
npm install -g firebase-tools
```

多分yarn add でも可

todo list の作成[](#todo_list_の作成 "todo_list_の作成")
-----------------------------------------------

vueとjavascriptについてはまだあんまり理解していない。

firebase でローカルでテスト[](#firebase_でローカルでテスト "firebase_でローカルでテスト")
--------------------------------------------------------------

```
firebase init  
firebase login  
firebase serve --only hosting
```

表示されたリンクをブラウザで開いてチェックする。

firebase でデプロイ[](#firebase_でデプロイ "firebase_でデプロイ")
--------------------------------------------------

```
firebase deploy
```

表示されたリンクにアクセスして、挙動を確認する。

[HabitsMaker](https://daily-task-e6c33.web.app)

todo実装[](#todo実装 "todo実装")
--------------------------

1.  ログインの実装

ログイン状態の保存がよくわからん。ログインページを挿入するといいのか？

[https://github.com/firebase/firebaseui-web](https://github.com/firebase/firebaseui-web)

ログインまではできるけど、リダイレクトした後にログアウトする？？

2.  ログインユーザー毎に専用のtodo リストが表示されるようにする

これはuse.uidで区別するような記述をすればできそう。

3.  ページのルーティング
    
4.  vueの書き方をもうちょい調べる
    

参考資料

*   [https://qiita.com/potato4d/items/cfddeb8732fec63cb29c#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E5%88%9D%E6%9C%9F%E5%8C%96](https://qiita.com/potato4d/items/cfddeb8732fec63cb29c#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E5%88%9D%E6%9C%9F%E5%8C%96)
*   [https://cr-vue.mio3io.com/tutorials/todo.html#%E5%AE%8C%E6%88%90%E5%BD%A2](https://cr-vue.mio3io.com/tutorials/todo.html#%E5%AE%8C%E6%88%90%E5%BD%A2)
*   [https://jp.vuejs.org/v2/examples/todomvc.html](https://jp.vuejs.org/v2/examples/todomvc.html)

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); });