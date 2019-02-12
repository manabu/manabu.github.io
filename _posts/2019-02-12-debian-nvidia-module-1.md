---
layout: post
title: ある日 X が立ち上がらなくなったとき、nvidiaのカードを使っているときの対処方法1
description: ある日 X が立ち上がらなくなったとき、nvidiaのカードを使っているときの対処方法1
date: 2019-02-12T22:07:02
categories: linux debian nvidia
---

nvidiaのカードを使っていると、ドライバーが古いものに対応していなくて、
X が立ち上がらないことがある。
その場合は `nvidia-detect` を実行し、指示に従うとうまく動くことがある。

出力例

```
Your card is only supported up to the 390 legacy drivers series.
It is recommended to install the
    nvidia-legacy-390xx-driver
package.
```

インストール

```
apt-get install nvidia-legacy-390xx-driver
```


ある一定年数を超えるとサポートがおわるのだろう。
最近なら、オンボードのもので、十分なのかもしれない。

# 参考

NVIDIA GeForce RTX 2080Ti 

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B07GJYS2WM&linkId=03e45945a66956216ec4b5534271770c"></iframe>
