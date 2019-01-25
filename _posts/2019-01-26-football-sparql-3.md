---
layout: post
title: Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた、その３、背番号も表示する
description: Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた、アーセナルに所属する選手名と背番号を表示する
date: 2019-01-26T00:07:02
categories: sparql football wikipedia dbpedia soccer wikidata
---

前回、[Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた – どこかのブログ – どこかの開発者](http://manabu.github.io/football-sparql-2/ "Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた – どこかのブログ – どこかの開発者") を作ったが、過去の選手もでてきていたので、現在の所属選手だけだしてみようとおもう。


背番号は、[sport number - Wikidata](https://www.wikidata.org/wiki/Property:P1618 "sport number - Wikidata")このプロパティでとれる

```
SELECT ?s ?w ?desc WHERE {
  ?s wdt:P54 wd:Q9617 .
  ?s wdt:P1618 ?w.
  OPTIONAL {
     ?s rdfs:label ?desc filter (lang(?desc) = "en").
   }
 }
```


これをクリックして、実行ボタンを押すと表示される。

[Wikidata Query Service](https://query.wikidata.org/#SELECT%20%3Fs%20%3Fw%20%3Fdesc%20WHERE%20%7B%0A%20%20%3Fs%20wdt%3AP54%20wd%3AQ9617%20.%0A%20%20%3Fs%20wdt%3AP1618%20%3Fw.%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%20%3Fs%20rdfs%3Alabel%20%3Fdesc%20filter%20%28lang%28%3Fdesc%29%20%3D%20%22en%22%29.%0A%20%20%20%7D%0A%20%7D "Wikidata Query Service アーセナルに所属している選手と背番号表示")

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B017LQG9XC&linkId=fcfdf756ec95bd5d1881f48f75da6e0f"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B0721RYV2P&linkId=8cf2b94ab97c0beffbee811c591e7764"></iframe>
