---
layout: post
title: Atom 1.8.0 にしたらエラーがでた。その解決策。
date: 2016-07-31T11:21:01
---

# coreos-vagrant での port forward の設定をなんとかしたかった

なんか起動するたび？か、いつかのタイミングでちょくちょくforwardするポートを
GUIでポチポチしていたのだが、どうにかならないかなぁとおもって、
よくみてみたらしたのような部分を見つけた

* [coreos-vagrant/Vagrantfile at master · coreos/coreos-vagrant](https://github.com/coreos/coreos-vagrant/blob/master/Vagrantfile#L108-L110)

さらに、このファイルにこのままかくのかなぁ？
とおもってたら

* [coreos-vagrant/config.rb.sample at master · coreos/coreos-vagrant](https://github.com/coreos/coreos-vagrant/blob/master/config.rb.sample#L89-L90)

こんな記述をみつけて

```
cp config.rb.sample config.rb
```

適当に修正して

```
vagrant up
```

こんな感じで無事にport forwardできるようになった
