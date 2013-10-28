---
layout: post
title: JavaScript はやっとくべき！
categories:
- javascript
- translate
tags:
- dom
status: publish
type: post
published: true
meta:
  pvc_views: '11963'
  _edit_last: '1'
  _aioseop_description: "もし君が3年前にどの言語を学ぶべきかと尋ねていたのなら私はRubyと答えていただろう。もしそれが6年前だったならPHPだ。\r\n\r\n君が新しくプログラミング言語を学ぼうとしているのであれば、JavaScriptを学ぶ必要があるだろう。"
  _aioseop_keywords: javascript,dom,js
---
新年1発目にこれを持ってくるのは2011年の抱負ってことで。

<cite>原文：<a href="http://thenerdary.net/articles/entry/you_must_learn_javascript">You Must Learn JavaScript — Article — The Nerdary</a>
投稿日：2010-12-2 by Kenny Meyers</cite>

もし君が3年前にどの言語を学ぶべきかと尋ねてきたのなら私はRubyと答えていただろう。もしそれが6年前だったならPHPだ。

君が新しくプログラミング言語を学ぼうとしているのであれば、JavaScriptを選べばよいだろう。

<!--more-->
<h3><span style="color: #993300;">なんでやねん？</span></h3>
これは私の考えだが、あらゆるWebプログラマーはJavaScriptを学ぶべきである。この原則を刺激するような新技術がたくさん出てきている。その背景にはある一つの理由がある。それは<a href="http://ja.wikipedia.org/wiki/%E3%83%A6%E3%83%93%E3%82%AD%E3%82%BF%E3%82%B9">ユビキタス</a><span style="color: #888888;">（「いつでも、どこでも、だれでも」が恩恵を受けることができるインタフェース、環境、技術のこと）</span>だ。もし君がJavaScriptを使うのであれば、それは誰でも動かすことができるし、アッと驚かせるようなこともできる。どんなコンピューター上ですぐさまに実行可能でもある。

すべての企業がRuby屋ではないし、.NET屋でもない。これら両社の99％の時間はJavaScriptを熟知している者や長けている人を探すことに費やされるだろうと私は考えている。Microsoft、Facebook、Apple、Googleなどの企業は大事を為すためにJavaScriptを使っている。

JavaScriptを熟知することは、最もチャレンジングなことであり、プログラマーとしてやりがいのあることだろう。それは君が考えているより、信じられないほど多様性のある言語であり、大規模アプリケーションで使用できる。たくさんの得るものがあり、素晴らしいAPIもあり、今なお進化中である。

人々がHTML5について話をしているとき、彼らはたいていJavaScriptの話をしている。
<h3><span style="color: #993300;">どこから始めたらええねん？</span></h3>
<a href="http://www.amazon.co.jp/exec/obidos/ASIN/4839922373/warikiru-22/ref=nosim/"><img class="fig alignright" src="http://ecx.images-amazon.com/images/I/41ER9SJujTL._SL160_.jpg" alt="DOM Scripting 標準ガイドブック ~やさしく学ぶ、JavaScriptとDOMによるWebデザイン~ (Web Designing BOOKS)" width="124" height="160" /></a>JavaScriptは学ぶ出発点はWebページを操作することであり、DOMを理解することである。多くのJSプログラマーはこのことに関して異論があると思う、なぜなら、AjaxやJSの革命前はJavaScriptはDOMマニピュレータとして過小評価されていた。JSはただ単にWebサイトで表示・非表示するためだけのものではないと理解すべきだろう。

DOMの操作は簡単であり、すぐさまその効果を実感するだろう。DOM操作の基本を理解する最も良い本として<a href="http://www.amazon.co.jp/gp/product/1430233893?ie=UTF8&amp;tag=warikiru-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=1430233893">Dom Scripting</a> がある。大きなニュースがある。ついに最新版が出版されつつある<span style="color: #888888;">（2010/12/30第2版が発売。邦訳は初版）</span>。Jeremy Keithの著書はJavaScriptの基礎を学ぶ上で最適な入門書となってくれるだろう。

<a href="http://www.amazon.co.jp/JavaScript-%E7%AC%AC5%E7%89%88-David-Flanagan/dp/4873113296%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113296"><img class="fig alignright" src="http://ecx.images-amazon.com/images/I/413amOWGgvL._SL160_.jpg" alt="JavaScript 第5版" width="123" height="160" /></a>これは始まりである。もし、君がより多くの知識を望むのであれば、<a href="http://stackoverflow.com/questions/74884/good-javascript-books">Stack Overflowのこの質問</a>を見ればいい。いくつかの素晴らしいレコメンドをされているのもあり、私もその多くを読んだことがある。中でも <a href="http://www.amazon.co.jp/gp/product/0596805527?ie=UTF8&amp;tag=warikiru-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=0596805527">Javascript: the Definitive Guide</a><img style="border: none !important; margin: 0px !important;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=as2&amp;o=9&amp;a=0596805527" alt="" width="1" height="1" border="0" /> <span style="color: #888888;">（2011/2/15第6版が発売予定。邦訳は第5版）</span>はJavaScriptのバイブルと言っていいだろう。これはありがたや！

<a href="http://twitter.com/#!/angusTweets">Angus Croll </a>の <a href="http://javascriptweblog.wordpress.com/">JavaScript, Javascript</a> は Core JavaScript を理解するのに最も適したブログだと考えている。このブログは、実際に知識が頭の中に飛び込んでくるように分かりやすく詳細に書かれている。<a href="http://www.crockford.com/">Douglas Crockford</a> も素晴らしいが、Angusほどきめ細かい解説をしない。

フレームワークは素敵なものであり、役立つものだ。もし誰かが学習中にフレームワークを使用していることで君のことを小ばかにしてきたら、聞く耳をもたなくてもいい。君は正しいことをしているからだ。どんな参考書や ドキュメントよりもjQueryは多くの人にJavaScriptにおける事の重要性について教えてくれる。君は君のやるべきことをやった後に Core JavaScript に挑戦すればいいだろう。

Firefox, Firebugをインストールしなさい。Webkit が追い上げてきているが、私はいまだに <a href="https://addons.mozilla.org/ja/firefox/addon/1843/">Firebug</a> はベストな装備だと考えている。どのように動作するのか理解するためにFirebugの紹介デモをサイトで見るとよいだろう。私の同僚であり友人でもあるLeevi Grahamは、<a href="http://twitter.com/#!/leevigraham/status/9403851249549312">”FirebugはこれからもFirefoxとの関係を保つ”</a>と言っている。お、どうやら新しいバージョンがリリースされたようだ。

MozillaもまたJavaScriptの素晴らしい<a href="https://developer.mozilla.org/ja/JavaScript">オンラインドキュメント</a>を公開している。君はここを参照するとよいだろう。

JavaScriptを学べ！君が考えているどの言語よりも絶対に重要だから。
