---
layout: post
title: サッカー関連のSPARQLクエリについて調べてみた
date: 2017-04-29T04:57:02
categories: sparql football wikipedia dbpedia soccer
---

# 概要

サッカー関連のSPARQLクエリについてよく考えるので、メモとして調べたことを残す

# DBpedia

本体と各言語ごとのサイトが存在するようだ。
返ってくることも違う感じ

全体
* [Virtuoso SPARQL Query Editor](https://dbpedia.org/sparql)

日本語
* [Virtuoso SPARQL Query Editor](http://ja.dbpedia.org/sparql)


# 検索ワード

背番号についてしらべたかったので、以下のように入れた結果、いくつかおもしろそうなものが見つかった。

* [sparql football no - Google 検索](https://www.google.co.jp/search?q=sparql+football+no&ie=utf-8&oe=utf-8)

## wikibooksのページ

* [XQuery/DBpedia with SPARQL - Football teams - Wikibooks, open books for an open world](https://en.wikibooks.org/wiki/XQuery/DBpedia_with_SPARQL_-_Football_teams)

### 検索例

上のwikibooksのページにあった、SPARQL クエリ

アーセナルの選手の誕生日と、出身地がでる

```sparql
PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
PREFIX p: <http://dbpedia.org/property/>  
PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>

SELECT * WHERE {
      <http://dbpedia.org/resource/Arsenal_F.C.> p:name ?player.
      ?player dbpedia-owl:birthPlace ?city;
              dbpedia-owl:birthDate ?dob.
      ?city geo:long ?long;
            geo:lat ?lat.
 }
```

日本語のdbpedia endpointだと結果が返ってこなかった

英語のページだと、でてきた

* [Virtuoso SPARQL Query Editor](https://dbpedia.org/sparql)

日本語のページだと、でてこなかった

* [Virtuoso SPARQL Query Editor](http://ja.dbpedia.org/sparql)

# 検索例

## アーセナル所属の選手の背番号

```sparql
PREFIX p: <http://dbpedia.org/property/>  
PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>

SELECT * WHERE {
      <http://dbpedia.org/resource/Arsenal_F.C.> p:name ?player.
      ?player dbpedia-owl:number ?num.
 }
```

# 参考

* [直感RDF!!　その2 -使いやすいRDFを作って，検索しよう。 - Qiita](http://qiita.com/maoringo/items/0d48a3d967a35581cc24)


# 参考図書

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B017LQG9XC&linkId=ef739d06595f6b8f39b7889985c0e4e6"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=433902869X&linkId=7e8ff9f1afa1b8b5409220ba1496cbcf"></iframe>


<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B00DR0DZCK&linkId=06fd37658d98f98f4404fe6ff7403172"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4627829310&linkId=436b7657627a93bc3a3374b8a5d17243"></iframe>
