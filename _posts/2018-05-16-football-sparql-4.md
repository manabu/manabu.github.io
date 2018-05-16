---
layout: post
title: Wikidataを使ってサッカー選手がチームに所属した日を調べる
description: Wikidataを使ってサッカー選手がチームに所属した日を調べる
date: 2018-05-16T23:07:02
categories: sparql football wikipedia soccer wikidata
---

以前、[Wikidataを使ってサッカー選手の背番号を取得する](http://manabu.github.io/football-sparql-3/ "Wikidataを使ってサッカー選手の背番号を取得する – どこかのブログ – どこかの開発者") を作ったが、今回はチームに所属した日も取得してみる。

# 所属日をあらわすプロパティと、そのデータ

今回もアーセナルをターゲットにしてみる。

所属した日をあらわすプロパティのようである。
[start time - Wikidata](https://www.wikidata.org/wiki/Property:P580)
ただし、以下の点はこれからさらなる調査が必要かもしれない。

* すべての選手がこのプロパティをもっているわけではないかもしれない
 * ほかのプロパティがあるかもしれない


```sparql
SELECT ?s  ?sLabel ?o ?num WHERE {
  ?s p:P54 [ ps:P54 wd:Q9617 ;  pq:P580 ?o ]
  OPTIONAL {?s wdt:P1618 ?num.}
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

[Wikidata Query Service](https://query.wikidata.org/#SELECT%20%3Fs%20%20%3FsLabel%20%3Fo%20%3Fnum%20WHERE%20%7B%0A%20%20%3Fs%20p%3AP54%20%5B%20ps%3AP54%20wd%3AQ9617%20%3B%20%20pq%3AP580%20%3Fo%20%5D%20%0A%20%20OPTIONAL%20%7B%3Fs%20wdt%3AP1618%20%3Fnum.%7D%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22.%20%7D%0A%7D%0A)

[Jack Wilshere - Wikidata](https://www.wikidata.org/wiki/Q15199)
所属したのが、`2008年1月1日`だと、とれている。
背番号も`10`と取れている。

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4334979335&linkId=8731b5b508e4c9c9f6a828272b071fe2"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=433902869X&linkId=75c9c47119193e30d4fe1a9d0da668fc"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B017LQG9XC&linkId=652b85de97312e6c214c6337377221f6"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4627829310&linkId=e27bfe9011ffee1dca6c4aeac9944d6c"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4839952264&linkId=4f5b87d8a683a92534eaa50b1cf5452d"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4767824710&linkId=5943862fe9df8fb74357e7a9dbee1731"></iframe>
