---
layout: post
title: gox でクロスビルドするときに変数を埋め込む
date: 2016-09-24T23:21:01
categories: go
---

# gox でクロスビルドするときに変数を埋め込む


これを見る感じ、いけそうにおもった

* [Go+Webアプリケーション+CircleCIで静的解析・テスト・バイナリリリースを効率良く行なう - Qiita](http://qiita.com/kaneshin/items/163626c09c1ad9818c6c)


* [tcnksm/wercker-step-gox: Wercker step for mitchellh/gox, cross-compiling golang project parallelly](https://github.com/tcnksm/wercker-step-gox)

ldflagsも定義できそうだ

* [wercker-step-gox/wercker-step.yml at master · tcnksm/wercker-step-gox](https://github.com/tcnksm/wercker-step-gox/blob/master/wercker-step.yml)


* [Goでビルドバージョン情報を参照できるようにする(Go1.5) - Qiita](http://qiita.com/reiki4040/items/6b32370532c3eafe1f0e)
* [go - Golang application auto build versioning - Stack Overflow](http://stackoverflow.com/questions/11354518/golang-application-auto-build-versioning)

# うまくできなかった原因がわかった。

指定するときにパッケージの名前の前に、"github.com/..." みたいのをいれる必要があった

* [Setting Go(1.5) variables at compile time for Versioning – Medium](https://medium.com/@joshroppo/setting-go-1-5-variables-at-compile-time-for-versioning-5b30a965d33e#.33fgqyxpl)

## 失敗していた時

```
-X config.CommitID=$COMMITID
```

## 成功した時

```
-X github.com/manabu/dockerlayer/config.CommitID=$COMMITID
```

# さらなる失敗の可能性

var の中で定義する変数名を大文字にしておかないと、他のパッケージから参照できないようだ

* [Go言語：エクスポートされる名前 - sugilogのブログ](http://sugilog.hatenablog.com/entry/2014/12/28/163339)

このあたりは、golintなどで名前が解決できないと指摘してくれる

# 参考図書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4621300253&linkId=54b7e05ab6406ca0d71627d0bd6794ab"></iframe>
