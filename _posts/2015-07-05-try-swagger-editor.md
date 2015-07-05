---
layout: post
title: Try Swagger editor
date: 2015-07-05T14:21:00
---
# Swagger
REST風のAPIのドキュメントを書いてみようとおもって、探していた

[Swagger | The World's Most Popular Framework for APIs.](http://swagger.io/ "Swagger | The World's Most Popular Framework for APIs.")

以前はなかったような気がしたのだが、今はドキュメントを書くためのエディタも作っていることがわかった。
さらにそのエディタは、ドキュメント書くだけではなくて、
いろいろな言語でサーバーサイドとクライアントサイドのコードも作ってくれるということがわかった。

# Swagger Editor

[Swagger Editor](http://editor.swagger.io/#/ "Swagger Editor")

![Swagger Editor](/images/swagger-editor.png)

ここで動いているので特にそれを使えばよい

## Server Generate
サーバーは以下のような言語で出力してくれるみたい。

![Swagger Generate Server](/images/swagger-editor-generate-server-list.png)
## Client Generate
クライアントは以下のような言語で出力してくれるみたい。

![Swagger Generate Server](/images/swagger-editor-generate-client-list.png)

# Swagger Editor を Dockerで動かす

ソースコードも配っていて
[swagger-api/swagger-editor](https://github.com/swagger-api/swagger-editor "swagger-api/swagger-editor")
その中にdocker用にDockerfileもあるので作ってみた

```
git clone https://github.com/swagger-api/swagger-editor.git
cd swagger-editor
docker build -t swagger-editor .
```
しばし待つと出来上がるので、動かしてみる

```
docker run  --rm -p 3000:8080 -t swagger-editor
```
おそらくデーモンで起動するんだろうけど
終了するときはCtrl+c
コンソールには戻れた



Newを選んで、デフォルトでうまっているものを少し編集してサーバーのコードを
ダウンロード

# Swagger Editor で作ったコードをDockerで試す。

docker の node.js のコンテナで
実際に動かしてみる

```
unzip nodejs-server-generated.zip
cd nodejs-server
docker run --rm --privileged=true -p 3001:8080 -v $PWD:/work -ti node:0.12.5 /bin/bash
cd /work
npm install
node index.js
```

で、動く
