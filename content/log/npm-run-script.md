---
date: 2015-03-25
title: Grunt/Gulpで憔悴したおっさんの話
subtitle: Hello, npm run-script!
categories: 
    - development
excerpt: 先人たちが1年前に通った道で、いろいろいまさらかよって話なんですが。基本的には下記の記事読んだら分かります。要はGulpとかGruntといったモノ使わずにnpm run-scriptでビルドしよーぜって話です。
ogimage: https://images-na.ssl-images-amazon.com/images/I/518ME653H3L.jpg
---

先人たちが1年前に通った道で、いろいろいまさらかよって話なんですが。基本的に以下の記事読んだら分かります。要はGulpとかGruntといったモノ使わずに`npm run hogehoge`でビルドしよーぜって話です。

+ [task automation with npm run](http://substack.net/task_automation_with_npm_run)
+ [オレ的Gruntに対する最新の気持ち - from scratch](http://yosuke-furukawa.hatenablog.com/entry/2014/02/19/112931)
+ [Node - npm で依存もタスクも一元化する](http://qiita.com/Jxck_/items/efaff21b977ddc782971)
+ [How to Use npm as a Build Tool](http://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/)

```json
// package.json
  "scripts": {
    "start": "npm run start-serve & npm run watch",
    "test": "stylestats public/files/css/maple.css",
    "start-serve": "browser-sync start --server public/ --files public/files/**/*",
    "clean": "rm -rf public/files/css/*",
    "js:min": "uglifyjs public/files/js/app.js > public/files/js/app.min.js",
    "build:js": "browserify assets/scripts/app.js > public/files/js/app.js",
    "css:sass": "node-sass assets/styles/maple.scss public/files/css/maple.css",
    "css:prefix": "autoprefixer -b 'last 2 versions' public/files/css/maple.css",
    "css:comb": "csscomb public/files/css/maple.css",
    "css:min": "csso public/files/css/maple.css public/files/css/maple.min.css",
    "build:css": "bin/build-css.sh",
    "build": "npm run build:js && npm run build:css",
    "lint:js": "jshint assets/scripts/app.js",
    "lint:css": "scss-lint assets/styles/**/*.scss",
    "lint": "npm run lint:js && npm run lint:css",
    "watch:js": "watch 'npm run build:js' assets/scripts/",
    "watch:css": "watch 'npm run build:css' assets/styles/",
    "watch": "npm run watch:js & npm run watch:css"
  }
```
こんな感じで`package.json`に記述して、`npm run watch`とかコマンド打って使う。


## npm run-scriptを使うに至るまでの経緯

率直に言って、おっさん疲れたのです。

### ユーザーとして

まぁタスクランナーを使うユーザーとしては、簡単に使いたいよねってのが本音なわけで、[2年前はGrunt便利だぜー！](https://t32k.me/mol/log/modern-development-workflow-with-grunt/)ってふれまわったけど、今いざ使ってみようと思うと、あれこれどーするんだっけ？みたいなことが多い。

ましてや、最近は[Gulp](http://gulpjs.com/)のほうが勢いあるみたいじゃないですか、まぁGulpも使うんですけど、開発しているプロジェクトによって採用しているのがGrunt/Gulpでバラバラになって、Gulpのプロジェクトで`grunt`ってコマンド叩いたりして、『あーここはGulpかー』なんてこともあったりするわけです。

またGruntで使ってるこのプラグインのGulpバージョンないかなーって探すとなかったりする。もしくは作る作る詐欺でリポジトリだけがあってションボリしたりするわけです。

はたまた四天王的に『クククッ、Gruntがやられたようだな、あいつは四天王のなかでも最弱（ｒｙ』とかいって、なんだか[Broccoli](http://www.solitr.com/blog/2014/02/broccoli-first-release/)とかゆー人もいるわけじゃないですか。もう頭いっぱいなんです。おっさん疲れたのです。

普通に元のコマンド叩いたらいいじゃんって思うんです。

### プラグイン作者として

若気の至りで、おっさんも昔はよく[Gruntプラグインを作った](https://www.npmjs.com/~t32k)のです。実際に自分のプロジェクトでGruntを使い、必要だったので、プラグイン開発に対する情熱もあったわけですけど、まぁGulpとか使い出したり、普通にコマンド打ってたら、開発するモチベーションがダダ下がりなわけです。

で、そんな時に限って、依存しているパッケージが頻繁にアップデートとかするんですよ。いっぱい新機能とか盛り込んできたりするわけですよ、そしたらissuesで対応しろとか言われるわけですよ。APIも変更してきたりするわけですよ、そしたらissuesで対応しろとか言われるわけですよ。もう追いつけないです。おっさん疲れたのです。

普通に元のコマンド叩けよって思うんです。

### 依存されるパッケージ作者として

[StyleStats](https://github.com/t32k/stylestats)というそこそこ使われるnpmパッケージを作っているのですが、ありがたいことに僕とは別の開発者様が[Grunt](https://github.com/tvooo/grunt-stylestats)/[Gulp](https://github.com/1000ch/gulp-stylestats)のプラグインを作ってもらっているのです。

ただですね、StyleStats Grunt Pluginのほうが[完全に開発が止まってまして](https://github.com/tvooo/grunt-stylestats/commits/master)、StyleStatsを使いたいGruntプロジェクトのユーザーに人になんて言ったらいいのかなーって、『Gulpの方使ってくださいー』って言うのもなーなんて。

かといって、Gruntプラグインの人に『ちょっとアップデートしてくれよ！』って言うのもなーって。前述の通り、やる気が無い気持ちは痛いほどわかるしなーって。でも更新止まってから、こちらとしてはいっぱいいろんな機能リリースしてるからみんなに使って欲しいしなーって。

僕がPR送ればいいのかもしれないけど、俺もGruntのプラグイン開発ってどうするんだっけって感じだし。そもそもPR送ってもマージしてくれるのか。てか飽きたならリポジトリをtransferしてくれないかなーって。そうやって気を使うのダルいんですよ、おっさん疲れたのです。

普通に元のコマンド叩いてくださいって思うんです。

## npm run-scriptの抑えどころ

ということで、npmで元のコマンド叩いたら皆しあわせってことでnpm run-script使おうぜって話。そんな難しいことはないです。基本的には各コマンドをpackage.jsonに記述していくだけです。ざっくりだけどプロジェクトで使う例としてはこんな感じかな。

+ [t32k/maple/package.json](https://github.com/t32k/maple/blob/master/package.json)

（久しぶりのMaple!!一応、[Gruntバージョン](https://github.com/t32k/maple/tree/grunt-ver)も残してある）

__ファイル監視はどーするの？：__

[mikeal/watch](https://github.com/mikeal/watch) を使ってね。

```json
"watch:css": "watch 'npm run build:css' assets/styles/"
```

__複数タスク実行はどーするの？：__

直列に実行するときは`&&`でつないでね。

```json
"build": "npm run build:js && npm run build:css"
```

並列に実行したいときは、`&`でつなぐか、[parallelshell](https://github.com/keithamus/parallelshell)を使ってね。

```json
"watch": "npm run watch:js & npm run watch:css"
"watch": "parallelshell 'npm run watch:js' 'npm run watch:css'"
```

__スクリプトが長すぎるよ！__

シェルファイルに分割するといいよ。

```shell
#!/bin/bash
npm run css:sass & npm run css:prefix & npm run css:comb & npm run css:min
```

`chmod +x`しとく。

```json
"build:css": "bin/build-css.sh"
```

または、設定系のオプションは、`config`フィールドに記述して、`scripts`フィールドで、`$npm_package_config_NAME`のようにして使う。が、$npm_package_configって！長い！

```json
  "config": {
    "stylestats": "path/to/configuration.json"
  },
  "scripts": {
    "test": "stylestats app.css --config $npm_package_config_stylestats",
```

はたまた、npm@2.0以上のユーザーであれば、[Passing Arguments](https://github.com/npm/npm/pull/5518)というナウい機能を使う。

```json
"scripts": {
  "test": "mocha test/",
  "test:xunit": "npm run test -- --reporter xunit"
}
```
上記のように、`--`を使うことで`npm test`のあとにコマンドをつなげられる。

__Windowsユーザーは？__

[win-bash](http://win-bash.sourceforge.net/)使ってもらうとか、UNIX系のコマンド系をラップしてるnpmパッケージ使って（例：`rm -rf` > [rimraf](https://github.com/isaacs/rimraf)）npm scriptを書くよう心がけるとか、とりまがんばってね。


## まとめ

そうゆうわけで、Gulp/Gruntを通さなければプラグインの依存パッケージの更新追随を待たなくてもいいし、Node.js/npmに関する知識とかUNIXに関する知識は、数ヶ月で変わることもないので、変化に適応できない私みたいなおっさんにも優しいんじゃないんでしょうか。ちょっと複雑なことやろうとすると、Node.jsのコードを書かないとできないかもしれないけど、きっと心の優しい誰かがその素晴らしい見聞を共有してくれると思うのです。おっさんは気長に待つのです。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/518ME653H3L._SL160_.jpg" alt="UNIXという考え方―その設計思想と哲学" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/" name="azlinklink" target="_blank">UNIXという考え方―その設計思想と哲学</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.3.26</div></div><div class="azlink-detail">Mike Gancarz,芳尾 桂<br />オーム社<br />売り上げランキング: 21740<br /></div><div class="azlink-review" style="margin-top:10px;margin-bottom:10px"></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

てか、Makefileでいいんじゃね？  
って、思ったそこのでっかいおっさんちょっと出てこいよ！

***

#### 関連エントリ

+ [【翻訳】Web世代のデベロッパーのためのmake - MOL](/mol/log/make-for-the-web-generation/)