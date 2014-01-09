---
layout: post
title: 手軽にCIを体験してみたい・その2
subtitle: Proactive Web Performance Optimization with Jenkins
cover_image: /2014/01-08-cover.png
categories: performance
excerpt: "前回の記事が全然手軽じゃない気がしてきたので、今回も幾分かマシにCIを体験するという目的で書いてみる。"
---

前回の記事が全然手軽じゃない気がしてきたので、今回も幾分かマシにCIを体験するというというかパフォーマンステストしてみる目的で書いてみる。

![Jenkins・WPT・GitHub](/mol/images/2014/01-08-fig01.png)

前回はTravisとYSlowを使ってパフォーマンステストをしたけど、今回はJenkinsとWebPagetestを使って全く同じことをしてみる。

やっぱしTravisの設定が慣れないんだ。ちなみに普通のユニットテストとかだったら、アクセストークンとか必要ないので軽くできる。僕はGruntのプラグインでやってる。

+ [grunt-csso/.travis.yml](https://github.com/t32k/grunt-csso/blob/master/.travis.yml)
+ [grunt-csso/package.json](https://github.com/t32k/grunt-csso/blob/master/package.json)

例えば、grunt-cssoの設定は上記みたいな感じ。ymlは実行環境指定してあるだけだし、package.jsonは`grunt test`のコマンドを実行してるだけで、要はnodeunitテストだ。ローカルでやるのとたいして変わらない。

なので、おもしろくない。

## Jenkins

やっぱり私、Jenkins触りたいんですですおおおお＾q＾！ってことで、世の中にはクラウドサービスとしてJenkinsを使えるそうで、CloudBeesってとこのDEV@cloud使ってみる。便利な世の中だ。

+ [CloudBees: The Java PaaS Company](http://www.cloudbees.com/)

Freeでは月300分までのビルドまでしかできなかったり制限あるけど、ちょっとJenkinsに触りたいんです欲求ぐらいなら満たせる。

### Jenkinsシステム設定

まず、GitHubとJenkinsの連携だけどDEV@cloudのJenkinsは[Git Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin)がデフォルトでインストールしてあるのでいちいちこちらでインストールしなくてもいいので楽ですね。

__CloudBees DEV@cloud Authorization__でCloudBees Public KeyをGitHubのAccount Settingsの[SSH Keys](https://github.com/settings/ssh)に登録しておく。

![NodeJS](/mol/images/2014/01-08-fig02.png)

次に後述するWebPagetest(WPT)をNode.jsから利用するのでJenkinsにNode.jsをインストールしたい。NodeJS Pluginを検索してインストールすれば、Jenkinsのシステム設定からNode.jsをバージョン管理できるようになる。

+ [NodeJS Plugin - Jenkins - Jenkins Wiki](https://wiki.jenkins-ci.org/display/JENKINS/NodeJS+Plugin)

また`webpagetest`パッケージが必要なので、__Global npm packages to install__からインストールできるようにしておく。


### Jenkinsビルド設定

__新規ジョブ作成__から『フリースタイル・プロジェクトのビルド』を選択する。

__ソースコード管理システム__はGitを選択しレポジトリURLを設定する。ここでは`git@github.com:t32k/maple.git`を指定。

![SCMをポーリング](/mol/images/2014/01-08-fig03.png)

次は__ビルド・トリガ__で、『SCMをポーリング』にチェックを入れ、スケジュールには本来Cronの設定を書くが今回はGitHubのServer Hookをトリガとするので、何も入力しない（便宜上、チェックをいれるらしい）。

![Service Hooks](/mol/images/2014/01-08-fig04.png)

GitHubのMapleのSettingsから__Service Hooks__で、Jenkins (Git plugin)を選択肢、Jenkins Urlを入力し、Activeにする。これでGitフックの設定は終わり。MapeレポジトリにコミットするとJenkinsがビルドする。

ほかにもいろいろ方法があるらしいので下記ページを参照してほしい。

+ [GithubからJenkinsへのServer Hook - Qiita [キータ]](http://qiita.com/mechamogera/items/dbeb3a540f636bfed7af)

次は__ビルド環境__で、Provide Node &amp; npm bin/ folder to PATHにチェックをする。

__ビルド__には『シェルの実行』を選択し、下記のようなコマンドを設定。

```
git checkout gh-pages
git rebase origin/master
git push origin gh-pages
git checkout master
test/test.sh YOUR_PRIVATE_INSTANCE_URL
```

要はmasterの内容をgh-pagesのブランチにマージしてWebPagetestを走らせているのだ。このへんはシェルでどうにでもできるので使い勝手がいい。

![JUnitテスト結果の集計](/mol/images/2014/01-08-fig05.png)

で最後に、__ビルド後の処理__としてJUnitテスト結果の集計を選択して、WebPagetestのテスト結果XMLのファイル名を選択すれば、Jenkinsのひと通りの設定は終わりだ。

## WebPagetest

WebPagetestはこのブログでも何回か紹介しているが、Webパフォーマンスの計測サービスだ。それをNode.jsのラッパーでCLIからテストを実行できるようにしたのが__webpagetest-api__。

+ [marcelduran/webpagetest-api](https://github.com/marcelduran/webpagetest-api)

これを利用するには自分でプライベートインスタンスを作ってそこでテストを実行させるか、パブリックインスタンス上でテストを実行させるかの2つだけど、後者はWPTの作者にメールしてAPIキーをもらわなきゃいけない。

もうこの辺りから全然お手軽でもないんだけども、プライベートインスタンスとか立ち上げるのだるいし（弊社にはあるのでウェーイ♪、今回の例ではAPIキーを利用していない）、とりあえず、Please API Key!ってメール投げてみましょう。1日200回までなら実行可能っぽいす。

+ [how can i get an api key? · Issue #8 · marcelduran/webpagetest-api](https://github.com/marcelduran/webpagetest-api/issues/8)

```
webpagetest test http://t32k.me/maple/test/fixtures/perf_test.html --server $1 --poll 3 --specs test/spec.json --reporter xunit > webpagetest.xml
```

+ [maple/test/test.sh · t32k/maple](https://github.com/t32k/maple/blob/master/test/test.sh)

とりま、このラッパーを使って上記のようなコマンドをシェルファイルとして実行している。今回は`--server $1`でプライベートインスタンスのURLを指定しているけど、みなさんは代わりに`--key $1`でAPIキーを引数でとるようにしてもらえればよいかと思います。

` --poll 3 `は、WPTのテストを実行しただけでは結果がかえってくるまで時間がかかるので3秒ごとにポーリングして結果が帰ってくるまで待ってるって意味。

`--specs test/spec.json`にはどの項目がどの程度のパフォーマンスまで許容できるのかしきい値を書いておく。

MapleのスペックではfistViewでリクエストが50、renderタイムが5000ms、loadTimeが10000msを超えるようであれば失敗とみなしている。ここら辺りは今はちょっと適当にやってるのだけど、YSlowに比べていろんな指標をWPTではチェックできるのでこんな風にしてスペック書くんだよってことを理解してもらえればよいです。

+ [maple/test/spec.json · t32k/maple](https://github.com/t32k/maple/blob/master/test/spec.json)

`reporter xunit > webpagetest.xml` 最後はXML形式でテスト結果を保存するよーって意味です。これをJenkinsに読み取らせて、Jenkins上でテスト結果が確認できるのです。

細かな設定に関してはここをみるとよいです。

+ [Test specs · marcelduran/webpagetest-api Wiki](https://github.com/marcelduran/webpagetest-api/wiki/Test-specs#jenkins-integration)

ほんとは、TAP形式のレポートのほうが見やすくて良いのだけど、CloudBeesのJenkinsにはTAPレポートを表示させるJenkinsプラグインがインストール出来ないからJUnit形式にしている。

![テスト結果](/mol/images/2014/01-08-fig06.png)

で、適当になんかPushしてやると、Jenkinsたんがビルドを走らせて上記のような結果を頂けます。

んなわけでやっぱJenkinsでこれだけいろいろできるのはよいなーと思いました。