---
layout: post
title: React UI Builerを試す
date: 2015-08-30T05:31:00
---
# React UI Builer



[ipselon/react-ui-builder](https://github.com/ipselon/react-ui-builder "ipselon/react-ui-builder")
をどこかで見つけてきた。
名前からしても、上のページの紹介からしても、

* React のUIが作れるのかなとおもった

上記のページにはビデオが２つ紹介されていて

* [React JS tutorial with React UI Builder - YouTube](https://www.youtube.com/watch?v=5nqOFSjXKPI "React JS tutorial with React UI Builder - YouTube")

少し古いバージョンでのビデオで、UIなどがちょっと違う感じがするが、大体同じであった。

これは14分くらいあり、reactのチュートリアルをReact UI Builderで実行するデモのようだった。
また reflux をつかっていることもわかった。

* [React UI Builder: how to create component - YouTube](https://www.youtube.com/watch?v=yycaq9qv7us "React UI Builder: how to create component - YouTube")

もう１つはこれで、３分半くらいだった。
create componentの方は、0.2.11をベースに作られているようで、UIはそっくりである。

デモをさわってみると、たしかにUIが作れる感じがあった。
また実際に自分で動かしてみても確かに動いた。

# できたこと

コンポーネントを作ることはできた。

# 作ったUIを自分のアプリケーションで使うには

作ったUIをコンポーネントにして、main.jsなりで利用することが１４分位ある方のビデオの最後で紹介されていた。

# はまったところ

よくビデオをみればよかったのだろうけど、いくつかあったので書いておく。
おそらく以下の点が守れればハマることはなかったのではないかと思っている。

* まずはプロジェクトのページをよく読む
* ビデオをよくみる


## mcに気を取られて最初をちゃんと見れない。

mcを使っているところに引っかかってしまい、ちゃんときけなかった。
mcが気にならないなら問題はない。

## 展開したばかりのreact-tutorial-masterをprojectのフォルダとしては使えなかった。

何度か見返した所、react-tutorial-masterを使っていることに気づいた。
よく考えたらタイトルにも書いてあるのだけれど、全く気づかなかった。
気づいた後に、zipをもってきて、展開したものを使おうとしたが使えなかった。
.builderがないからなのかなぁというエラーメッセージが出ていたと思う。

## server.js,comments.jsonをreact-tutorial-masterからコピーすることに気づかなかった。

結構頭のほうで、server.jsを起動しているがこれがどこからくるのかわからなかった。

```
node server.js
```

よく聞くと、server.jsとcomments.jsonはreact-tutorial-masterからコピーしているようだった。

expressをpackage.jsonに追加しておく。

## vagrantだったらsshのポートを変更する

react-ui-builderのサーバーは、2222固定であるよだった。
vagrantだったら、2222はsshに使う可能性があるので、sshのポートを変更したい。
まずは、vagrantのバージョンを1.7.2以降にする。

その後、以下を参考に

[Cannot override default ssh port forwarding · Issue #3232 · mitchellh/vagrant](https://github.com/mitchellh/vagrant/issues/3232#issuecomment-76710491 "Cannot override default ssh port forwarding · Issue #3232 · mitchellh/vagrant")

Vagrantファイルに以下を追加する

```
config.vm.network :forwarded_port, guest: 22, host: 12345, id: 'ssh'
```

# 使い方

## まずはreact-ui-builderを実行してプロジェクトをクローンする

react bootstrapを使うことにした
あらかじめ、probeというからディレクトリを作っておく。

* ディレクトリがないとエラーになる
* 空でないとエラーになる


## server.jsなどをコピーする

react-tutorial-masterからserver.jsをコピーする。
あとcomments.jsonもコピーしておく。

また、probeの中にあるpackage.jsonにexpressに関する記述がないので追加する。

```
npm install
```

## bundle.jsを作る

index.htmlの中身を見てみたら
bundle.jsを読み込もうとしているが、このファイルがないことがわかった。

probeのディレクトリで

```
npm run
```
以下のものがつかえそうだとわかった。
このあたりpackage.jsonにも書いてある。

```
npm run-script build-dev
```

問題がなければ、bundle.jsができあがる

## サーバーを立ち上げる。

```
node ./server.js
```

するとサーバーが立ち上がる。
ブラウザでアクセスするとタイトルしかみえなかった

```
http://localhost:3000
```
次に以下のようにアクセスするとjsonが返ってくるはず。
```
http://localhost:3000/comments.json
```

## プロジェクトのセッティングでproxyの設定を行う

react ui builder の方で、projectのセッティングでproxyの設定を行う

```
http://localhost:3000
```
を入力しておく。

```
http://localhost:2222
```
にアクセスると、3000番のところをproxyしてくれるようであった。

おそらくUIを作った後に、変更を加えていった時に便利なのかなと思った。


# Docker

公開されていた

[lowlo/react-ui-builder](https://hub.docker.com/r/lowlo/react-ui-builder/ "lowlo/react-ui-builder")
