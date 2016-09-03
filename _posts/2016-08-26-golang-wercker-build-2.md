---
layout: post
title: Goを始めてみた。werckerでビルドしてみる。
date: 2016-08-26T11:21:01
---

# やりたいこと

Goで書いたhelloworldだけするプログラムを
wercker でbuildして、githubに置きたい。

## 感想

wercker動き出しまで速い。

## 失敗したこと

deployの中を１つづつ詰めていこうと思ったのだけど
deployというpipelineを作ることをしていなくて、
まったくdeployプロセスがおこなわれていなかった。

書きなおそうかと思ったけど、失敗をそのまま記録することにした。

deployというpipelineを作ったらうまくいった

# まずはgithubにレポジトリを作る

githubにレポジトリを作る

* [manabu/wercker-golang-helloworld-build-cmd: Build binaries for hello world command](https://github.com/manabu/wercker-golang-helloworld-build-cmd)

# 手元にcloneする

```
git clone https://github.com/manabu/wercker-golang-helloworld-build-cmd.git
```

# Hello world を作る

日本語は問題ないと思うが念の為、日本語をない状態にしてみた

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello world!!")
}
```

# 手元で実行する

本来はテストをしたほうがよいのかもしれないが、まずは実行してみる

```
$ go run helloworld.go
Hello world!!
```

# githubへpush

# wercker で登録

# werckerどうなるか

READMEを更新してpushしてみた
buildというところが成功していた
あとは失敗していない感じ

# テストを書く。

標準出力へ出力するだけだったので、以下を参考にしてテストをかく

* [golangでIOへのテストを行う | おおたの物置](http://ota42y.com/blog/2015/04/01/go-io-test/)

# わざと失敗するテストを書く

# 失敗することを確認する

# プログラムの修正をして、なおることを確認

# build してみたい

* [Go プロジェクトのバージョニングとリリースを CI で自動化する - 詩と創作・思索のひろば](http://motemen.hatenablog.com/entry/2015/08/go-auto-gobump-ci)

ここを参考に、以下を参照

* [ghq/wercker.yml at master · motemen/ghq](https://github.com/motemen/ghq/blob/master/wercker.yml)

## boxだけ変えてみる

```
box: tcnksm/gox
```

問題なく、ビルドは通った

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - wercker/golint
    - script:
        name: go build
        code: |
          go build ./...
    - script:
        name: go test
        code: |
          go test ./...
```

# build stepsを変えてみる

うまくいった

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
```

# deploy scriptを追加

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
```

## motemen/gobump-github-pull-request について

おそらく、ほかのブランチ、PRからの取り込みではないのではないかとおもい
この部分はまずは省略してみる。

あとでわかるが、これを省いたのは失敗だった

# deploy script , gox 部分追加

最後のdestのインデントが失敗していたようだが動いた
うまく動いた

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
- script:
    name: go get
    code: |
      go get ./...
- wercker/gox:
    os: darwin linux windows
    arch: 386 amd64
    output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
dest: $WERCKER_OUTPUT_DIR/pkg
```

# script 追加

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
- script:
    name: go get
    code: |
      go get ./...
- wercker/gox:
    os: darwin linux windows
    arch: 386 amd64
    output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
    dest: $WERCKER_OUTPUT_DIR/pkg
- script:
    name: include assets into artifacts
    code: |
      for dir in $WERCKER_OUTPUT_DIR/pkg/*; do
        if [ -d "$dir" ]; then
          cp -R zsh/ "$dir"
          cp ghq.txt "$dir/README.txt"
        fi
      done
```

# zip

うまく動いた

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
- script:
    name: go get
    code: |
      go get ./...
- wercker/gox:
    os: darwin linux windows
    arch: 386 amd64
    output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
    dest: $WERCKER_OUTPUT_DIR/pkg
