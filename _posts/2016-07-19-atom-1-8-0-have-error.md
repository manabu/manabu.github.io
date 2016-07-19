---
layout: post
title: Atom 1.8.0 にしたらエラーがでた。その解決策。
date: 2016-07-19T01:21:01
---

# atom のバージョンをあげたら、エラーがでた

```
onDidChangeStatus
```

こんなエラーがでた。
エラーのなかに、issueへのリンクがあったのでクリック。

* [Crashes in Atom v1.7.0-beta: Cannot read property 'onDidChangeStatus' of undefined · Issue #20 · andischerer/atom-svn](https://github.com/andischerer/atom-svn/issues/20)

中を読むと

* [Linux installation packages on atom.io are broken · Issue #12182 · atom/atom](https://github.com/atom/atom/issues/12182)

このリンクにあるように、

1. 一旦uninstall
2. 新しいパッケージをとってくる
3. 再度インストール手順にしたがっていれる。

とやってみたが、うまくいかなかった。

# 解決策

よくよくRoot Causeを読んでみたら、
* [Atom](https://atom.io/)
これだとだめらしく

* [Release 1.8.0 · atom/atom](https://github.com/atom/atom/releases/tag/v1.8.0)

こちらから落とせとのことであった。

実際におとしてみたら、問題なくエラーがなくなりました。

# 参考

atom 1.8.0 のパッケージだが、落とす場所によって、md5がちがっていた。


|どこからおとしてきたか|MD5|
| - | - |
|atom.io から落としたもの|d8379f317727e67ddfa1ca3ea1427dc0|
|github から落としたもの|e9899377a519db25a630a5dad8a8ca4f|




<iframe src="http://rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=ss_til&asins=4774182702" style="width:120px;height:240px;" scrolling="no" marginwidth="0" marginheight="0" frameborder="0"></iframe>
