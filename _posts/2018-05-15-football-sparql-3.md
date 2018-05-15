---
layout: post
title: Wikidataを使ってサッカー選手の背番号を取得する
description: Wikidataを使ってサッカー選手の背番号を取得する
date: 2018-05-15T00:07:02
categories: sparql football wikipedia soccer wikidata
---

以前、[Wikidata を使ってアーセナルに所属したことがある選手一覧](http://manabu.github.io/football-sparql-2/ "Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた – どこかのブログ – どこかの開発者") を作ったが、今回は背番号も取得してみる。

# 背番号をあらわすプロパティと、そのデータ

これが、背番号をあらわすプロパティのようである。
[sport number - Wikidata](https://www.wikidata.org/wiki/Property:P1618)
ただし、以下の点はこれからさらなる調査が必要かもしれない。

* すべての選手がこのプロパティをもっているわけではないの
 * そのため、`OPTIONAL` としている
 * ほかのプロパティがあるかもしれない
* アーセナルに所属していたときの背番号ではないケースがあるかもしれない
 * もう少し複雑なクエリが必要？


```sparql
SELECT ?s  ?sLabel  ?num WHERE {
  ?s wdt:P54  wd:Q9617.
  OPTIONAL {?s wdt:P1618 ?num.}
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

[Jack Wilshere - Wikidata](https://www.wikidata.org/wiki/Q15199)
の背番号は、`10`でとれている。

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4334979335&linkId=8731b5b508e4c9c9f6a828272b071fe2"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=433902869X&linkId=75c9c47119193e30d4fe1a9d0da668fc"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B017LQG9XC&linkId=652b85de97312e6c214c6337377221f6"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4627829310&linkId=e27bfe9011ffee1dca6c4aeac9944d6c"></iframe>
