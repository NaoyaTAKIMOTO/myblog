---
title: 'Google Apps Scriptで後輩系line bot 作ったった'
date: 2020-06-25T03:55:00.003+09:00
draft: false
aliases: [ "/2020/06/line-bot.html" ]
tags : [技術系]
---

     .markdown-body { box-sizing: border-box; min-width: 200px; max-width: 980px; margin: 0 auto; padding: 45px; } .markdown-body pre { background: #23241f; } .markdown-body strong, .markdown-body h1, .markdown-body h2, .markdown-body h3, .markdown-body h4, .markdown-body h5 { font-weight: 700; } @media (max-width: 767px) { .markdown-body { padding: 15px; } }Google Apps Scriptで後輩系line bot 作ったった

Google Apps Scriptで後輩系line bot 作ったった　[](#Google_Apps_Scriptで後輩系line_bot_作ったった_ "Google_Apps_Scriptで後輩系line_bot_作ったった_")
=======================================================================================================================

そういえばLINE botを個人開発したことがありました！

目次

*   [動機](#動機)
*   [botの概要](#botの概要)
*   [サンプルコード](#サンプルコード)
*   [結果](#結果)

動機[](#動機 "動機")
--------------

当時、仲間内でDTMが流行りまして、作った曲を共有するためにGoogleドライブを利用してました。

ですが、こっそりアップするシャイなメンバーが多かったので、曲のアップを見逃すことが多かったんですね。

そこでGoogleドライブの共有フォルダに更新があったら教えてくれるヤツあったら見落としが減っていいだろうな、という動機でbot作成に着手しました。

あれは完全に自分に需要があるという理由で作ったけど、よく作れたなと思います。

botの概要[](#botの概要 "botの概要")
--------------------------

定期的に共有フォルダの更新をチェックして、更新があればそのファイルのリンクをLINEグループに投稿してくれるものです。

LINE botはGASを使ってサーバーレスの仕様にしたので、今でも動いています。

たまに共有フォルダにファイルをアップすると通知してくれます。

ファイル名とリンクと曲をアップしたことへのねぎらいの一言があって、個人的にはbotというよりはキャラクターなんですよね。

当時FGOにハマっていたので後輩系のキャラなんです。

サンプルコード[](#サンプルコード "サンプルコード")
-----------------------------

Googleドライブとラインの設定は以下のリンクを参考にしました。

*   [Google Apps ScriptでLINE BOTつくったら30分で動かせた件](https://qiita.com/hakshu/items/55c2584cf82718f47464)
    
*   [【ソースコード付き】GoogleDriveでファイルが追加・更新されたらメールで通知する](https://boomin.yokohama/archives/797)
    

上記のリンクを参考に下記のコードの穴埋めをすることでline botを実装できます。

下記の部分で変数の設定を行います。

*   bangdore\_FOLDER\_ID
    
    Googleドライブの更新をチェックしたいディレクトリのID。
    

*   SEND\_MAIL\_ADDRESS
    
    更新通知を送りたいメールアドレス。
    
*   access\_token
    
    line developersのアクセストークン
    

```
var bangdore_FOLDER_ID = 'google drive directoy id';  
var SEND_MAIL_ADDRESS = ['eｰmail＠dot.com'];  
var ADD_FILE_COUNT = 0;  
var ADD_FOLDER_COUNT = 0;  
var lastUpdateMap = {};  
var lastUpdate = 0  
var updateFileList = [];  
var updateFileLinkList = [];  
var day_ago_unix_time = 0  
  
//Time is processed by minute  
var msecPerMinute = 1000 * 60;  
var SEARCH_TIME = 100;  
  
var access_token = "hogehoge";  

```

スクリプトの起動を通知するためにメールを送る関数。別になくても動きます。

```
function sendMail(){  
  SEND_MAIL_ADDRESS.forEach(function(o,i) {  
    MailApp.sendEmail(SEND_MAIL_ADDRESS[i],"バンドリチェッカー起動通知", "run bandre checker"  
                     );  
  })  
}
```

lineにメッセージを送るための関数。

```
function sendHttpPost(message){  
  var token = [access_token];  
  Logger.log('token '+token);  
  var options =  
      {  
        "method"  : "POST",  
        "payload" : "message=" + message,  
        "headers" : {"Authorization" : "Bearer "+ token}  
  
  };  
UrlFetchApp.fetch("https://notify-api.line.me/api/notify",options);  
}  

```

Googleドライブのフォルダ内のファイルを全てサーチして、更新時間を取得する部分。

もっとエレガントな実装があるとは思うので、あくまで参考程度に。

```
function stackFiles(file){  
  updateFileList.push(file.getName());  
  updateFileLinkList.push(file.getUrl());  
  lastUpdate = createdTime;  
  ADD_FILE_COUNT++;  
}  
  
function DeepFolder(bangdoreFolder){  
  Logger.log('deep folder')  
  var deepFolder = bangdoreFolder.getFolders();  
  while (deepFolder.hasNext()){  
    var folder = deepFolder.next()  
    Logger.log("folder names are "+folder.getName())  
    DeepFolder(folder);  
    var files = folder.getFiles();  
  
    while (files.hasNext()) {  
      var file = files.next();  
      createdTime = Utilities.formatDate( file.getLastUpdated(), 'Asia/Tokyo', 'yyyyMMddHHmm');  
      if(day_ago_unix_time < createdTime){  
        stackFiles(file)  
      }  
    }  
    ADD_FOLDER_COUNT++;  
  }  
}
```

botがランダムで挨拶をしてくれる部分。

ここを変えるとキャラ付けが変わる。

今回は心配性な後輩キャラ。マ○ュにインスパイアされました。

```
function greeting(){  
  var results=["一緒にがんばりましょうね","無理は禁物ですよ","お茶でも飲みませんか？","私はちゃんと分かってますから","食事はきちんと取りましょうね","頑張ってますね","いい加減にしましょうね？"];  
  var greet = results[Math.floor(Math.random()*results.length)]  
  Logger.log(greet);  
  return greet;  
}
```

実際のメイン関数。

更新されたファイルのリンクをメッセージとしてlineに投稿します。

```
function main() {  
  //sendMail()  
  var dateobj = new Date();  
  var now_unix_time =  Utilities.formatDate(dateobj, 'Asia/Tokyo', 'yyyyMMddHHmm');  
  Logger.log("now_unix_time"+now_unix_time)  
  //How to show the time SEARCH_TIME minutes before from now....?  
  day_ago_unix_time = now_unix_time - SEARCH_TIME;  
  
  var bangdoreFolder = DriveApp.getFolderById(bangdore_FOLDER_ID);  
  var files = bangdoreFolder.getFiles();    
  
  while (files.hasNext()) {  
    var file = files.next();  
    createdTime = Utilities.formatDate( file.getLastUpdated(), 'Asia/Tokyo', 'yyyyMMddHHmm');  
    if(day_ago_unix_time < createdTime){  
      stackFiles(file)  
    }      
  }  
  
  DeepFolder(bangdoreFolder);  
  Logger.log("day_ago_unix_time "+day_ago_unix_time);  
  var min_update_time = 0;  
  
  if(lastUpdate > day_ago_unix_time) {  
    Logger.log("There are renewed files ")  
    SEND_MAIL_ADDRESS.forEach(function(o,i) {  
      MailApp.sendEmail(SEND_MAIL_ADDRESS[i],"更新通知",  
                        "譜面が" + ADD_FILE_COUNT + "枚更新されたよ！" + "\n\n" +  
                        "URLはこちら↓" + "\n" +  
                        "https://drive.google.com/open?id=" + bangdore_FOLDER_ID + "\n\n" +  
                        "更新された譜面のリンク\n"+  
                        updateFileList.join("\n")  
      );  
    })  
  
    var message = "更新ですよ、先輩\n\n";  
    Logger.log("renewed "+updateFileList);  
    for(var i=0; i<updateFileList.length; i++){  
      var name = updateFileList[i];  
      var link = updateFileLinkList[i];  
      Logger.log("renew file "+name);  
      message = message + name + "\n";  
      message = message + link + "\n\n";  
    };  
    message = message + "以上です\n";  
    message = message + greeting();  
    Logger.log(message)  
    sendHttpPost(message);  
  }  
  else{  
    Logger.log("There are no renewed files ");  
  }  
  Logger.log("The number of renewed files "+ADD_FILE_COUNT);  
  Logger.log("The number of renewed folders "+ADD_FOLDER_COUNT);  
}  

```

結果[](#結果 "結果")
--------------

結局はメンバーの熱が冷めて、活躍の場面も無くなっていきました。メンバーのエンゲージメントを保つのは難しいですね。

グループでメンバーが活動しやすいように、作曲に対してリアクションがあると嬉しいんじゃないかな！という想いを込めてLINE bot にねぎらいの一言を添えるようにしました。

だけど、それはメンバーのモチベーションには繋がらなかったようです。

botを可愛がってもらえるようにするには各メンバーの好みを把握するのは次回に活かします。

hljs.initHighlightingOnLoad(); $(document).on("mouseover", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").text("🔗").show(); }); $(document).on("mouseout", "h1,h2,h3,h4,h5", function(e) { $(e.currentTarget).find(".fa-link").hide(); });