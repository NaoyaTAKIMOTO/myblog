---
title: "Mac bash zsh移行 メモ"
description: ""
date: "2021-02-08T20:54:54+09:00"
thumbnail: ""
tags: [mac,bash,zsh]
---

## 手順
1. 環境変数などの移行

    cat .bash_profile >> .zprofile

1. bashからzshへの切り替え

    chsh -s /bin/zsh