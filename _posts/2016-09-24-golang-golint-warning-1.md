---
layout: post
title: golint の comment の warning
date: 2016-09-24T01:21:01
categories: go
---

# golint のWarning

次のようなコードを書いてみた。

```go
package config

var (
	VersionString = "not set version string" // VersionString
)
```

atomでは次のようなWarningがでた

```
config/config.go:4:2:warning: exported var VersionString should have comment or be unexported (golint)
```

次のようにするとWarningは消えた。

```go
package config

// Variables for commands
var (
	VersionString = "not set version string" // VersionString
)
```

# golint と gometalinter

atomでのメッセージをみたら、[gometalinter](https://github.com/alecthomas/gometalinter) というのが見えた。
どうも、まとめて色々なツールをかけてくれるものらしい。

* [gometalinter で楽々 lint - Qiita](http://qiita.com/spiegel-im-spiegel/items/238f6f0ee27bdf1de2a0)


# 参考図書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4621300253&linkId=54b7e05ab6406ca0d71627d0bd6794ab"></iframe>
