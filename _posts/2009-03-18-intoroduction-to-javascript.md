---
layout: post
title: JavaScript 第5版 1章 JavaScriptの概要
categories:
- javascript
tags:
- sai5
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/03/intoroduction-to-javascript.html
  _edit_last: '1'
  pvc_views: '1684'
---
<ul>
	<li>オブジェクト指向機能を備えたインタプリタ型のプログラミング言語</li>
	<li>クライアントサイドJavaScript</li>
	<li>もともとはLiveScriptという名前</li>
	<li>コアJavaScriptはECMA、DOMはW3C</li>
	<li>メソッドというのは、関数や手続きに相当するオブジェクト指向の用語</li>
	<li>イベントハンドラというのは、あるイベントが発生した時に実行するJavaScriptコード</li>
	<li>MozillaのCで書かれたインタプリタ SpiderMonkey</li>
	<li>MozillaのJavaで書かれたインタプリタ Rhino（ライノー）</li>
	<li>JSの勉強方法：とりあえずコード書け</li>
</ul>
<h2>疑問点</h2>
<h3>・関数は数じゃないん？</h3>
これはFunctionの中国語訳ですね、函数。数字を入れると数字が出てくる箱（函）と言う意味らしいっす。 ブラックボックスって感じかね。なので関数は日本語的に言えば「機能するもの」と捉えれば良いかな。 そういえば、中学校の数学の先生が2次関数を説明するときに関数は自販機と考えればよいと言ってたけ。 お金を入れたら（なにか数値を入力したら）ジュースが出てくる（値が返ってくる）って感じ。
<h3>・サンプルコードのiってなに？</h3>
i： integer（整数）の略だそうです。
習わし的にやってる感じですかね。
参考：<a href="http://q.hatena.ne.jp/1086523013">なぜプログラムのFor構文などの例文で使われる関数はいつも”i”なのでしょうか？</a>
<h3>・クライアントサイドJavaScriptとコアJavaScriptとDOMの違い</h3>
Core JS：じゃばすくりぷとの基本的な機能 DOM：HTML文書を操作するための仕様群
参考：<a href="https://developer.mozilla.org/ja/The_DOM_and_JavaScript">The DOM and JavaScript - MDC</a>

Client-side JS：Core JS＋DOMをブラウザ上に組み込んだもの。対となるのはServer-side JS。 基本的に『JavaScript』と言えば、Client-side JSのことを指す！ イメージとしてはこんな感じ↓
<img src="http://lh5.ggpht.com/_1drnogi3vdg/ScnDbx94PRI/AAAAAAAAAUs/RoHCZNYLBvw/js.png" alt="" />
<blockquote><a href="http://ja.wikipedia.org/wiki/%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%97%E3%83%AA%E3%82%BF">インタプリタ</a>インタプリタ（interpreter）とは、プログラミング言語で書かれたソースコードを逐次解釈しながら実行するソフトウェアである。プログラムの実行に主としてインタプリタが用いられるプログラミング言語をインタプリタ言語と呼ぶ。同じく解釈を行なうコンパイラと対比される。</blockquote>
