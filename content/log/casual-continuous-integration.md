---
date: 2014-01-07
title: 手軽にCIを体験してみたい
subtitle: Proactive Web Performance Optimization with Travis-CI
cover_image: /2014/01-07-cover.jpg
categories: performance
excerpt: "昨年のFrontrend/06では、全くもってながら個人的な趣向のもと継続インテグレーションをテーマに開催したんだけど..."
---

昨年の[Frontrend/06](http://frontrend.github.io/events/06/)では、全くもってながら個人的な趣向のもと継続インテグレーション（CI:Continuous Integration）をテーマに開催した。もはや、フロントエンドとは！という感じだが、非常に良いイベントだったと思う。

基本的に昨今のフロントエンドは膨大なタスクに追われている、そのようなタスクを手動でちまちまやっていては手戻りやミスなど必ず発生するので自動化すべきである。フロントエンドの自動化は[Grunt](/mol/log/modern-development-workflow-with-grunt/)などがあるが、結局フロントだけで問題を解決しようとすると問題（限界）があったりするので、CIサーバーとか使ったほうがいいよね。てかフロントエンドの人も慣れておいたほうがいいよねって話。

しかし、フロントエンドの人が[いちからJenkinsを立ち上げたり](/mol/log/vagrant1-2-centos6-4-jenkins1-5/)するのもさほど面倒でもないが多少の心理的障壁があるので、もっとカジュアルに利用したい。

![Build・Test・Commit](/mol/images/2014/01-07-fig01.png)

[Frontend/06の佐竹さんのセッション](http://www.slideshare.net/st44100/ss-28353683)でCIを構成する要素として、Build・Test・Commitの3つがあると紹介されていた。Commitは普段Gitを使ってるから馴染み深いというかGitHub使ってるよね？みんな！！ってことで問題無いとして、Build/TestをなんとかCIサーバーでやってもらいたい。Testに関してはJavaScriptのTestなんかフロントエンドの人もやるので問題ないかと思うけど僕はそんなJavaScriptとか書かないのでよくわからないので、今回はWeb Performanceのテストをやってみるよ。

![Travis・YSlow・GitHub](/mol/images/2014/01-07-fig02.png)

今回のGitHubのレポジトリ(master)にPushしたら、Travisがgh-pagesブランチに同じ内容をコミットして反映された(gh-pagesの)ページのパフォーマンスをYSlowで検証してみるという流れだ。

gh-pagesをDev環境と見立てて、Dev環境でBuildした内容がパフォーマンス的に不適切（テストが失敗）ならProduction環境にはリリースできない・させないというようなサイクルを想定している。

## Travis-CI

CIサーバーはなにもJenkinsだけではない。GitHub上でレポジトリを管理しているのなら連携している[Travis-CI](https://travis-ci.org/)を使用するのが何かと都合がよい。

Travisを使うにはアカウントを連携して、自分の[プロフィール](https://travis-ci.org/profile)から検証したいレポジトリを`ON`にする。


Travisをどのように使用するかは`.travis.yml`というファイルに記述する。Mapleでの設定は下記ファイルを見てもらえればよい。

+ [maple/.travis.yml at master · t32k/maple](https://github.com/t32k/maple/blob/master/.travis.yml)


```
language: node_js
node_js: 0.10
```
最初の行は実行環境を指定する。node.jsを使ったテストがしたいので、`node_js`を指定する。バージョンは0.8、0.10とか複数指定できる。

```
env:
  global:
<<<<<<< HEAD
    - GIT_AUTHOR_NAME=YOUR_ID
    - GIT_AUTHOR_EMAIL=YOUR_MAIL_ADDRESS
    - GIT_COMMITTER_NAME=YOUR_ID
    - GIT_COMMITTER_EMAIL=YOUR_MAIL_ADDRESS
=======
    - GIT_AUTHOR_NAME=your-name
    - GIT_AUTHOR_EMAIL=your-mail
    - GIT_COMMITTER_NAME=your-name
    - GIT_COMMITTER_EMAIL=your-mail
>>>>>>> bc00bb731570eceb7f151001eafb282b7ce2fe56
    - secure: "Xtk................"
```

TravisからGitHubにコミットするには、OAuth access tokensが必要になので[ここから発行する](https://github.com/settings/applications)。そんでトークンをこんなパブリックなところに公開できないので、コマンドラインの`travis`で暗号化したのが`secure`のところ。

```
$ gem install travis
$ travis encrypt -r t32k/maple "GH_TOKEN=<生成したトークン>"
```

こんな感じで暗号化する。詳しくは下記のサイトを参照して欲しい。

+ [Middleman で作った web サイトを Travis + GitHub pages でお手軽に運用する - tricknotesのぼうけんのしょ](http://tricknotes.hateblo.jp/entry/2013/06/17/020229)
+ [MiddlemanとTravis CIでgh-pagesを運用したら身長が伸びた | 1000ch.net](http://1000ch.net/2013/08/30/MiddlemanAndGruntOnTravis/)

まぁ、GitHubの設定をしてるとこです。

```
before_script:
  - "git clone --quiet https://github.com/t32k/maple.git"
  - "git checkout -b gh-pages"
  - "git rebase master"
  - "[ \"$TRAVIS_BRANCH\" == \"master\" ] && [ $GH_TOKEN ] && git push --quiet https://$GH_TOKEN@github.com/t32k/maple.git gh-pages 2> /dev/null"
```

`before_script`はtestが実行する前に実行しておきたいコマンドで、ここでは、masterブランチの内容をgh-pagesにマージしてプッシュしてる。

```
script:
  - "npm test"
```

で、最後にテストコマンドを実行って流れ。


## YSlow

で、次はパフォーマンスのテスト内容に関して。[YSlow](http://yslow.org/)はFirefoxとかChromeの拡張機能でみんな使ったことあるよね？君のサイトはパフォーマンス的にAランクですよ！とか教えてくれるツール。それをPhantom.jsを使ってTravis上でも実行できるように解説してるのが以下のページ。

+ [YSlow - Official Open Source Project Website](http://yslow.org/phantomjs/#travisci-integration)

基本的にこの通りにやっていく。さっきの`.travis.yml`で指定した`npm test`ってのは`package.json`
の以下の部分が実行されるということ。

+ [maple/package.json at master · t32k/maple](https://github.com/t32k/maple/blob/master/package.json#L15)

で、`yslow.sh`を実行するって書いてあるから、yslow.shのファイルは以下。

+ [maple/test/yslow.sh at master · t32k/maple](https://github.com/t32k/maple/blob/master/test/yslow.sh)


```
./node_modules/phantomjs/bin/phantomjs test/yslow.js --info grade --format tap --threshold '{"ycdn": 10, "yexpires": 10}' t32k.me/maple/test/fixtures/perf_test.html?${CACHE_CLEAR}
```

長ったらしく書いてあってややこいけど、基本的には以下のような構造になってる。

```
phantomjs yslow.js [オプション] <テストしたいURL>
```

で、重要なオプションである、しきい値の設定も忘れずに。

```
--threshold '{"ycdn": 10, "yexpires": 10}'
```

単純にテストしたいだけなので『CDN使えよ！』の項目や、gh-pagesでホストしてるのでサーバーの設定とかできないので、キャッシュの項目とか10点でもOKなように（テストが通るように）しておく（もちろん、その他の項目がダメならテストが失敗したよってメールが飛んでくる（飛んでこないようにも設定できる））。

てな感じで、これでmasterにpushするとその内容をgh-pagesにマージしてホストされたURLをパフォーマンステストするって流れが出来ました。

+ [Travis CI - Free Hosted Continuous Integration Platform for the Open Source Community](https://travis-ci.org/t32k/maple)

まぁ今回のテストページとか適当だし、そもそもgh-pagesのホストにデプロイしてる間にtestが実行されちゃって残念な状態にもなってるのであれですけど、雰囲気つかんで貰えれば幸いっす＞ｍ＜

### 参考リソース

+ [Performance Calendar » Proactive Web Performance Optimization](http://calendar.perfplanet.com/2012/proactive-web-performance-optimization/)
