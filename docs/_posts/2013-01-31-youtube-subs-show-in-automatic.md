---
author: aki
title: "YouTubeの字幕をデフォルトで表示する"
slug: youtube-subs-show-in-automatic
id: 6737
date: '2013-01-31 03:06:40'
layout: post
categories:
  - TIPS
tags:
  - cc_load_policy
  - YouTube
---

YouTubeの字幕機能，使ってますか？結構便利です．

まずは字幕です．仕事上，多言語字幕などを必要とするのですが，

universalsubtitles.org → ※このサイトはその後 amara になっています

というサイトで既存のYouTube動画に字幕をつけることが多いです．

[https://www.amara.org/](https://amara.org/ja/)

.srtファイルを使って各国言語の字幕を作ります．

で，せっかく作った字幕ですから，みんなに見て欲しいわけです．
しかしYouTubeの字幕機能は，よくよく見ないとわからないところにボタンがあります．

ユーザの設定で字幕をデフォルトでONにしていればいいのですが，それも期待できない場合．
このようなリンクを作れば，自動で字幕が付加されます．試してみてください．

[https://www.youtube.com/watch?v=mTwEhZMapLw&cc_load_policy=1&fs=1&rel=0&autoplay=1&loop=1](https://www.youtube.com/watch?v=mTwEhZMapLw&cc_load_policy=1&fs=1&rel=0&autoplay=1&loop=1) 

www.youtube.com に /v/ として 動画のIDを加えます．

その後ろにお好みの設定を入れればいいわけです．

以下私のお好み設定．

★youtube.GoogleAPIS.ComへのURLはwww.youtube.comを指定した場合にも自動で行われるようです．

*   cc_load_policy=1 字幕をデフォルトでONにする
*   rel=0　再生終了時の関連動画を表示しない
*   autoplay=1 読み込み終了時，自動で動画を再生します．
*   loop=1 再生終了時にループします．

これは埋め込みプレイヤーの設定なので，詳しくは[こちら](https://developers.google.com/youtube/player_parameters?hl=ja#cc_load_policy)を読んでいただければもっといろんな機能があることがわかります．

## 追記：2020-08-13

かつて GoogleAPIS だったのですが、現在は YouTube として動きますのでURLを変更しました。

