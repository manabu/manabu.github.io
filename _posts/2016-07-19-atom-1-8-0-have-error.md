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
