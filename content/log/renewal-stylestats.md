---
date: 2015-04-27
title: そんなに目新しくもない技術でWebアプリをリニューアルした2015年春
subtitle: An evaluating tool for writing better CSS
categories: development
excerpt: 世間はReactの話題で持ちきりのようだけど、Backbone.jsでStyleStatsのWebアプリをリニューアルした。以上で伝えることは終わったが、リニューアルするにあたってつらかったことつらつらかきとめておく。
ogimage:
---

[世間はReactの話題で持ちきり](http://reactjs-meetup.connpass.com/event/11232/)のようだけど、Backbone.jsでStyleStatsのWebアプリをリニューアルした。以上で伝えることは終わったが、リニューアルするにあたってつらかったことつらつらかきとめておく。

+ [StyleStats - An evaluating tool for writing better CSS](http://www.stylestats.org/)

そもそもBackbone使うほど複雑なアプリでもないんだけど、勉強がてら使ってみた。てか[Parse.com](https://parse.com/)を使いたくて、それが[BackboneベースのSDK](https://parse.com/docs/js_guide)だったからというのもある。

Parse.comはmBaaS（Mobile Backend as a Service)の類で、データを簡単にストアしてくれるもの。僕のようなフロント側の人間でバックエンドがからっきしな人も、こうゆうのを使うとWebアプリケーションを簡単に作れるそうだ。StyleStatsで、テスト結果をデータに貯めときたかったので使ってみた。

+ [StyleStats Test Result | http://www.google.com/ - Sun Apr 26 2015 04:32:59 GMT-0700 (PDT)](http://www.stylestats.org/results/nBEUw1oi7k)

リニューアル後はテスト結果ひとつひとつにパーマリンクができるようになったので、定期的にテストかけといて、あとから比較（目視）とかできる。まぁデータ自体は溜まっていくので、今後はグラフ生成機能とか提供できるかもしれない（やらないかもしれない。[D3.js](http://d3js.org/)か...）。

## JavaScriptとか

個人的にJavaScriptはCrome拡張だったりNode.jsでCLIツール作ったりで書くくらいで、今回はじめてWebアプリケーションとしてのJavaScriptをBackbone.jsで書いた。うん、難しいよね。なんかうまく動かなかったら、それBackboneの問題なのかParseSDKの問題なのか、どっちかわからんと思ってたら、結局、自分のJS基礎力のなさから来る問題だったりして苦労した。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00NBHLZIA/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51oknTylWUL._SL160_.jpg" alt="入門Backbone.js" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00NBHLZIA/warikiru-22/" name="azlinklink" target="_blank">入門Backbone.js</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.4.27</div></div><div class="azlink-detail">James Sugrue,クイープ<br />翔泳社<br />売り上げランキング: 27475<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00NBHLZIA/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

世間がReact!React!React!って言ってる中、せっせと2012年くらいの記事を貪っていてちょっと辛かった。いや今までサボっていた自分が悪いんだ。置いてけぼり感つらい。資料に関しては上記の本で事足りる。

あと、[Browserify](http://browserify.org/)を使ってみた。個人的にどちらかというとNode.jsの文化に親しみを感じているのでモジュール管理としてはこれがいいのではと思ったけど、うまいこと使いこなせている自信はない。[Concatでいいんじゃないか](http://havelog.ayumusato.com/develop/others/e613-concat_build_pattern_examples.html)と思うこともあるが、`require()`したいんや。

でも[ES6のimport](http://www.2ality.com/2014/09/es6-modules-final.html)ってのもあるのね、どうしよう。まぁいいや。[es6ify](http://thlorenz.com/es6ify/)や[babelify](https://github.com/babel/babelify)というのもある。なんだこれ？まぁいいや。あ、そうそう。browserifyでHandlebarsのプリコンパイルしたかったら[hbsfy](https://github.com/epeli/node-hbsfy)っての使うらしいい。ファイファイやかましいわ。とにかく最近のES6,7事情ついていけてない、つらい。

あと[Grunt/Gulpで憔悴した話](http://t32k.me/mol/log/npm-run-script/)したけど、やっぱなんやかんやで、Gulp使った。起動させるインターフェイスとしてはnpm run script使っているので許して欲しい（誰）。

## CSSとか

UIは[Material Design](http://www.google.com/design/spec/material-design/introduction.html)をやってみたかったので、ここは王道な感じで、[Polymer](https://www.polymer-project.org/0.5/)の[Paper Element](https://www.polymer-project.org/0.5/docs/elements/)を使ってみようと思った。てか、Material Design以前に、Polymer以前に、[Web Components](http://webcomponents.org/)分かってないので色々読んだ。

### Web Components

+ [Custom Elements: HTML に新しい要素を定義する - HTML5 Rocks](http://www.html5rocks.com/ja/tutorials/webcomponents/customelements/)
+ [HTML で利用可能になった Template タグ: クライアントサイドのテンプレートの標準化 - HTML5 Rocks](http://www.html5rocks.com/ja/tutorials/webcomponents/template/)
+ [HTML Imports: ウェブのための #include - HTML5 Rocks](http://www.html5rocks.com/ja/tutorials/webcomponents/imports/)
+ [Shadow DOM 201: CSS とスタイリング - HTML5 Rocks](http://www.html5rocks.com/ja/tutorials/webcomponents/shadowdom-201/)
+ [Shadow DOM 301: 上級者向けコンセプトと DOM API - HTML5 Rocks](http://www.html5rocks.com/ja/tutorials/webcomponents/shadowdom-301/)

### Polymer

<div class="rm"><iframe src="https://www.youtube.com/embed/jrt7sMq9lO0?list=PLOU2XLYxmsII5c3Mgw6fNYCzaWrsM3sMN&amp;controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></div>

+ [Polycasts - YouTube](https://www.youtube.com/playlist?list=PLOU2XLYxmsII5c3Mgw6fNYCzaWrsM3sMN)


わー覚えること多すぎだ。疲れた。Polymerが0.8で爆速になったとかでAPIも変わったとかで、Paper elementsが0.8対応してないので、ここまできてやっぱやめた。つらい。

普通にMaterial DesignのCSSフレームワークを使おうと思ったけど、[Material UI](http://callemall.github.io/material-ui/#/)はReactで使うのをリコメンドしてるし、なんぞ！と思った。ので、[Materialize](http://materializecss.com/)使おうと思ったけど、これ120K近くもあるぞ。ということで、自分で、Mateliaze CSSを参考にしつつ、それっぽく作ってみた。単純に見た目だけでも再現してもなーと思って、動きもつけようと思ってCSS Animationとかよくわからんしなー、てかSVGもよくわからん。というか、UI作るの難しくなってきてるよね？JavaScript使うの前提とか。とにかくつらい。

## HTMLとか

```html
body
    header
        h1
            a タイトル
```

Node.jsのプロジェクトなので、惰性的にView Engineを[Jade](http://jade-lang.com/)で使ってたけど、このぶら下がり感がつらい。というか、嫌い。

Viewつながりで、サーバー上でもBackbone.jsを動かす[Rendr](https://github.com/rendrjs/rendr)使えたら、もっとシンプルになるのになーと思ったけど、力尽きた。導入は次回で。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4862462669/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51mzyCBKBDL._SL160_.jpg" alt="コーディングWebアクセシビリティ - WAI-ARIAで実現するマルチデバイス環境のWebアプリケーション" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4862462669/warikiru-22/" name="azlinklink" target="_blank">コーディングWebアクセシビリティ</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.4.27</div></div><div class="azlink-detail">伊原力也, 太田良典<br />ボーンデジタル<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4862462669/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

[WAI-ARIA](http://www.hitachi.co.jp/universaldesign/ria/ajax/wai-aria/index.html)とかあるよね、とりあえず`body role="application"`しとくので精一杯だ。また本読もう。ということで、つらかった。というか力尽きた。


## まとめとか

まぁ趣味プロジェクトで、とくにしがらみもないので、地道にマイペースでやってくしかない。よそはよそ、うちはうち。

React資料読んでて気づいたのだけど、[ReactはViewライブラリでBackbone + Reactって使い方もあるのね](https://speakerdeck.com/geta6/reacttofluxfalsekoto?slide=5)。[ParseReact](https://github.com/ParsePlatform/ParseReact)ってのもあるみたいだし、今度はReactがんばろう。

***

リニューアルにあたって、数多くの助言を与えてくださった[利休1000](https://twitter.com/1000ch)と[寿司銀平](https://twitter.com/ginpei_jp)さんに多大なる感謝の念を伝えたい。












