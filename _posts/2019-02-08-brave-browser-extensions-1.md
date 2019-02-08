---
layout: post
title: Debian 10 に、brave browser を入れる。
description: Debian 10 に、brave browser を入れる。
date: 2019-02-08T22:07:02
categories: browser brave chromium
---

# debian にbrave 0.59.x をインストールする

0.26系はもはやサポートされなくなったようなので、新しいのをいれたかったのだが
debian用の適切な方法を公式ページではうまく見つけられなかった。

その後いろいろ調べt見たところ、


[Installing Brave — Brave Browser documentation](https://brave-browser.readthedocs.io/en/latest/installing-brave.html#linux)

基本的には、ここに書いてあるようにすればよいが、

aptのアドレスだけ以下のように書き換える。
以下のように `stretch` と記述してあげると、インストールができた


```
deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stretch main
```

あとは

```
apt-get update
apt-get install brave-browser brave-keyring
```

こんなかんじだろうか。
必要があれば、古いやつを消す

```
apt-get remove brave
```


