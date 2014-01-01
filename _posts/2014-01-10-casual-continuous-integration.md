---
layout: post
title: 手軽にCIを体験してみたい
subtitle: Proactive Web Performance Optimization
categories: performance
status: true
excerpt: "昨年のFrontrend/06では、全くもってながら個人的な趣向のもと継続インテグレーションをテーマに開催した"
---
昨年の[Frontrend/06](http://frontrend.github.io/events/06/)では、全くもってながら個人的な趣向のもと継続インテグレーション（CI:Continuous Integration）をテーマに開催した。もはや、フロントエンドとは！という感じだが、非常に良いイベントになったと思う。

基本的に昨今のフロントエンドは膨大なタスクに追われている、そのようなタスクを手動でちまちまやっていては手戻りやミスなど必ず発生するので自動化すべきである。フロントエンドの自動化はGruntなどがあるが、結局フロントだけで問題を解決しようとすると問題（限界）があったりするので、CIサーバーとか使ったほうがいいよね。てかフロントエンドの人も慣れておいたほうがいいよねって話。

しかし、フロントエンドの人がいちからJenkinsを立ち上げたりするのもさほど面倒でもないが多少の心理的障壁があるので、もっとカジュアルに利用したい。


Frontend/06の佐竹さんのセッションでCIを構成する要素として、Build・Test・Commitの3つがあると紹介されていた。Commitは普段Gitを使ってるから馴染み深いというかGitHub使ってるよね？みんな！！ってことで問題無いとして、Build/TestをなんとかCIサーバーでやってもらいたい。Testに関してはJavaScriptのTestなんかフロントエンドの人もやるので問題ないかと思うけど僕はそんなJavaScriptとか書かないのでよくわからないので、今回はWebPerfomrnaceのテストをやってみるよ。


今回のGitHubのレポジトリにPushしたら、Travisがgh-pagesブランチに同じ内容をコミットして反映された(gh-pagesの)ページのパフォーマンスをYSlowでテストしてみる。

gh-pagesをDevelopment環境と見立てて、Dev環境でBuildした内容がパフォーマンス的に不適切（テストが失敗）ならProduction環境にはリリースできないというようなサイクルを想定している。

## Travis-CI

CIサーバーはなにもJenkinsだけではない。GitHub上でレポジトリを管理しているのなら連携しているTravis-CIを使用するのが何かと都合がよい。



## YSlow

