---
layout: post
title: Docker の python:2.7.11 をベースに localeを設定する
date: 2016-03-25T03:31:00
---

django関連で以下のようなエラーがでていた。

```
fields.E134: max_digits must be greater or equal to decimal_places
```

で、その後いろいろ調べた結果、localeが必要かと思い

```
FROM python:2.7.11
RUN apt-get update -qq ; apt-get install -y locales ; apt-get clean
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
```

こんな感じにして見てたがうまくいかず

最終的に

```
FROM python:2.7.11
RUN apt-get update -qq ; apt-get install -y locales ; apt-get clean
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
```

こんな感じにしてみたら、うまくいった。

参考にしたのは以下のサイト

* [locale setting for debian · Issue #276 · phusion/baseimage-docker](https://github.com/phusion/baseimage-docker/issues/276#issue-125378976)
