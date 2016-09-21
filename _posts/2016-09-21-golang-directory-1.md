---
layout: post
title: go の開発環境を整える。ディレクトリ
date: 2016-09-21T21:21:01
---

# カレントディレクトリってどうするんだ？

さいしょ、適当なディレクトリで、作り始めたが
どうもパッケージの読み込みがうまくいかない。

```
import "./cmd"
```

みたいに書いてみたけど、多分これ違うかなぁと。。。

# そもそも

```
$GOPATH/src
```

に作るのかな。

# 公開したプロジェクトであれば

```go get``` すればよいのかな


# 参考

* [そろそろ真面目に Golang 開発環境について考える — GOPATH 汚染問題 - Qiita](http://qiita.com/spiegel-im-spiegel/items/73ebc684b5807277b7e2)

* [Go言語のDependency/Vendoringの問題と今後．gbあるいはGo1.5 | SOTA](http://deeeet.com/writing/2015/06/26/golang-dependency-vendoring/)

# 参考図書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4621300253&linkId=54b7e05ab6406ca0d71627d0bd6794ab"></iframe>
