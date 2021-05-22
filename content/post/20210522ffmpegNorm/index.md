---
title: "ffmpegで音声ファイルの音量の正規化(ノーマライゼーション)"
description: ""
date: "2021-05-22T17:41:25+09:00"
thumbnail: "/img/equalizer-153212_1280.png"
tags: [ffmpeg]
---

音量の正規化のためにffmpegを用いた。

後々のために記録しておく。
## コマンドの例
    ffmpeg -i input.mp3 -af loudnorm=I=-16:LRA=11:TP=-1.5 output.mp3

input.mp3, output.mp3
は適当な名前に変更すること。

拡張子はmp3以外でも構わない。

## 感想
まあ、音量としてはちょうどいい。

一般のストリーミングサービスの音量と同じくらいに調整できているんじゃかろうか？

ただ賢いノーマライズをしていないので、
ノイズも増幅される点には注意してほしい。

## 他の方法
音量の正規化のアプリは色々とあるだろうけれど、
コマンドで一発で変換したかったので今回はffmpegを利用することにした。

## 参考リンク
[(FFmpeg) How to normalize audio?](http://johnriselvato.com/ffmpeg-how-to-normalize-audio/)

