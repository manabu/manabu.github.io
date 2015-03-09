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

まずは、インストールできるかだけを確認する
docker run -ti node:0.12.0 /bin/bash
npm install -g csv2geojson

次に、実際のデータをあつかえるかを試す

位置参照情報ダウンロードサービスから落としてきたデータは日本語がSJISなので
まずは、変換する。

unzip 31000-12.0a.zip
nkf 31000-12.0a/31_2013.csv > 31000-12.0a/31_2013.utf8.csv


```
docker run --rm -v $PWD:/data -ti node:0.12.0 /bin/bash
csv2geojson  -lat 緯度 -lon 経度 31_2013.utf8.csv
```

ではうまくいかなかった。
失敗の可能性はいくつか考えられて、
そもそもオプションがあってない(--lat なのか -lat なのか)
日本語がとおらない。

などなど

まずは、ダブルクォーテーションで括っていても大丈夫かを確認するために、以下のように置き換えた
"latitude","longtitude"

日本語が通るか気にするくらいなら、このように加工すべきか。

geojsonにしたら、elasticsearchに入れるだけなので

elasticsearchにkuromojiをいれたdockerコンテナをつくる
* [dockerfile/elasticsearch · GitHub](https://github.com/dockerfile/elasticsearch)


Dockerfile

```
FROM dockerfile/elasticsearch:latest
run /elasticsearch/bin/plugin -install elasticsearch/elasticsearch-analysis-kuromoji/2.4.1
```

起動する
```
docker run -d -p 9200:9200 -p 9300:9300 -v $PWD/data:/data manabu/elasticsearch /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
```


インデックスを作る
```
#!/bin/bash
# require kuromoji plugin

curl -XPUT 'localhost:9200/isj' -d '{
  "settings": {
    "analysis": {
      "analyzer": {
        "default" : {
          "type" : "kuromoji_analyzer"
        }
      }
    }										 }
}'
```												  
インデックスを作るbashスクリプト
```
#!/bin/bash

curl -XPUT 'http://localhost:9200/isj/'

curl -XPUT 'http://localhost:9200/isj/isj/_mapping' -d '
{
  "isj" : {
    "properties": {
      "geometry": {
        "type": "geo_shape",
        "tree": "quadtree",
        "precision": "1m"
      }
    }
  }
}'
```


import用のruby script

```ruby
require 'json'
json_file_path = 'geojson.json'
json_data = open(json_file_path) do |io|
  JSON.load(io)
end
id = 1
json_data['features'].each do |item|
  header = '{ "index" : { "_index" : "isj", "_type" : "isj", "_id" : "' + id.to_s + '" } }'
  puts header
  puts JSON.dump(item)
  id=id+1
end
```	  



