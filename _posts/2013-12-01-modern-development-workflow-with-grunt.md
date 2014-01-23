---
layout: post
title: 今どきのGruntを使ったフロントエンド開発（HTML/CSS編）
subtitle: HTML5 Conference 2013
categories: blog
status: true
excerpt: "あらゆる作業をGruntに任せてより効率的な開発環境を手に入れてみませんか"
---
<script async class="speakerdeck-embed" data-id="57a669003bb9013102323286f532ced0" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

SassなどのCSSプリプロセッサを使うWebデザイナが増えてきました。Sassをコンパイルするだけなら黒い画面（ターミナル）を使わずともGUIアプリからの利用で問題ありません。が、ここは一歩踏み込んでGrunt（JavaScript製のタスクランナー）を使って、Sass以外のコンパイルやライブリロード、画像最適化、CSSのリントやスタイルガイド生成など、あらゆる作業をGruntに任せてより効率的な開発環境を手に入れてみませんか。

---

ども、Front-end Developerをしております[@t32k](https://twitter.com/t32k)です。今日はがんばります。

[Frontrend](http://frontrend.github.io/)というコミュニティ活動をしています。通常は東京で3~4ヶ月の周期でフロントエンドをテーマにした勉強会を開催しています。良かったらみなさんもご参加くださいませ。

## Agenda

今日の話す内容は以下のとおりです。

+ なぜGruntを使うの？
+ Gruntの使い方
+ Gruntfileをカスタマイズしてみましょう

ちなみに今日の話のターゲットはGruntを使ったことのないHTML/CSSコーダーやWebデザイナーさんです。私自身、元Webデザイナーなので僕もできたことは皆さんもできるかと思います。

## Why use Grunt?


+ __[Grunt: The JavaScript Task Runner](http://gruntjs.com/)__

まず、Gruntはなんでしょうか。公式サイトを見てみると__JavaScript Task Runner__と書いています。JavaScriptでTask（あなたがしてほしい処理）をしてくれるRunner（実行してくれるもの）といった意味です。

Gruntの使い方としてはこのように黒い画面に`grunt`といったコマンド名を打つことで使います。

### Complexity

私達はWeb __ドキュメント__ を作っているわけではない。Web __アプリケーション__ を作っている。そのため以前よりもましてWeb制作は複雑性を増している。 

#### GUI Apps

+ [CodeKit — THE Mac App For Web Developers](http://incident57.com/codekit/)
+ [Koala - a gui application for LESS, Sass, Compass and CoffeeScript compilation.](http://koala-app.com/)
+ [Prepros :: Compile Sass, less or any preprocessing language](http://alphapixels.com/prepros/)

Sassとかのコンパイルや画像最適化処理などであったら、別に黒い画面(Grunt)を使わなくても上記のようなGUIアプリを使うことができます。デザイナーにとっては分かりやすいかもしれないGUIアプリですが、エンジニアさんが『ちょっとSass修正したいんだけど。。。』って言われた時に、これらのGUIアプリの使い方を説明するにあたって『ここのボタンを押して、ここのメニューからhogeを選択して、、、』といったまどろっこしい説明をしなければなりません。Gruntであれば後述するPackage.jsonとGruntfile.jsを渡して、任意のGruntタスクコマンドを打つだけです。

またカスタマイズ性においても、私達は唯一無二のWebアプリケーションを制作しているわけですから、当然、最大公約数をターゲットとしているGUIアプリでは都合が悪い時があります（ウチの開発環境ではこれが使えない、これしたいんだけど負の遺産が。など）。そんな時はGUIアプリではその機能や設定が実装されるまで指を加えて待たないといけません。しかし、Gruntなら、タスクを組み合わせたりすることで、ある程度柔軟に対応することができます。

余談ですが、弊社でGitHub Enterpriseを導入した時に私は『やったーこれでGitが使えるお！』と思い、喜び勇んで[Tower](http://www.git-tower.com/)というGUIのGitクライアントアプリ購入しました。それでエンジニアさんにTowerのGit設定をやってもらおうと思ったのですが、『いや俺、Towerの使い方わかんねーし、コマンドラインなら教えますよ』って言われたので、僕はコマンドラインでGit使ってます(ヽ´ω`)

#### Paid Apps

また、これらのアプリの中には有料のものもあります。現在有料じゃなくても将来有料になるかもしれませんし、より良いサービスを受けようとおもうと有料プランを選択肢なければならないかもしれません。良いアプリにお金を払うこと自体、とても素晴らしいことだと思います。しかし、例えばさっきの例でエンジニア：『Sassコンパイルしたいんだけど』、デザイナー：『有料アプリ買ってね！』って言うのはなんか違うかと思います。Gruntなら各種プラグインは基本的に無料です。

### Web Performance

+ [High Performance Web Sites](http://stevesouders.com/hpws/rules.php)

またWebパフォーマンスの観点から見れば、2007年にSteve Soudersが『[ハイパフォーマンスWebサイト](http://www.oreilly.co.jp/books/9784873113616/)』の著書で初めてフロントエンドのパフォーマンスの重要性について説きました。その当時は高速サイトの14のルールという基本的なルールさえ守れば、だいたい問題ありませんでした。

時は経ち、2013年、[#perfmatters](https://twitter.com/search?q=%23perfmatters&src=hash)の大号令を気に、Webパフォーマンスと言っても、__Network__、__Render__、__Compute__の3つの分野に分類され、それぞれの分野ごとに本が出るほど、対応する対策というのは複雑、高度化してきました。

+ [High Performance Browser Networking](http://chimera.labs.oreilly.com/books/1230000000545)
+ [O'Reilly Japan - ハイパフォーマンスJavaScript](http://www.oreilly.co.jp/books/9784873114903/)

__Render__は同僚の[ahomuさんの資料](https://speakerdeck.com/ahomu/web-frontend-rendering-performance-knowledge-and-tips)が一番まとまっているかと思います。

そんなわけで、フロントエンド(HTML/CSS)に関しても、画像の最適化、効率的なスタイルシートの管理、縮小化など対応すべきタスクは多くなってきています。これらの作業を一つ一つ手作業でやっていては抜けなどもありまうすし、面倒です。こういったものはGruntに任せ自動化すべきです。


## How to use Grunt

次は使い方です。まずは、__[node.js](http://nodejs.org/)__をインストールしましょう。公式サイトにはインストーラーが配布されているのでポチポチとボタンを押していくだけでインストールできます。Node.jsをインストールすると同時にNPM(Node Package Module)というパッケージ管理ツールも一緒にインストールされます。

```
$ npm install grunt-cli -g
```

なので、このコマンドの意味はnpmでinstallします、grunt-cliを。グローバルで。って意味です。grunt-cliってのgruntをCommandline Interfaceから使えるようにするパッケージで、グローバルと言うのはどのディレクトリにいても`grunt`のコマンドを使えるようにするという意味で、これがなけばローカルです。

### Structure

これで下準備は整いました。つぎにGruntの構成ですが__Package.json__と__Gruntfile.js__(coffeescriptでも可)の2種類のファイルが必要です。

試しに、[grunt-csso](https://npmjs.org/package/grunt-csso)をというCSSを圧縮してくるれるGruntプラグインを使用できるところまで解説していきましょう。

#### Package.json

+ [Package.json](https://npmjs.org/doc/json.html)

```
$ npm init
```
Package.jsonを作るには、上記のようなコマンドを打ちます。そうすると対話形式でいろいろ黒い画面が訪ねてきますので、適当にYESもしくはENTERキーを押し続けます。そうするとPackage.jsonのひな形が作成されます。

```
$ npm install grunt --save-dev
$ npm install grunt-csso --save-dev
```
次にローカルモジュールのインストールをしていきます。先ほどのgrunt-cliはあくまでコマンドラインからgruntを利用するためだけのパッケージなので、ここでインストールするgruntが実質のパッケージです。このような仕組みになっているので、現在gruntはv0.4ですが、grunt v0.5のバージョンが出てきた時にプロジェクトごとに違うバージョンのgruntを共存することができます。

`--save-dev`というオプションは、パッケージをインストールする際にPackage.jsonに`devDependency`を追記してくれるものです。このように自分の使っているパッケージを記録しておくことで、Aさんが作ったPackage.jsonをBさんに渡して、Bさんが`npm install`することで、Aさんと同じパッケージを一度でインストールすることができます。

### Gruntfile

+ [Sample Gruntfile - Grunt: The JavaScript Task Runner](http://gruntjs.com/sample-gruntfile)


```
$ npm install grunt-init -g
$ git clone https://github.com/gruntjs/grunt-init-gruntfile.git ~/.grunt-init/gruntfile
$ grunt-init gruntfile
```

次にGruntfileの作成ですが、少々面倒です。まず`grunt-init`というプラグインをインストールする必要があります。そして、gruntfileを作るためのテンプレートを`git clone`でダウンロードしてきます。そうすることで`grunt-init gruntfile`を打つとまた`npm init`のようにいろいろ黒い画面が問いてきますが、とりあえずはENTER押しておきましょう。

こうすることで、Gruntfileが作成されます。なんかいろいろ黒い画面いっぱいで面倒だなと思った方は、最初の内は同じようなことをしているGruntfileをGitHubで見つけてコピペして作れば問題無いです。


```js
// Load the task:
grunt.loadNpmTasks('grunt-csso');
```

Gruntfileの中身はいろいろ書かかれていますが、大事なのは3つの部分です。最初にnpm installしたパッケージを読み込む記述です。これがないと`csso`のタスクが使えません。


```js
// Configure the task:
grunt.initConfig({
  csso: {
    dist: {
      files: {
        'output.css': ['input.css']
      }
    }
  },
  foo: { //....}
});
```

次がGruntファイルのメインとなる部分のタスクの設定の部分です。`initConfig`配下にタスクを記述していきます。`dist`の部分はターゲットを表します。この部分の名前は別になんでも構いません。例えばプロダクション環境とディベロプメント環境で圧縮するファイルが違うのなら`prod:`や`dev:`といった名前をつけ、`grunt csso:prod`や`grunt csso:dev`とコマンドを打てば、実行したいタスクを分離できます。`grunt csso`と打つとprodとdev両方のタスクが実行されます。そしてdistの下の階層には大抵処理したいファイルのインプットと処理したあとのファイルのアウトプット先、あと必要であればプラグインのオプションを記述しまうす。

これらが基本的なタスクの設定で、この粒度でタスクをどんどん追加していきます。

```js
// Register the task:
grunt.registerTask('default', ['csso']);
```

最後にカスタムタスクを登録します。`default`を文字通りデフォルトでこの文字列で指定したタスクは`grunt`だけで実行できます。`grunt.registerTask('foo', ['csso']);`とすれば、`grunt foo`でcssoタスクを実行できます。もちろん、CSSの縮小化、JSの縮小化、画像の最適化などの複数のタスクをまとめて任意のタスク名と登録することもできるので、かっこいタスク名考えときましょう。グラント・ティロ・フィナーレ！！！！！

## Customize your Gruntfile!

+ [Plugins - Grunt: The JavaScript Task Runner](http://gruntjs.com/plugins)

さて基本的なGruntの使い方はわかったので、今度は自分好みのGruntfileにしていきましょう。あなたが『こうゆうのあったら便利だなー』って思うプラグインはたいてい公式サイトのプラグインを検索すれば見つかることでしょう。それほどGruntのエコステムは巨大なものとなっています。

また、同じような機能を提供するプラグインが2つ合った場合は基本的には`grunt-contirb-***`の名前がついたプラグインを選択すれば問題ないです。これはGruntjsチームが公式にメンテナンスしているプラグインという証なので。


```
$ npm install grunt-init -g
$ git clone https://github.com/gruntjs/grunt-init-gruntplugin.git ~/.grunt-init/gruntplugin
$ grunt-init gruntplugin
```

また、もし自分のほしいプラグインが見つからなかったら自分で作っちゃいましょう。先ほどの`grunt-init`でもgruntpluginのひな形を作ってくれるのでがんばってみましょう。

私もあまりJavaScriptは書かないのですが、なぜかgruntプラグインをちょこちょこ書いてますので、良かったら使ってみてください。

+ [t32k:npmjs](https://npmjs.org/~t32k)

### Maple 

+ __[t32k/maple](https://github.com/t32k/maple)__

さて最後は僕のGruntfileの設定を紹介しておきます。この一年スマホのWebアプリを制作してきてた集大成をCSSフレームワーク:Mapleとして公開しています。CSSフレームワークといいながら今は全然CSSの部分作ってないですが、ベターなHTML/CSSを書く、パフォーマンス性の高いアプリを作成するために必要なGrunt設定ある程度できていますのでぜひ参考にしてみてください。

+ [maple/Gruntfile.coffee at master · t32k/maple](https://github.com/t32k/maple/blob/master/Gruntfile.coffee)

基本的なことはコード読めば分かるかと思います。MapleのGruntfileはCoffeeScriptで書いてあります。っていいても全然CoffeeScript分かんないですけど、Gruntfileってほぼ設定ファイルのようなものなので、コーフィーで書いたほうがシンプルで見やすいかなと思ってます。


 + __default__: ['develop']
 + __develop__: ['connect', 'watch']
 + __stylesheet__: ['sass', 'autoprefixer', 'csscomb', 'csslint']
 + __typeset__: ['webfont', 'stylesheet']
 + __publish__: ['stylesheet', 'kss']
 + __build__: ['stylesheet', 'csso', 'imageoptim']

タスクの設定の詳しいことは過去のブログ読んで下さいまし！

+ [CSScomb — MOL](/mol/log/csscomb/)
+ [CSSOとGRUNT-CSSO — MOL](/mol/log/csso-and-grunt-csso/)
+ [部屋とYシャツと私 — MOL](/mol/log/good-bye-compass-good-bye-ruby/)
+ [【CSS Sprite編】スプライト地獄からの解放 — MOL](/mol/log/reduce-http-requests-css-sprite/)
+ [【WebFont編】ドラッグ＆ドロップでウェ～イ — MOL](/mol/log/reduce-http-requests-webfont/)
+ [grunt-initとYeoman — MOL](/mol/log/grunt-init-yo/)


### Jet Start

+ [Yeoman - Modern workflows for modern webapps](http://yeoman.io/)

で、ここまでいろいろ説明してきて頭がパンクされた方！大丈夫です！そんな方のために最速でGruntを動かす（Mapleプロジェクトを動かす）ためのコマンドを用意しました。

<iframe width="560" height="315" src="//www.youtube.com/embed/U26K5NXvRxc" frameborder="0" allowfullscreen></iframe>

YeomanというGruntとBowerを内包したツールがあります。これだけ（node.js必要ですが）でgruntを実行できますので、ぜひためしてみてください。

```
$ npm install yo -g
$ npm install generator-maple -g
$ mkdir your_proj && cd $_
$ yo maple
$ grunt
```

## Summary

僕自身も1年前まで普通のHTMLコーダーでGUIアプリ大好きっ子でした。『黒い画面』ってのは必要そうだなとは思ってましたし、使ったら便利なんだろうなとも思ってましたけど、軽く触った程度でわかんなくなってGUIのほうがいいや！と何度も投げ出したものです。しかし、とりあえず触ってみる！動かす！ということを続けていれば、今ではGrunt（というかターミナル）無しではアプリ開発は考えれないほど手に慣れています。

多くのデザイナーさんたちがこちら側に来ていただければ、もっとデザイナーに便利なNodeパッケージやGemなどが出てくるでしょうし、みんなの制作環境がハッピーになると思っていますので、ぜひとも、まずは一歩を踏み出す、そして動かす、続けるってことを実践するキッカケとなってくれれば幸いです。

ありがとうございました。

### 追記

普段使ってるGruntプラグインまとめてみました。

+ __[CSSを書くために必要なGruntプルギン集！！ — MOL](http://t32k.me/mol/log/modern-coder/)__

---

この記事は[Frontrend Advent Calendar 2013](http://www.adventar.org/calendars/62)の1日目に寄稿した記事です。