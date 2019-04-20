---
layout: post
title: アクションカメラで撮った複数の動画ファイルを結合する
description: アクションカメラで撮った複数の動画ファイルを結合する
date: 2019-04-19T22:07:02
categories: linux debian nvidia
---

# 格安のアクションカメラの映像をつなげてみたい

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B07J2MKCXS&linkId=d22004b61de46832ccd9e92649ad12b6"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B06XSV23T1&linkId=d69db185b7e3a6131ef1ed9e925b9964"></iframe>

この APEMAN A66S を買ってみて、問題なく録画ができるし、タブレットでは問題なく再生できたし、フォーマットを変更して、PS4のメディアプレーヤーでもみれるようになった。

複数のファイルにわかれているので、これを結合したうえで、フォーマットを変換したい。

参考:
[アクションカメラの映像がPS4のメディアプレーヤーで音声がでないとき対処方法1](../convert-movie-format/)


# 複数の動画ファイルをまとめて、結合し１つのファイルにする

## 方法１

```
ffmpeg -i "concat:input1.mp4|input2.mp4" -brand mp42 mp42_out.mp4
```

## 方法2

ファイルに書き出しておく

ファイルの中身は

```
file file1.mp4
file file2.mp4
```

```
ffmpeg -f concat -i files1.txt  -brand mp42 concat_all_from_file_out2.mp4
```

絶対パスの場合はファイルの中身は、絶対パスにするだけでよい


```
file /home/hogehoge/hoge1.mp4
file /home/hogehoge/hoge2.mp4
```

ただし、絶対パスのときは実行のコマンドに `-safe 0` が必要らしい。ないとうまくいかなかった。

```
ffmpeg -safe 0  -f concat -i files1.txt  -brand mp42 concat_all_from_file_out2.mp4
```

# 参考
- [Slideshow – FFmpeg](https://trac.ffmpeg.org/wiki/Slideshow)
  - ファイルの中身の書式
- [\[ffmpeg\]複数の動画ファイルを連結する - Qiita](https://qiita.com/suzutsuki0220/items/a60ac53592f48edf32a1)


# GoPro 6

APEMAN A66Sもかなりよかったので、GoProだとどんなものなのかも知りたいという気持ちもある。

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B07K373BXZ&linkId=92145c08856520202ae0539e865c9441"></iframe>
