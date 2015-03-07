---
layout: post
title: Elasticsearchに国土交通省位置参照情報を入れる
---

Elasticsearchに住所のデータをいれて、住所をいれたら緯度経度を返すようなものを作りたい。

最初にデータを以下の場所からダウンロードする

* [位置参照情報ダウンロードサービス](http://nlftp.mlit.go.jp/isj/)

ファイルの中身を確認すると、CSVだった。
小さなデータであれば、以下のようなサイトで変換することもできる。

* [CSV to GeoJSON](http://togeojson.com/)

全国分入れようとすると、それなりっぽいのデータっぽいので、ツールを探した

* [mapbox/csv2geojson · GitHub](https://github.com/mapbox/csv2geojson)

node.jsで動くようなので、まずはこれを試す。

そのためにdockerでnode.js環境を用意する

* [node Repository | Docker Hub Registry - Repositories of Docker Images](https://registry.hub.docker.com/_/node/)

最新版は0.12.0のようなので

docker pull node:0.12.0
