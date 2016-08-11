---
layout: post
title: Goを始めてみた。atomで。
date: 2016-07-31T11:21:01
---

# Goをはじめてみた。atomで。

# Go のインストール

* [The Go Programming Language](https://golang.org/)

ここを見ると golang 1.6 が、最新の安定版(2016-08-11現在)のようなので、
それをインストールした。

# GOPATH の設定

atom側で設定できるかと思ったが、どうも推奨されていなようだった。

どうも、つぎの場所につくるのが、デフォルト？のようなので、まずはそれに従ってみる。

```
mkdir ~/go
```

~/.bashrc とか ~/.zshrc

に以下のものを追記しておく。

```
export GOPATH=/home/manabu/go
export PATH=$PATH:$GOPATH/bin
```

たぶん、ここで一度この環境変数が使えるようにしておいたほうが良い。

# atom に入れたもの

* [go-plus](https://atom.io/packages/go-plus)

いろいろいれてくれる。

ツールなどもおとしてくれるが、これが ***~/go*** 以下に入るようだ。

## GOPATHの設定。atomで、できるのか？

go-plusをいれると、次のものもいれてくれて、その中でも設定できそうなのだが、

* [go-config](https://atom.io/packages/go-config)

設定画面をみると以下のように書いてあった。

```
Not recommended for use
```

まぁ、atom以外からも使うだろうし、わすれなさそうとおもって、~/.bashrc とか ~/.zshrc に書くことにした。

# 参考書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4621300253&linkId=54b7e05ab6406ca0d71627d0bd6794ab"></iframe>
