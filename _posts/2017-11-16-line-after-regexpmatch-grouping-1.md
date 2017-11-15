---
layout: post
title: sedで、マッチした文字列を含めて次の行に追加したい
date: 2017-11-16T00:47:02
categories: sed
---

# sed で、マッチした文字列を含めて次の行に追加したい

chef や、ansibleにある特定の行の後ろに、ある行をいれるというのを

* [ある文字列をファイルの特定行に挿入するコマンド - 元RX-7乗りの適当な日々](http://d.hatena.ne.jp/rx7/20110310/p1)

このときにマッチした特定の部分を次の行にいれたい。

* [text processing - Insert newline before each line matching a pattern unless the previous line is already empty - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/323162/insert-newline-before-each-line-matching-a-pattern-unless-the-previous-line-is-a/323177#323177)

plagger の config で、qiitaのタグと同じものをslideshareからとってきたいときは、こんなかんじ

```
sed -zri  's!qiita.com/tags/([^/].*)/feed.atom!\0\n        - https://www.slideshare.net/rss/tag/\1!g' work.yaml
```


<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4797393106&linkId=2732a2b7370e7b3708dca2b0eab451b3"></iframe>
