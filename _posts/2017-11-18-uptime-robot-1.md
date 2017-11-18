---
layout: post
title: Uptime Robotを使って、サイトが落ちていないか監視して、SlackとDiscordに通知する。
description: Uptime Robotを使って、サイトが落ちていないか監視してSlackとDiscordに通知する
date: 2017-11-18T14:57:02
categories: uptimerobot slack discord monitoring
---

# 概要

[Uptime Robot](https://uptimerobot.com/)を使ってみる。

## Slackの場合

デフォルトで用意してあるので、設定は非常に簡単、

1. サインアップすると、確認のemailがくる
1. URLをクリックする
1. ログインする
1. 設定画面があるので、必要なことを記録して保存
1. slackの設定が必要なら My Settings から、通知先を追加
1. さっき作った設定に、slackを追加する

普通のwebhookも使えるようだ

## Discordの場合

Discordの場合は、Webhookを使う

Webhookを作るのは非常に簡単で、チャンネルのところにある、

1. 設定のボタンを押す
1. `Webhook` とかいてあるところを押す
1. `Webhook 作成` をクリック
1. でてきた、`Webhook URL` を設定に追加。
1. パラメータについては、、、

パラメータの詳細については以下のページ。日本語のページはないようなので、ヘルプからくるときは、
エラーページで、言語を `English` にすると、表示されてくる。
日本語がないと、英語にいくということはないので、注意する

https://support.discordapp.com/hc/en-us/articles/228383668


```
Uptime Robot will add the below querystring to the end of the requests sent:

monitorID=*monitorID*&monitorURL=*monitorURL*&monitorFriendlyName=*monitorFriendlyName*&alertType=*alertType*&alertTypeFriendlyName=*alertTypeFriendlyName*&alertDetails=*alertDetails*&monitorAlertContacts=*monitorAlertContacts*
So, make sure that the URL added ends with

? (if it doesn't have a querystring) or
& (if it already has a querystring)
to make it a valid request.

Or, you can create a totally custom web-hook URL by using the variables.
```


とりあえずメッセージが届く確認をしたときの設定はこんな感じ。
以下の３つを設定した。

`Friendly Name` には、わかりやすい名前を入れて

`URL to Notify` には、URLは、DiscordのWebhook URLをいれて、最後に、`?` をつける。

`POST Value (JSON Format)` には、以下のような感じ

```json
{"content": "@channel *monitorFriendlyName*  *monitorURL* is *alertTypeFriendlyName* . *alertDetail* .." }
```

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4873117917&linkId=006425e083c405aad908baf2d6819134"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B01HI2TD28&linkId=b21d59c9a2ad0e1dbb24d5d1a236b650"></iframe>
