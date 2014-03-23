---
layout: post
title: バッジ駆動開発（2014:Node.js）
subtitle: Readmeをバッジで飾ろう！
cover_image: /2014/03-24-cover.jpg
categories: blog
excerpt: "みんな、バッジ好き？バッジ！バッジ！バッジ！"
---

こんちわ！@t32kだよ。

みんな、バッジ好き？バッジ！バッジ！バッジ！小学生の頃、自由勉強ノートってのがあって、勉強したページ分、先生からシールをもらったのは良い思い出です。あのノスタルジーをもう一度！

ということで、大人の自由勉強ノートといえばGitHubレポジトリですな。OSSがんばります！私、気になります！そしたら、シール欲しいじゃないですか？

あるよ、シールあるよ、シール的なバッジだけど。

[![](/mol/images/2014/03-24-fig01.png)](https://github.com/t32k/stylestats)

上記は最近作ってる[StyleStats](https://github.com/t32k/stylestats)のReadmeだけど、なんか緑のバッジいっぱいですよね。それを説明していく！

## Travis-CI Status Images

![](/mol/images/2014/03-24-fig02.png)

+ [Travis CI: Status Images](http://docs.travis-ci.com/user/status-images/)

まずは、この中のバッジの中では一番有名じゃないだろうか、Travisの Status Images。昔、@kyo_agoさんが『テストもしてないプラグインなんて怖くて使えませんよね！』と言ってたのを聞いて、その日のうちにとりあえずテスト書いて、テストしてるよって意味で載っけた思い出深いバッジです。

Travis-CIでビルドがコケてるかどうか、要はテストが失敗してるかどうか、このバッジが赤いままだと、恥ずかしくておめおめ出社もできません。

## Version Badge

![](/mol/images/2014/03-24-fig03.png)

+ [Version Badge for your RubyGems, PyPI packages, and NPM modules](http://badge.fury.io/for/js/stylestats)

次によく見かける、バージョンバッジ。gem, PyPI, NPMに登録してあるモジュールなら、サイトから検索してスニペット取得するだけ。

よく使っているモジュールの最新バージョンはいくつだろう？と思ってpackage.jsonとか見たりするけど、このバッジが貼ってあると分かりやすくてよい。あと、NPMに登録してある＝野良モジュールじゃない、ってことでそれなりに、信用度があがる（なんでもNPMに登録できるからあんまり意味ない）かもしれない。

## David

![](/mol/images/2014/03-24-fig04.jpg)

+ [David, a dependency management tool for Node.js projects](https://david-dm.org/)

これもバージョン関係だけど、依存しているモジュールのバージョンが最新かどうかチェックしてくれるサービス。

+ [Dependency status for t32k - stylestats 2.3.0](https://david-dm.org/t32k/stylestats#info=dependencies&view=table)

こんな感じで`dependencies`と`devDependencies`が最新かどうかチェックしてくれる。

まぁ安定して動いてくれてるならそのバージョンが古くても問題ないけど、やっぱり最新がいいよね！僕は新しいもの好きです！！

+ 参考: [Node.jsの開発を超速化するGitHub連携 三種の神器 - teppeis blog](http://teppeis.hatenablog.com/entry/2013/12/node-github)

## Code Climate

![](/mol/images/2014/03-24-fig05.jpg)

+ [Code Climate. Hosted static analysis for Ruby and JavaScript source code.](https://codeclimate.com/)

元は、Ruby専用のコード品質チェックサービスだったけど、最近(?)Node.jsも対応してたみたいだから早速導入してみた。

[GPA(Grade Point Average)](http://ja.wikipedia.org/wiki/GPA)って指標で、4ポイントが一番良いらしい。オープンリポジトリなら無料で利用できるからみんなも見てみよう。

+ [Feed - Code Climate](https://codeclimate.com/github/t32k/stylestats)

最初にやってみたら0.何ポイントとかで、マジ焦って、改善したのは良い思い出です。いろいろおもしろいので個人的にこれはおすすめ。あと、最近使っている[Slack](https://slack.com/)(チャットサービス)と連携できてGPAが上がった下がったの通知もしてくれるのもナイス♪

+ 参考: [Travis CIとCoverallsとCode Climateを使ってGitHubリポジトリにバッジを付ける - アインシュタインの電話番号](http://blog.ruedap.com/2013/09/02/travis-ci-coveralls-code-climate-github-badge)

## Coveralls

![](/mol/images/2014/03-24-fig06.png)

+ [Your Repositories | Coveralls - Test Coverage History & Statistics](http://coveralls.io/)

テストのカバレッジ（網羅率）を表示してくれるサービス。Travis-CI Status Imagesでpassedが出てても、極端な話、どんなテストでいいので、公開してるコードと関係ない単純なテストでも通ってれば、緑色のバッジを表示させることが出来る。

それじゃあんましなので、ちゃんとすべてのコードを網羅してるかどうかカバレッジを確認する必要がある。カバレッジ自体はローカルでもカバレッジを測定するツールを使えば確認できるけど(僕はMocha + Istanbulで取ってる)、それ公開するためのプラットフォームのCoverallsがあることで、テストの信用性をほかのユーザーも簡単に確認できるのは良い。

最初にカバレッジを確認すると90%くらいで、もうちょっと上げる過程で、やっぱりテスト通ってないとこでバグを発見したのでカバレッジ取っててよかった。

+ 参考: [JavaScript coverage with Istanbul and Coveralls via Travis CI | Craig Cook's Blog](http://boycook.wordpress.com/2013/09/17/javascript-coverage-with-istanbul-and-coveralls-via-travis-ci/)

## まとめ

そんなわけで、グリーンだよ！いいんだよ！ってことで、やっぱり赤色のバッジをReadmeに貼ってあるのはカッコ悪い。そこで、緑にしよう！もっといいポイントにしよう！ってモチベーションが湧いて、よりよい開発ができるのは良いと思う。

また、Readmeとかで懇切丁寧な英語で解説できない分、緑色のBadgeを貼ってあるだけでも信用性を担保できるのかなと思って最近頑張ってたって話。