- script:
    name: include assets into artifacts
    code: |
      for dir in $WERCKER_OUTPUT_DIR/pkg/*; do
        if [ -d "$dir" ]; then
          cp -R zsh/ "$dir"
          cp ghq.txt "$dir/README.txt"
        fi
      done
- tcnksm/zip:
    input: $WERCKER_OUTPUT_DIR/pkg
    output: $WERCKER_OUTPUT_DIR/dist
```

# set release tag

うまく動いた


```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
- script:
    name: go get
    code: |
      go get ./...
- wercker/gox:
    os: darwin linux windows
    arch: 386 amd64
    output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
    dest: $WERCKER_OUTPUT_DIR/pkg
- script:
    name: include assets into artifacts
    code: |
      for dir in $WERCKER_OUTPUT_DIR/pkg/*; do
        if [ -d "$dir" ]; then
          cp -R zsh/ "$dir"
          cp ghq.txt "$dir/README.txt"
        fi
      done
- tcnksm/zip:
    input: $WERCKER_OUTPUT_DIR/pkg
    output: $WERCKER_OUTPUT_DIR/dist
- script:
    name: set release tag
    code: |
      if [ -n "$GOBUMP_NEW_VERSION" ]; then
        export RELEASE_TAG="v$GOBUMP_NEW_VERSION"
      fi
```

# tcnksm/ghr

予想では失敗すると思ったが、成功してしまった

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
- script:
    name: go get
    code: |
      go get ./...
- wercker/gox:
    os: darwin linux windows
    arch: 386 amd64
    output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
    dest: $WERCKER_OUTPUT_DIR/pkg
- script:
    name: include assets into artifacts
    code: |
      for dir in $WERCKER_OUTPUT_DIR/pkg/*; do
        if [ -d "$dir" ]; then
          cp -R zsh/ "$dir"
          cp ghq.txt "$dir/README.txt"
        fi
      done
- tcnksm/zip:
    input: $WERCKER_OUTPUT_DIR/pkg
    output: $WERCKER_OUTPUT_DIR/dist
- script:
    name: set release tag
    code: |
      if [ -n "$GOBUMP_NEW_VERSION" ]; then
        export RELEASE_TAG="v$GOBUMP_NEW_VERSION"
      fi
- tcnksm/ghr:
    token: $GITHUB_TOKEN
    input: $WERCKER_OUTPUT_DIR/dist
    replace: true
    version: $RELEASE_TAG
    opt: --draft
```

# motemen/gobump-github-pull-request

```
- motemen/gobump-github-pull-request:
    github_token: $GITHUB_TOKEN
    label_pattern_major: ^(major|breaking)$
    label_pattern_minor: ^(minor|feature)$
```

を追加

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
    - motemen/gobump-github-pull-request:
        github_token: $GITHUB_TOKEN
        label_pattern_major: ^(major|breaking)$
        label_pattern_minor: ^(minor|feature)$
    - script:
        name: go get
        code: |
          go get ./...
    - wercker/gox:
        os: darwin linux windows
        arch: 386 amd64
        output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
        dest: $WERCKER_OUTPUT_DIR/pkg
    - script:
        name: include assets into artifacts
        code: |
          for dir in $WERCKER_OUTPUT_DIR/pkg/*; do
            if [ -d "$dir" ]; then
              cp -R zsh/ "$dir"
              cp ghq.txt "$dir/README.txt"
            fi
          done
    - tcnksm/zip:
        input: $WERCKER_OUTPUT_DIR/pkg
        output: $WERCKER_OUTPUT_DIR/dist
    - script:
        name: set release tag
        code: |
          if [ -n "$GOBUMP_NEW_VERSION" ]; then
            export RELEASE_TAG="v$GOBUMP_NEW_VERSION"
          fi
    - tcnksm/ghr:
        token: $GITHUB_TOKEN
        input: $WERCKER_OUTPUT_DIR/dist
        replace: true
        version: $RELEASE_TAG
        opt: --draft
```

GITHUB_TOKENいれてないから失敗すると思っていたが
これも予想に反して、失敗してしまった。

# GITHUB_TOKEN に適当なものを入れてみる

これも予想に反して成功してしまった

# ここで盛大にやらかしていることにきづく

ここまでは、yamlのbuildの部分しか実行していなかった。。。

ウェブで、deployを追加してビルドしてみたらエラーがでた

```
cp: cannot stat `zsh/': No such file or directory
```

# エラーを修正

いまは、zshというディレクトリはないので、その部分は削った。
さらに、ghq.txtをREADME.txtに置き換えて
適当なREADME.txtをおいてみた

```
box: tcnksm/gox
dev:
  steps:
    - internal/watch:
        code: |
          go build ./...
          ./source
        reload: true
build:
  steps:
    - setup-go-workspace
    - script:
        name: show environments
        code: |
          git version
          go version
    - script:
        name: go get
        code: |
          go get -t ./...
    - script:
        name: go test
        code: |
          go test -v ./...
deploy:
  steps:
    - setup-go-workspace
    - script:
        name: install tools
        code: |
          apt-get update
          apt-get install -y zip
          curl -L http://stedolan.github.io/jq/download/linux64/jq -o /usr/local/bin/jq
          chmod +x /usr/local/bin/jq
    - motemen/gobump-github-pull-request:
        github_token: $GITHUB_TOKEN
        label_pattern_major: ^(major|breaking)$
        label_pattern_minor: ^(minor|feature)$
    - script:
        name: go get
        code: |
          go get ./...
    - wercker/gox:
        os: darwin linux windows
        arch: 386 amd64
        output: '{{.Dir}}_{{.OS}}_{{.Arch}}/{{.Dir}}'
        dest: $WERCKER_OUTPUT_DIR/pkg
    - script:
        name: include assets into artifacts
        code: |
          for dir in $WERCKER_OUTPUT_DIR/pkg/*; do
            if [ -d "$dir" ]; then
              cp helloworld.txt "$dir/README.txt"
            fi
          done
    - tcnksm/zip:
        input: $WERCKER_OUTPUT_DIR/pkg
        output: $WERCKER_OUTPUT_DIR/dist
    - script:
        name: set release tag
        code: |
          if [ -n "$GOBUMP_NEW_VERSION" ]; then
            export RELEASE_TAG="v$GOBUMP_NEW_VERSION"
          fi
    - tcnksm/ghr:
        token: $GITHUB_TOKEN
        input: $WERCKER_OUTPUT_DIR/dist
        replace: true
        version: $RELEASE_TAG
        opt: --draft
```

# 想定したいた感じのエラーでた

releaseはしていないので気になる点ではあるが、
適当なTOKEN("a"一文字)を設定しているので、401なのだろう

```
no version was supplied; using pre-release as version
ghr version v0.2.0, build 4b9b3ea
2016/09/03 18:37:37 Run as DEBUG mode
2016/09/03 18:37:37 token: a
2016/09/03 18:37:37 owner: manabu
2016/09/03 18:37:37 repository: wercker-golang-helloworld-build-cmd
2016/09/03 18:37:37 requestURL: https://api.github.com/repos/manabu/wercker-golang-helloworld-build-cmd/releases
2016/09/03 18:37:37 HttpStatus: 401 Unauthorized
Github returned 401 Unauthorized
```

# GITHUB_TOKENを作る

* [wercker/step-github-create-release: wercker step for deploying to GitHub releases](https://github.com/wercker/step-github-create-release#creating-a-github-token)

ここを参考につくってみた

Settingにいって、
Personal Access Tokenをクリックし
新しい物を作る
このときのスコープは、repo publicだけあればよいみたい。
descriptionになまえをかいて生成する

werckerでは、
buildと、deployの２つパイプラインがあるので、deployの方に
environment で、protected valueにして保存する

# deployできた

releaseタグは打たなかったが無事に、Draftにzipがたくさんできていた





# 参考



* [Go プロジェクトのバージョニングとリリースを CI で自動化する - 詩と創作・思索のひろば](http://motemen.hatenablog.com/entry/2015/08/go-auto-gobump-ci)
* [Werckerの仕組み，独自のboxとstepのつくりかた | SOTA](http://deeeet.com/writing/2014/10/16/wercker/)
* [CI-as-a-ServiceでGo言語プロジェクトの最新ビルドを継続的に提供する | SOTA](http://deeeet.com/writing/2014/10/16/golang-in-ci-as-a-service/)
* [Wercker で Go のプロジェクトをクロスコンパイルし、GitHub にリリースする - 詩と創作・思索のひろば](http://motemen.hatenablog.com/entry/2014/06/27/xcompile-go-and-release-to-github-with-wercker)
* [Deploy golang binaries using wercker, glide and gox](http://www.blang.io/posts/2015-09_wercker_golang_github_release/)
* [Deploying your assets to GitHub Releases](http://blog.wercker.com/2014/05/08/Deploying-assets-to-github-releases.html)
* [tcnksm-sample/wercker-golang: Sample of using wercker step & box for golang](https://github.com/tcnksm-sample/wercker-golang)
* [Wercker を使ってみた - Qiita](http://qiita.com/ngyuki/items/47a66b26e1bbf833e8c8)
* [複数プラットフォームにGo言語のツールを配布する #hikarie_go // Speaker Deck](https://speakerdeck.com/tcnksm/fu-shu-puratutohuomunigoyan-yu-falseturuwopei-bu-suru-number-hikarie-go)
* [wercker/getting-started-golang: A sample application in Go for wercker](https://github.com/wercker/getting-started-golang)

* [tcnksm/wercker-step-ghr: Wercker step for tcnksm/ghr, create Github Release and uploading artifacts](https://github.com/tcnksm/wercker-step-ghr)
* [tcnksm-sample/wercker-golang: Sample of using wercker step & box for golang](https://github.com/tcnksm-sample/wercker-golang)
* [wercker入門 | フリップフラップ](http://blog.flup.jp/2016/02/23/beginning_wercker/)

Travis の例だけど

* [Travis CI でクロス・コンパイル — プログラミング言語 Go | text.Baldanders.info](http://text.baldanders.info/golang/cross-compiling-in-travis-ci/)
