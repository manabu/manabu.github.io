---
layout: post
title: git add -p と git checkout -p について
date: 2016-09-15T21:31:00
---

# git add -p と git checkout -p について

いくつか同時に変更してしまったとき
コミットをそれぞれの事柄に分けたいとしたら、
add について

```
git add -p
```

を使うとよいということであった。

ただ、いくつかについては
もとにもどしたいんだよなぁとおもっていたら、以下のコメントを発見。

* [横着で神経質な私とあなたに贈るgit add -p - Qiita](http://qiita.com/crifff/items/1abf08bca4ce51db4775#comment-21e0707afe141d343ff5)

```
git checkout -p
```

便利であった。

add と checkout と両方同時に判定していけるコマンドはあるのだろうか。
あると便利なような気がするのだが。
