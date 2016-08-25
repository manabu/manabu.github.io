---
layout: post
title: Goを始めてみた。werckerでビルドしてみる。
date: 2016-08-23T11:21:01
---

# やりたいこと

goで書いたプログラムをビルドして、それをgithubに配置してみたい。
しかし、最初からそこまでいけるかわからないので、まずは getting started 的なサンプルを動かしてみる。

# 結論

* [wercker - getting started - Getting started with wercker &amp; Go](http://devcenter.wercker.com/quickstarts/building/golang.html)

これに従えば良い。

## プログラムの内容

サーバーをたてて、特定のURLにアクセスすると、結果が返ってくるものであった

## werckerにlogin

githubとか選べる。

## 対象にする、レポジトリを選択

作ったサンプルを選ぶ。

## 完成

publicにして作成してみた

## wercker.yml

サンプルにあるやつを使った。

# わざと間違えてみる

写経したのでタイプミスがあった。
そこをきちんとチェックしてくれていた。

もしcloneした場合は、わざと、ミスタイプして、pushすると何がおこるのかチェックするとよいのではないかと思う。


# 参考書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4621300253&linkId=54b7e05ab6406ca0d71627d0bd6794ab"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4048707876&linkId=ea12fe19844a2dac292c771e40a7368b"></iframe>
