---
layout: post
title: GoアプリをHerokuにデプロイする
subtitle: Go on Heroku!
cover_image: /2014/12-23-cover.png
categories: develop
excerpt: Heroku Advent Calendar 2014 - Qiita
---

[Heroku Advent Calendar 2014 - Qiita](http://qiita.com/advent-calendar/2014/heroku) の23日目です、たぶん。

最近、僕の周りの人らがGO!GO!うるさいので、ついつい僕もそそのかされてGo言語やりたいなーと思ったのです。[Go 1.4](https://golang.org/doc/go1.4)も出たしね。

+ [A Tour of Go | Hello, 世界](http://go-tour-jp.appspot.com/#1)

ひととおりチュートリアルはやってみたんですけど、やっぱりWeb上で動かしたいわけですよ。そうゆうわけで、Heroku上でGoアプリを動かしてみようと思います。

## Go on Heroku

+ __[Getting Started with Go on Heroku](https://mmcgrana.github.io/2012/09/getting-started-with-go-on-heroku.html)__

まぁ、上記の記事を参考にしたらちゃんとGoアプリをHerokuで稼働させることができます。以下は自分の備忘録代わりということで。

### Install Go

[goenv](https://bitbucket.org/ymotongpoo/goenv)というGoのバージョン管理ツールもあるみたいだけど、初心者なので[Homebrew](http://brew.sh/)で入れることにする。

```sh
$ brew install go
$ go version
go version go1.3.3 darwin/amd64
```

わーい、かんたん٩(๑❛ᴗ❛๑)۶

### Go Environment

`$GOPATH`等を設定する。ここで指定したパス以下がGoのワークスペースとなる。お好きなシェルプロファイルに記述。

```sh
$ echo 'export GOPATH=$HOME' >> $HOME/.bash_profile
$ echo 'export PATH=$PATH:$GOPATH/bin'  >> $HOME/.bash_profile
```

以下のようなディレクトリ構成で管理される。

```sh
$GOPATH
├── bin（コンパイルしたバイナリファイル）
├── pkg（パッケージオブジェクトファイル）
└── src（Goの作業ソースファイル）
```

GitHub上に置かれているソースファイルは、 `~/src/github.com/{USER_NAME}/{REPOSITORY_NAME}` みたいに管理される。

+ [ghq + peco/percol - Tatsuhiko Miyagawa's blog](http://weblog.bulknews.net/post/89635306479/ghq-peco-percol)
+ [peco、ghq、gh-openの組み合わせが捗る - Webtech Walker](http://webtech-walker.com/archive/2014/06/peco-ghq-gh-open.html)

だもんでghqの方もそっち合わせてpecoとか使うと捗るらしいよ。

```sh
git config --global ghq.root ~/src
```

ghqでgetしてきたリポジトリの保存先の設定。

+ [motemen/ghq](https://github.com/motemen/ghq)（Go言語製、リポジトリ管理ツール）
+ [peco/peco](https://github.com/peco/peco)（Go言語製、フィルタリングツール）
+ [typester/gh-open](https://github.com/typester/gh-open)（Go言語製、GitHubのレポジトリURLを開くツール）

まとめると、上みたいな感じ。世の中便利ですな。

ちなみに、Intellij IDEAでGolangのプラグイン（0.9.15）を入れると、ちゃんと指定しているのにもかかわらず、$GOROOTと$GOPATH設定しろや、(ﾟДﾟ)ｺﾞﾙｧ!!って言われるけど、0.9.16-alpha入れると治った٩(๑❛ᴗ❛๑)۶

+ [Releases · go-lang-plugin-org/go-lang-idea-plugin](https://github.com/go-lang-plugin-org/go-lang-idea-plugin/releases)

んで、$GOROOTは設定しなくてもいいらしい。

+ [あなたがGOROOTを本当に設定しなくていい理由 | Androg](http://kwmt27.net/index.php/2013/06/14/you-dont-need-to-set-goroot-really/)

### Go Web App

話が逸れたので戻すと`~/src/demoapp`のディレクトリを作ってそこで作業する。

```sh
$ mkdir $GOPATH/src/demoapp
$ cd $GOPATH/src/demoapp
```

`web.go`のファイルを作成する。

```go
// web.go
package main

import (
    "fmt"
    "net/http"
    "os"
)

func main() {
    http.HandleFunc("/", hello)
    fmt.Println("listening...")
    err := http.ListenAndServe(":"+os.Getenv("PORT"), nil)
    if err != nil {
      panic(err)
    }
}

func hello(res http.ResponseWriter, req *http.Request) {
    fmt.Fprintln(res, "hello, world")
}
```

んで、`go get`（コンパイル、インストール）して、demoappをバイナリで動かすようにする。


```sh
$ PORT=5000 demoapp
$ open http://localhost:5000/
```

ローカル環境で動いてることを確認する。

### Heroku Setup

`heroku login`とかしとく。

```sh
$ echo 'web: demoapp' > Procfile
```
Procfileを作る。

```sh
$ go get github.com/kr/godep
```

Godepという依存性の管理ツールをインスコ。


```sh
$ godep save
```

依存性を保存。


```sh
$ heroku create --buildpack https://github.com/kr/heroku-buildpack-go.git
```

+ [kr/heroku-buildpack-go](https://github.com/kr/heroku-buildpack-go)

GoのHeroku Buildpackを使ってHerokuアプリを作成する。ちなみに、BuildpackとはHeroku上でアプリをコンパイルするためのスクリプトで、Goなどのデフォルトで対応していない言語は[Third-PartyのBuildpack](https://devcenter.heroku.com/articles/third-party-buildpacks)を使ってデプロイすることになる。だもんで、Go言語以外も動かせる。

Buildpackを使ってアプリで来たら、`git push heroku master`してデプロイして完了！

わーい、できたー٩(๑❛ᴗ❛๑)۶

## A fast Heroku CLI client

ちなみに、Go言語製のCLIツールが多いのにお気づきだろうか。なんか速いらしいね。ってことで、`heroku`コマンドも`hk`というGoで作らたコマンドがある。

+ [heroku/hk](https://github.com/heroku/hk)

まだBeta版でherokuにあってhkに無いコマンドもありますが。

```sh
$ L=/usr/local/bin/hk && curl -sL -A "`uname -sp`" https://hk.heroku.com/hk.gz | zcat >$L && chmod +x $L
```

インスコ。

```sh
t32k at MBP in ~
$ time heroku apps >/dev/null
real	0m1.980s
user	0m0.711s
sys	0m0.064s

t32k at MBP in ~
$ time hk apps >/dev/null
real	0m0.724s
user	0m0.076s
sys	0m0.019s
```

おぉー、桁が違うぜ！ってことで、速いもの好きなあなたはインストールしてみてはどうでしょうか。

僕もGoで作ったCLIツール作りたい٩(๑❛ᴗ❛๑)۶
