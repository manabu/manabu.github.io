---
layout: post
title: Arduino Leonard 互換ボードでキーボードを作る、その２、ダイオード
date: 2016-11-23T01:53:02
categories: arduino keyboard
---

# 今回試したこと

matrixへ、向けて、まずは、1x1を試してみることにした。
確認したいことは
* 以前試した1つのボタン（push button）のやつが動くことを確認する
* 1N4148というダイオードを正しい向きにいれてみる。
* 1N4148を逆向きにすると、ボタンを押しても認識しないことの確認。

# 結論

* １つのボタンで動いた
* 1N4148をいれても上手く動いた
* 1N4148を逆にすると、ボタンを押しても認識しないことを確認した。

# 問題点？

* 1度おしただけだとおもっているが、文字が何度も出力された。チャタリング？
 * 今後の課題か

# 回路

![1 Button 1 Diode](/images/1button_1diode.png)

# コード

```
// pin 2
int Pin2=2;

void setup() {
  Serial.begin(9600);
  pinMode(Pin2,  INPUT_PULLUP);
}

int key_enable = 1;
int key_enableB = 1;
void loop() {
    if(digitalRead(Pin2)==LOW){
      key_enable = 0;
    }else{
      if (key_enable == 0) {
        Serial.println("A");
        key_enable = 1;
      }
    }
}
```

# Arudinoをボードを挿し間違えた時にでるエラー

Arduino Leonard互換ボードで最後に作業したのをすっかり忘れて
Arduino Unoをさしたら、Verifyはうまくいくが、Uploadすると
以下のようなエラーがでた。

```
avrdude: butterfly_recv(): programmer is not responding
```

色々でてくるが、結局ボードの選択ミスで、正しい物を選択すると、問題なくUploadできた。
