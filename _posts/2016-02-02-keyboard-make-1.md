---
layout: post
title: Customized Keyboard のチュートリアルするための準備１
date: 2016-02-02T03:31:00
---

# やってみたいこと。

キーボード自作とか、調べるだけならと思った結果、以下のものをみつけた。
作りたいものいくつかあるけど、

[Customized Keyboard Tutorial for Hackers and Developers | Toptal](http://www.toptal.com/embedded/from-the-ground-up-how-i-built-the-developers-dream-keybooard "Customized Keyboard Tutorial for Hackers and Developers | Toptal")

これの Step one と two　は、やってみたいな。

# 部品

必要そうなもの

|部品|個数|URL|表面実装 URL|
| - | - | - |
|Arduino Micros|1|[Amazon.co.jp： Arduino Micro: パソコン・周辺機器](http://www.amazon.co.jp/Arduino-ARD-A000059-Micro/dp/B00AFY2S56 "Amazon.co.jp： Arduino Micro: パソコン・周辺機器")||
|抵抗10kΩ|2|[カーボン抵抗（炭素皮膜抵抗）　１／２Ｗ　１０ｋΩ　（１００本入）: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gR-07838/ "カーボン抵抗（炭素皮膜抵抗）　１／２Ｗ　１０ｋΩ　（１００本入）: パーツ一般 秋月電子通商 電子部品 ネット通販")|[パナソニックエレクトロニックデバイス ＥＲＪ３ＧＥＹＪ１０３Ｖ １６０８（０６０３）チップ抵抗　１０ＫΩ](https://www.sengoku.co.jp/mod/sgk_cart/detail.php?code=2A5R-DUEE "パナソニックエレクトロニックデバイス ＥＲＪ３ＧＥＹＪ１０３Ｖ １６０８（０６０３）チップ抵抗　１０ＫΩ")|
|スイッチ（タクトスイッチでよい？）|4|[タクトスイッチ（水色）: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-03649/ "タクトスイッチ（水色）: パーツ一般 秋月電子通商 電子部品 ネット通販")||
|ダイオード|4|[汎用小信号高速スイッチング・ダイオード　１Ｎ４１４８　１００Ｖ２００ｍＡ（５０本入）: 半導体 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gI-00941/ "汎用小信号高速スイッチング・ダイオード　１Ｎ４１４８　１００Ｖ２００ｍＡ（５０本入）: 半導体 秋月電子通商 電子部品 ネット通販")|[高速スイッチング・ダイオード　１Ｎ４１４８Ｗ　（４０個入）: 半導体 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gI-07084/ "高速スイッチング・ダイオード　１Ｎ４１４８Ｗ　（４０個入）: 半導体 秋月電子通商 電子部品 ネット通販")|
|ブレッドボード|1|[ブレッドボード　ＢＢ－８０１: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-05294/ "ブレッドボード　ＢＢ－８０１: パーツ一般 秋月電子通商 電子部品 ネット通販")||
|ジャンパワイヤ|いくつか|[ブレッドボード・ジャンパーワイヤ　ＥＩＣ－Ｊ－Ｌ: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-00288/ "ブレッドボード・ジャンパーワイヤ　ＥＩＣ－Ｊ－Ｌ: パーツ一般 秋月電子通商 電子部品 ネット通販")||
|ジャンパコード|いくつか|[ブレッドボード・ジャンパーコード（オス－オス）セット: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gC-05159/ "ブレッドボード・ジャンパーコード（オス－オス）セット: パーツ一般 秋月電子通商 電子部品 ネット通販")|||


ダイオードは、[ErgoDox.org - Hardware](http://ergodox.org/Hardware.aspx "ErgoDox.org - Hardware")をみると、

```
1N4148 diode
(SOD-123 package (SMD),
or DO-35 (through hole 0.3" pitch))
```

となっているので、同じものを選ぶことにしてみる。

SMDでやったらどうなるのか考えてみたが、
基盤とかどうするんだろうか、、、という感じ。
こちらのほうは、あまり考えないことにする。
1リールとかあっても、一生使い切れそうにない気がするが、、、


# ブレッドボード

大きいのがよいなら

[ブレッドボード　ＢＢ－１０２: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-09257/ "ブレッドボード　ＢＢ－１０２: パーツ一般 秋月電子通商 電子部品 ネット通販")

# タクトスイッチ

[タクトスイッチ（大）１０個セット: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-02561/ "タクトスイッチ（大）１０個セット: パーツ一般 秋月電子通商 電子部品 ネット通販")

# SMD

少しちさすぎる？

[表面実装用タクトスイッチ　ＳＫＲＰＡＣＥ０１０（５個入）: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-06185/ "表面実装用タクトスイッチ　ＳＫＲＰＡＣＥ０１０（５個入）: パーツ一般 秋月電子通商 電子部品 ネット通販")

[表面実装用タクトスイッチ　（１０個入）: パーツ一般 秋月電子通商 電子部品 ネット通販](http://akizukidenshi.com/catalog/g/gP-08081/ "表面実装用タクトスイッチ　（１０個入）: パーツ一般 秋月電子通商 電子部品 ネット通販")