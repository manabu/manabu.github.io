---
layout: post
title: Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた
description: Wikidataを使ってサッカー関連のSPARQLクエリについて調べてみた
date: 2017-11-19T00:07:02
categories: sparql football wikipedia dbpedia soccer wikidata
---

以前、[DBPediaを使ったやつ](http://manabu.github.io/football-sparql-1/ "サッカー関連のSPARQLクエリについて調べてみた – どこかのブログ – どこかの開発者") を作ったが、今回は [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page "Wikidata")

# Wikidata と DBPedia との違い

個人の印象なのと、最近は少し情勢がかわっているかもしれないが。

||Wikidata|DBPedia|
|---|---|---|
|更新頻度|ほぼ最新？|ちょっと遅い？|
|プロパティのわかりやすさ|プロパティだけみてもわかりにくい|みただけでわかりやすい|

# Wikidata の Sparql Endpoint

Wikidata の Sparql Endpoint は以下の場所。

* [Wikidata Query Service](https://query.wikidata.org/)


# アーセナル所属したことのある選手一覧

過去の選手も含めて、アーセナル[Arsenal F.C. - Wikidata](https://www.wikidata.org/wiki/Q9617 "Arsenal F.C. - Wikidata")　に、所属[member of sports team - Wikidata](https://www.wikidata.org/wiki/Property:P54 "member of sports team - Wikidata")
していた選手の一覧は以下でとれる

```sparql
SELECT ?s  ?sLabel WHERE {
  ?s wdt:P54 wd:Q9617;
  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
```

今所属している選手も、過去に所属していたも選手でてくるので

* [浅野拓磨](https://www.wikidata.org/wiki/Q11557367 "浅野拓磨")
* [宮市亮](https://www.wikidata.org/wiki/Q310605 "宮市亮")

なんかもでてくる。

# 参考

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4334979335&linkId=8731b5b508e4c9c9f6a828272b071fe2"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=433902869X&linkId=75c9c47119193e30d4fe1a9d0da668fc"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B017LQG9XC&linkId=652b85de97312e6c214c6337377221f6"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4627829310&linkId=e27bfe9011ffee1dca6c4aeac9944d6c"></iframe>
