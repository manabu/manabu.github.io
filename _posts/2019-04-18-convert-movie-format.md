---
layout: post
title: アクションカメラの映像がPS4のメディアプレーヤーで音声がでないとき対処方法1
description: アクションカメラの映像がPS4のメディアプレーヤーで音声がでないとき対処方法1
date: 2019-04-18T22:07:02
categories: linux ffmpeg apeman actioncamera
---

# 格安のアクションカメラを買ってみた

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B07J2MKCXS&linkId=d22004b61de46832ccd9e92649ad12b6"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B06XSV23T1&linkId=d69db185b7e3a6131ef1ed9e925b9964"></iframe>

この APEMAN A66S を買ってみて、問題なく録画ができるし、タブレットでは問題なく再生できていた。
ただ、PS4のメディアプレーヤーでは、動画はみれるのだが、音声が再生できなかったので、変換してみたところ、問題なく音声も聞こえた。


参考:
[アクションカメラで撮った複数の動画ファイルを結合する](../concat-movies/)


# PS4のメディアプレーヤーで再生できるフォーマットへ変換する

とりあえず、以下のコマンドで変換できた。

```
ffmpeg -i input.mp4 -brand mp42 mp42_out.mp4
```


# どんなフォーマットなのかを確認する

```
ffmpeg -i input.mp4
```

## PS4で動画も音声も再生できるフォーマット

`mp42` は、動画も音声も問題なく再生できた。

```
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from '/mnt/contents/20190413_律_FC東京_ドリブル/V_20190413_133021_vHDR_On.mp4':
  Metadata:
    major_brand     : mp42
    minor_version   : 0
    compatible_brands: isommp42
    creation_time   : 2019-04-13T04:34:38.000000Z
    com.android.version: 8.0.0
  Duration: 00:04:14.30, start: 0.000000, bitrate: 20092 kb/s
    Stream #0:0(eng): Audio: aac (LC) (mp4a / 0x6134706D), 48000 Hz, stereo, fltp, 96 kb/s (default)
    Metadata:
      creation_time   : 2019-04-13T04:34:38.000000Z
      handler_name    : SoundHandle
    Stream #0:1(eng): Video: h264 (Baseline) (avc1 / 0x31637661), yuv420p(tv, smpte170m/bt470bg/smpte170m), 1920x1080, 19992 kb/s, SAR 1:1 DAR 16:9, 29.93 fps, 29.92 tbr, 90k tbn, 180k tbc (default)
    Metadata:
      creation_time   : 2019-04-13T04:34:38.000000Z
      handler_name    : VideoHandle
```

## PS4で動画は問題ないが、音声が再生できないフォーマット

`qt` は、音声が対応していないようだ。

```
Input #0, mov,mp4,m4a,3gp,3g2,mj2, from 'no_audio.mov':
  Metadata:
    major_brand     : qt  
    minor_version   : 512
    compatible_brands: qt  
    creation_time   : 2002-10-29T03:32:30.000000Z
  Duration: 00:03:22.29, start: 0.000000, bitrate: 13466 kb/s
    Stream #0:0(eng): Video: h264 (Constrained Baseline) (avc1 / 0x31637661), yuv420p, 1920x1080, 12950 kb/s, 30 fps, 24.50 tbr, 1k tbn, 2k tbc (default)
    Metadata:
      creation_time   : 2002-10-29T03:32:30.000000Z
      handler_name    : VideoHandler
    Stream #0:1(eng): Audio: pcm_s16le (sowt / 0x74776F73), 32000 Hz, mono, s16, 512 kb/s (default)
    Metadata:
      creation_time   : 2002-10-29T03:32:30.000000Z
      handler_name    : SoundHandler
```


# GoPro 6

APEMAN A66Sもかなりよかったので、GoProだとどんなものなのかも知りたいという気持ちもある。

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B07K373BXZ&linkId=92145c08856520202ae0539e865c9441"></iframe>
