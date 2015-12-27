---
layout: post
title: Elasticsearchに国土交通省位置参照情報を入れる、その２
date: 2015-12-26T05:31:00
---

# 大きな流れ

以前にも書いたが以下の２ステップが必要。

1. GeoJSONへ変換する
2. elasticsearchへ入れる



# GeoJSONへ変換する

[位置参照情報ダウンロードサービス](http://nlftp.mlit.go.jp/isj/ "位置参照情報ダウンロードサービス")

落としてきたデータが、zipで圧縮されていて、さらに中にあるファイルがShiftJISのcsvなので、これを一気に変換するようなdockerコンテナを作った。

1.unzip
2.nkf -S -w (入力をShiftJISとして、出力をUTF-8とする)
3.テンポラリファイルに書き出す
4.テンポラリファイルをGeoJSONに変換して、標準出力へ出す

テンポラリファイルを使わずに、パイプだけでやってみようとしたのだが、もしかするとサイズが大きいのでエラーなのかもしれない。
このあたりは、そのような記事をみかけたので試してみるとよいのかな。

# elasticsearchへ入れる

1. indexを作る
2. データをインポートする

elasticsearchに大量にインポートするときは以下を参照
[Bulk API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html#docs-bulk "Bulk API")
