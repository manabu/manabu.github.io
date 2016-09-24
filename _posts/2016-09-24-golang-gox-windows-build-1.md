---
layout: post
title: spf13/cobraを使った後、goxでビルドしたときに、windows用のバイナリができなかった時の対処方法
date: 2016-09-24T23:51:02
categories: go
---

# spf13/cobraを使い始めてからwindowsのバイナリがない。。。

spf13/cobraを使い始めたら、windows用のバイナリが作成されなかった
werckerで、でていたエラーは次のようになっていた。

```
2 errors occurred:
--> windows/amd64 error: exit status 1
Stderr: ../../fsouza/go-dockerclient/client_windows.go:16:2: cannot find package "github.com/Microsoft/go-winio" in any of:
	/goroot/src/github.com/Microsoft/go-winio (from $GOROOT)
	/gopath/src/github.com/Microsoft/go-winio (from $GOPATH)
../../spf13/cobra/command_win.go:9:2: cannot find package "github.com/inconshreveable/mousetrap" in any of:
	/goroot/src/github.com/inconshreveable/mousetrap (from $GOROOT)
	/gopath/src/github.com/inconshreveable/mousetrap (from $GOPATH)

--> windows/386 error: exit status 1
Stderr: ../../fsouza/go-dockerclient/client_windows.go:16:2: cannot find package "github.com/Microsoft/go-winio" in any of:
	/goroot/src/github.com/Microsoft/go-winio (from $GOROOT)
	/gopath/src/github.com/Microsoft/go-winio (from $GOPATH)
../../spf13/cobra/command_win.go:9:2: cannot find package "github.com/inconshreveable/mousetrap" in any of:
	/goroot/src/github.com/inconshreveable/mousetrap (from $GOROOT)
	/gopath/src/github.com/inconshreveable/mousetrap (from $GOPATH)
```

`spf13/cobra/command_win.go:9:2` を検索したら

* [Cross-compilation fails without explicitly installing mousetrap · Issue #250 · spf13/cobra](https://github.com/spf13/cobra/issues/250)

このページがひっかかってきた。

最終的にwercker.ymlに以下を追加して解決

```
  go get github.com/inconshreveable/mousetrap
```

手元ではそれでよかったがwercker/goxでは、さらに次のものが必要だったようだ。
エラーにも確かに出ている

```
  go get -d github.com/Microsoft/go-winio
```

どうも、go-winioの問題らしい。

* [Fix building instructions · aaronlehmann/swarmkit@a7a8b7a](https://github.com/aaronlehmann/swarmkit/commit/a7a8b7a66346b440061eb1f79b6517e680c2662c)

上のものへのリンクは以下で発見

* [syscall.Overlapped Error while cloning swarmkit using go get · Issue #1067 · docker/swarmkit](https://github.com/docker/swarmkit/issues/1067)

# 参考図書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4621300253&linkId=54b7e05ab6406ca0d71627d0bd6794ab"></iframe>
