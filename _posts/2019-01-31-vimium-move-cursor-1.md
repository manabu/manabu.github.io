---
layout: post
title: VimiumのVisual Modeのカーソル移動について
description: VimiumのVisual Modeのカーソル移動について
date: 2019-01-31T23:07:02
categories: browser firefox chromium chrome
---

# Vimium

ブラウザもキーボードで操作できて、できれば、vimとかemacsっぽいバインドがいいなと思っていたところ、 `Vimium` というのがよいらしい。
実際に使っていて非常によかったが、Visual Modeの使い方をもう少しよくしたかったので調べた。

- Chrome
    - [Vimium - Chrome ウェブストア](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb)
- Firefox
    - [Vimium-FF – Get this Extension for 🦊 Firefox (ja)](https://addons.mozilla.org/ja/firefox/addon/vimium-ff/)

ビジュアルモードに入ったあと、終了位置は指定できるが、開始位置の変更方法がよくわからなかったがついにその方法がわかった

[Visual Mode · philc/vimium Wiki](https://github.com/philc/vimium/wiki/Visual-Mode)

1. <kbd>v</kbd> を押す
2. <kbd>c</kbd> を押す
3. vim みたいにカーソルを動かして、先頭を合わせる
4. <kbd>v</kbd> を押す

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B00HWLJI3U&linkId=a0132ee074721b379e4c971ae9952313"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B00OIDI7SW&linkId=c5969e996ddbff59a06b5f76e29f6d17"></iframe>
