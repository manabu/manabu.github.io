---
layout: post
title: python flask の中でcronのような動作をさせたい
date: 2017-11-19T00:27:02
categories: python
---

flask の中で、cronのような動作をさせたいと思った。
以下を使うと良さそうだ

* [viniciuschiele/flask-apscheduler: Adds APScheduler support to Flask](https://github.com/viniciuschiele/flask-apscheduler)

# サンプルのコードをコピーアンドペーストして動かない時

エラーメッセージみればわかる人はわかるが、
`jobs.py` のコードをコピーして `app.py` の中にいれたら、
上手く動かなった

```
class Config(object):
    JOBS = [
        {
            'id': 'job1',
            'func': 'jobs:job1',
            'args': (1, 2),
            'trigger': 'interval',
            'seconds': 10
        }
    ]

    SCHEDULER_API_ENABLED = True
```

問題の修正方法の１つは

```
            'func': 'jobs:job1',
```

を

```
            'func': '__main__:job1',
```

にする

その他(ためしてないけど)

* `app.py` というファイルをやめて、`jobs.py`


<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B01HSMKJIA&linkId=15b971ea669bd0bde50474db62c2e336"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=B00K00W9LI&linkId=1e89a6ed7ffdd0c7fd64a7522701d046"></iframe>

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=000000&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=mi3002-22&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=487311778X&linkId=f90f884a7e78d7d5fcef9427012daef5"></iframe>
