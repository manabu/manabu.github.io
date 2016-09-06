---
layout: post
title: werckerからgithubへ配置するときにバージョンにタグがあるときだけ、replace
date: 2016-09-07T09:21:01
---

# 概要

バージョンを固定したら、上書きはしてほしくないが、
バージョンにタグがあるときだけ、成果物の置き換えを行いたい。
具体的には、以下のような感じ

|version|置き換え|
| --- | --- |
|0.1.4-dev|する|
|0.1.4|しない|




# gobumpでバージョンを取得し、タグが付いてるか調べる

タグがついているときだけ、replaceしたいので、
正規表現で調べることにした。
こんなかんじ、gobumpなどはあらかじめインストールしてあるとする。

```
- script:
    name: get version from gobump
    code: |
      export REPLACEFLAG=true
      export RELEASE_TAG=$(gobump show | jq -r .version)
      if [[ "$RELEASE_TAG" =~ ^[0-9]+\.[0-9]+\.[0-9]+$ ]]; then
        export REPLACEFLAG=false
      fi
```


# 最終的にはこんなかんじなった

バージョンにタグがついてるときだけ
replaceを有効にした。

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
          go get github.com/motemen/gobump/cmd/gobump
    - script:
        name: get version from gobump
        code: |
          export REPLACEFLAG=true
          export RELEASE_TAG=$(gobump show | jq -r .version)
          if [[ "$RELEASE_TAG" =~ ^[0-9]+\.[0-9]+\.[0-9]+$ ]]; then
            export REPLACEFLAG=false
          fi
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
        replace: $REPLACEFLAG
        version: $RELEASE_TAG
```

# 参考

* [wercker-golang-helloworld-build-cmd/wercker.yml at master · manabu/wercker-golang-helloworld-build-cmd](https://github.com/manabu/wercker-golang-helloworld-build-cmd/blob/master/wercker.yml)
