---
layout: post
title: コメントスタイルと、見た目と
date: 2016-07-13T01:21:01
---

* [Linus Torvaldsが許せないコメントスタイルとは？ | スラド デベロッパー](http://developers.srad.jp/story/16/07/12/056244/)

このページを見て（読んで）、正直なところ(b)と(no)が区別がつかなかった。
文が途中でわかれてるとかそういうことなのかとおもっているのだが
「ight alignment of the asterisks」くだりと、あわないし、

I'm sure that looks really nice if you
are out of your mind on LSD, and have nothing better to do than to
worry about the right alignment of the asterisks.

そのときの画面がこれ

(b)
![(b)](/images/comment-b.png)


(no)
![(no)](/images/comment-no.png)

どうしてもよくわからなかったので、ソースをみた


(b)のソース
![(b)のソース](/images/source-comment-b.png)


(no)のソース
![(no)のソース](/images/source-comment-no.png)

おそらく、空白の数でずれている部分のことなんだろうなぁと思うのだが、、、

ブラウザで等幅フォントの設定とか正しくがんばろうってさいきんおもわなくなったなぁ、、、

見えているものは見えているものであるということを勝手に再確認しました。
