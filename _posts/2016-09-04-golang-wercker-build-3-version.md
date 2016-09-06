---
layout: post
title: werckerからgithubへ配置するときにバージョンを付ける
date: 2016-09-04T11:21:01
---

# バージョンを付けてみたかった

* [motemen/gobump: Bumps up Go program version](https://github.com/motemen/gobump)

を参考に

```
package main

const version = "0.1.0"

import (
    "fmt"
    "io"
    "os"
)

func testPrint(w io.Writer){
        fmt.Fprint(w,"Hello world!!\n")
}

func main() {
        testPrint(os.Stdout)
}
```

こんなコードにしてみたら

werckerで以下のように怒られた

```
./helloworld.go:5: syntax error: non-declaration statement outside function body
```

goの書き方の問題だったので、なおしてみた

# githubにtagがないと、指摘されているようだ

なにもタグを打たずに実行したらこうなった。


```
2016/09/03 19:04:34 requestURL: https://api.github.com/repos/manabu/wercker-golang-helloworld-build-cmd/releases/4045586
2016/09/03 19:04:35 HttpStatus: 204 No Content
2016/09/03 19:04:35 requestURL: https://api.github.com/repos/manabu/wercker-golang-helloworld-build-cmd/git/refs/tags/pre-release
2016/09/03 19:04:35 HttpStatus: 422 Unprocessable Entity
Github returned 422 Unprocessable Entity
```


# すでにあるバージョンだと

こんな感じに言われる。

```
2016/09/03 19:36:31 requestURL: https://uploads.github.com/repos/manabu/wercker-golang-helloworld-build-cmd/releases/4045669/assets?name=wercker-golang-helloworld-build-cmd_windows_amd64.zip
2016/09/03 19:36:32 HttpStatus: 422 status code 422
2016/09/03 19:36:32 HttpStatus: 422 status code 422
2016/09/03 19:36:32 HttpStatus: 422 status code 422
2016/09/03 19:36:32 HttpStatus: 422 status code 422
2016/09/03 19:36:32 HttpStatus: 422 status code 422
2016/09/03 19:36:32 HttpStatus: 422 status code 422
2016/09/03 19:36:32 HttpStatus: 422 status code 422
7 errors occurred:
--> upload /pipeline/output/dist/wercker-golang-helloworld-build-cmd_darwin_386.zip error: Github returned 422 status code 422 (this is probably because the release already exists)

--> upload /pipeline/output/dist/wercker-golang-helloworld-build-cmd_darwin_amd64.zip error: Github returned 422 status code 422 (this is probably because the release already exists)

--> upload /pipeline/output/dist/wercker-golang-helloworld-build-cmd_linux_amd64.zip error: Github returned 422 status code 422 (this is probably because the release already exists)

--> upload /pipeline/output/dist/wercker-golang-helloworld-build-cmd_linux_386.zip error: Github returned 422 status code 422 (this is probably because the release already exists)

--> upload /pipeline/output/dist/wercker-golang-helloworld-build-cmd_windows_amd64.zip error: Github returned 422 status code 422 (this is probably because the release already exists)

--> upload /pipeline/output/dist/wercker-golang-helloworld-build-cmd_windows_386.zip error: Github returned 422 status code 422 (this is probably because the release already exists)

--> upload /pipeline/output/dist/SHASUMS error: Github returned 422 status code 422 (this is probably because the release already exists)
```

# mergeとかPRとかのときは、新しくタグをつくってくれそうだ

tagを打った時に、ビルドが始まって欲しいとおもっている
