---
layout: post
title: リモートのfirefoxを起動する
date: 2016-07-15T01:21:01
---

# リモートのfirefoxを起動したい

ローカルにもリモートにもfirefoxがあるとき、リモートのfirefoxを起動したい

* [How do I launch a remote firefox window via SSH? - Ask Ubuntu](http://askubuntu.com/questions/3515/how-do-i-launch-a-remote-firefox-window-via-ssh)

ここにかいてあったが


ssh -X などで入った先で、以下のコマンドを実行すると良い

```
firefox -no-remote
```
