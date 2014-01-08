---
layout: post
title: 手軽にCIを体験してみたい・その2
subtitle: Proactive Web Performance Optimization with Jenkins
cover_image: /2014/01-08-cover.png
categories: performance
excerpt: "前回の記事が全然手軽じゃない気がしてきたので、今回も幾分かマシにCIを体験するという目的で書いてみる。"
---
前回の記事が全然手軽じゃない気がしてきたので、今回も幾分かマシにCIを体験するという目的で書いてみる。

![Jenkins・WPT・GitHub](/mol/images/2014/01-08-fig01.png)

前回はTravisとYSlowを使ってパフォーマンステストをしたけど、今回はJenkinsとWebPagetestを使ってみる。

やっぱしTravisの設定が慣れない気がする。ちなみに普通のユニットテストとかだったら、アクセストークンとか必要ないので軽くできる。僕はGruntのプラグインでやってる。

+ [grunt-csso/.travis.yml](https://github.com/t32k/grunt-csso/blob/master/.travis.yml)
+ [grunt-csso/package.json](https://github.com/t32k/grunt-csso/blob/master/package.json)

例えば、grunt-cssoの設定は上記みたいな感じ。ymlは実行環境指定してあるだけだし、package.jsonは`grunt test`のコマンドを実行してるだけで、nodeunitのテストだ。ローカルでやるのとたいして変わらない。

なので、おもしろくない。

## Jenkins

やっぱり私、Jenkins触りたいんです！ってことで、世の中にはクラウドサービスとしてJenkinsを使えるそうで、CloudBeesってとこのDEV@cloud使ってみる。

+ [CloudBees: The Java PaaS Company](http://www.cloudbees.com/)

Freeでは月300分までのビルドまでしかできなかったり制限あるけど、ちょっとJenkinsに触りたいんです欲求ぐらいなら満たせる。

### 設定

まず、GitHubとJenkinsの連携だけどDEV@cloudのJenkinsはGitプラグインがデフォルトでインストールしてあるので楽。CloudBees DEV@cloud AuthorizationでCloudBees Public KeyをGitHubに登録しておく。


次に後述するWebPagetest(WPT)をNode.jsから利用するのでJenkinsにNode.jsをインストールしたい。NodeJS Pluginを検索してインストールすれば、Jenkinsのシステム設定からNode.js管理できる。

+ [NodeJS Plugin - Jenkins - Jenkins Wiki](https://wiki.jenkins-ci.org/display/JENKINS/NodeJS+Plugin)

`webpagetest`のnpmが必要なので、インストールしておく。



## WebPagetest

+ [marcelduran/webpagetest-api](https://github.com/marcelduran/webpagetest-api)


+ [Test specs · marcelduran/webpagetest-api Wiki](https://github.com/marcelduran/webpagetest-api/wiki/Test-specs#jenkins-integration)
