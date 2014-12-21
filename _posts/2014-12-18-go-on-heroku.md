---
layout: post
title: HerokuでGoを動かす
subtitle: Go on Heroku!
categories: develop
excerpt: HerokuでGo Appを動かす
---

[Heroku Advent Calendar 2014 - Qiita](http://qiita.com/advent-calendar/2014/heroku) の23日目です、たぶん。

最近、僕の周りの人らがGO!GO!うるさいので、ついつい僕もそそのかされてGoやりたいなーと思ったのです。

+ [A Tour of Go | Hello, 世界](http://go-tour-jp.appspot.com/#1)

チュートリアルをやってみたんですけど、やっぱりWeb上で動かしたいわけですよ。そうゆうわけで、Heroku上でGoアプリを動かしてみようと思います。

## Go on Heroku

+ [Getting Started with Go on Heroku](https://mmcgrana.github.io/2012/09/getting-started-with-go-on-heroku.html)

まぁ、上記の記事を参考にしたらちゃんとGoアプリをHerokuで稼働させることができました。




+ [kr/heroku-buildpack-go](https://github.com/kr/heroku-buildpack-go)
[Read How Do I Write And Deploy Simple Web Apps With Go? | Leanpub](https://leanpub.com/howdoibuildawebappwithgo/read#leanpub-auto-deploying-go-web-apps-to-heroku)

[Buildpacks | Heroku Dev Center](https://devcenter.heroku.com/articles/buildpacks)

[Go on Heroku](http://go-talks.appspot.com/github.com/freeformz/go-on-heroku/presentation.slide#1)


## hk CLI tool


+ [heroku/hk](https://github.com/heroku/hk)

```sh
$ L=/usr/local/bin/hk && curl -sL -A "`uname -sp`" https://hk.heroku.com/hk.gz | zcat >$L && chmod +x $L
```

