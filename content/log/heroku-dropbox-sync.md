---
date: 2014-12-13
title: Heroku Dropbox Syncで実現するWeb開発の未来
subtitle: Heroku Advent Calendar 2014 - Qita
categories: development
cover_image: /2014/12-13-cover.jpg
excerpt: 2014年11月にHerokuからDropbox Sync機能のアナウンス（Beta版）がありました。今日はこれを使ってみようと思います。
---

[Heroku Advent Calendar 2014](http://qiita.com/advent-calendar/2014/heroku)の13日目の記事です。

2014年11月に[HerokuからDropbox Sync機能のアナウンス（Beta版）](https://blog.heroku.com/archives/2014/11/19/announcing_beta_dropbox_sync)がありました。今日はこれを使ってみようと思います。

<small>この記事はBeta機能について解説しています。機能に関しては変更の可能性があります。</small>

## デザイナーとデプロイ

まず先に私とHerokuと言えば、[StyleStats](http://www.stylestats.org/)というCSS解析ツールをHeroku上で動かしています。私は元はWebデザイナーでしたので、つい最近まで『デプロイ？なにそれ？おいしいの？』って感じでしたが、`git push heroku master`でデプロイできるHerokuさんのおかげで、こんな私でもWebアプリを稼働・運用していけています。

> 配備する、配置する、展開する、配置につく、などの意味を持つ英単語。
ソフトウェアの分野で、開発したソフトウェアを利用できるように実際の運用環境に展開することをデプロイということがある。

+ [デプロイとは 【 deploy 】： IT用語辞典](http://e-words.jp/w/E38387E38397E383ADE382A4.html)

とはいえ、純粋なるWebデザイナーさんがGitコマンドを使いこなし黒い画面から`git push heroku master`とタッターンッ！！と軽快にデプロイする姿を見れるのはまだ先かもしれません。

Herokuにデプロイすることに関して言えば、Gitコマンドを使いこなす必要はなく最低限のコマンドを覚えるだけですし、黒い画面も使わなくてもGUIアプリを使えばよいわけですが、やっぱりGitを使うということには見えない大きな壁があるように個人的には考えています。

そうゆうわけで、Gitを使わないユーザーにもデプロイの手段を提供するのが、今回のDropbox Sync機能です。その名の通り、Dropboxを通して、Web上からデプロイできる機能です。

## Heroku Dropbox Syncの使い方

Dropboxであれば、デザイナーさんもよく使ってますよね、デザインマテリアルの保存とか、それこそDropboxでバージョン管理してたりとか、デザイナーさんにとってDropboxがGitみたいな位置づけかもしれません。

![Heroku Dashboard](/mol/images/2014/12-13-fig01.jpg)  
使い方はすごく簡単です。Herokuアカウントとか基本的なセッティングは終わってる前提で話します。まず、[Heroku Dashboard](https://dashboard.heroku.com/apps)で新規Appを作成して（ここではt32k-drop-sync）、Codeタブを選択してその下部に[Connect to Dropbox]のボタンがありますので、そこをクリックします。

![Authorize](/mol/images/2014/12-13-fig02.jpg)  
Dropboxから確認を求められる画面になるので許可しましょう(Dropboxにログインしてなかったらまずログイン画面がでてきます)。

![Finder](/mol/images/2014/12-13-fig03.jpg)  
許可するとローカルマシンの中に`Dropbox/アプリ/Heoku/t32k-drop-sync/`というフォルダが作成されているのが確認できます。

`アプリ`はローカライズ部分なので、人によっては`Dropbox/Apps/Heroku/{APP-NAME}`って感じのディレクトリになってるかと思います。

あとはここのディレクトリにアプリを作成していくだけです。試しにRailsアプリを作ってみました。

![Deploy](/mol/images/2014/12-13-fig05.png)  
ひととおりの作業が終わったら、またHeroku Dashboardのt32k-drop-syncアプリのCodeタブの下部にデプロイボタンがあります。コミットメッセージを記入します。

![Deploy](/mol/images/2014/12-13-fig04.png)  
うまくいけばこのようにチェックされます。というわけで、Dropbox Syncって名前だけど、Dropboxがファイルを同期するたびにデプロイが実行されるわけじゃないです。ちゃんとWeb UI上からデプロイボタンを押さないといけません。

![Rails new](/mol/images/2014/12-13-fig06.png)  
とりま、できました。


## Heroku Dropbox Syncの使いドコロ

HerokuアプリをGitを使わずにDropbox Syncで作成できましたが、実際のところ、Herokuに新規アプリをデプロイするときにはアプリケーション側でいろいろ設定しなきゃいけないことが多いので、デザイナーがひとりで完遂できるかというと疑問ですが、Dropbox Syncはなにも新規アプリでDropbox Syncを有効にしたアプリだけに適用されるわけではないです。

![2Ways](/mol/images/2014/12-13-fig07.png)

Gitで管理している既存アプリでもDropbox Sync機能を有効にすることができます。使い方は上記と同じです。また、デザイナーが修正したファイルをDropbox Syncからデプロイした場合、Git管理しているエンジニアは次にデプロイしたいときは`git pull heroku master`をしてデザイナーが行った修正の差分をマージしておかなければなりません。その逆にエンジニアが`git push heroku master`でデプロイした場合は自動的にデザイナー側のDropboxが同期します。

極端な話、文言修正だけだったら、iPadにDropboxアプリ入れて、Dropbox連携のテキストエディタで編集して、Safariからデプロイボタン押せばiPadだけでデブロイが可能となります。

まぁそれ自体には意味は無いですけど、デプロイの敷居はだいぶ下がったのではないかなと思います。ちょっとデザイナーさんにバナー差し替えを依頼したいときなど、編集してaddしてcommitしてpushしてもらうより、Dropbox内のファイルいじってもらって、終わったらエンジニア側でデプロイボタン押せば圧倒的に説明コストが低くて済みます。

しかしコミットの粒度を考えると、こまめにGitでコミットしておいたほうがなにかと良いので、Dropbox Sync機能はその点まだクリアできていない問題だけど、非エンジニアのデプロイの敷居を下げるという意味ではすごく良いアプローチだと思うし、それで興味をもった人が今度はGitからデプロイ！って段階が踏めるようになったのは良い流れじゃないかなと個人的には感じます。

そういうわけで、エンジニアとデザイナー仲良くデプロイしていきましょう。

+ __[Dropbox Sync | Heroku Dev Center](https://devcenter.heroku.com/articles/dropbox-sync)__


