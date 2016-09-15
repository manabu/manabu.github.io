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

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=477416366X&linkId=5817eb126b7d58c0431f6c4cccb5c21f"></iframe>
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4873115655&linkId=04d63439348b40230efbf2f08d634c58"></iframe>
<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=477415654X&linkId=aadf10a67a87f3aa6002a14c23177163"></iframe>
