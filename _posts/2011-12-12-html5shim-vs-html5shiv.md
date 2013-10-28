---
layout: post
title: html5shim vs html5shiv
categories:
- javascript
- markup
tags:
- html5
- javascript
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '9390'
  _aioseop_description: "Don’t lose any more time.\r\nhtml5shim and html5shiv are
    exactly the same thing."
---
<a href="http://atnd.org/events/21980">JavaScript Advent Calendar 2011 (オレ標準コース) </a>12日目の id:t32k です。去年も参加しましたがなんでもありと聞いて今年も懲りずに参加！
<a href="http://keycss.com/html5/html5shim-vs-html5shiv.html"><img title="Don’t lose any more time." src="http://t32k.me/mol/file/2011/12/same.png" alt="Don’t lose any more time. html5shim and html5shiv are exactly the same thing." />
</a>はじめに言っておきますが、html5shimもhtml5shivどっちもまったく同じです。違いなんて無いので、こんなことに頭を悩ませる暇があったらさっさとコードでも書いてろ！以上！うんこ(・∀・)!!

そんなこと言っても世の中結果じゃない、過程が大切だと思うんだ先生！ってことで今回は調べてみます。

<!--more-->

html5shi(m|v)、めんどくさいので以下html5.jsは"HTML5 IE enabling script"の名の通り、IE8以下で<em>article</em>などの新要素が正しく認識されずスタイル(CSS)がうまく適用されない問題を解決しそれらのブラウザでも利用可能にしてくれます。
<pre><code>document.createElement("article");</code></pre>
こんな感じにDOMで要素を生成すると、IEでもHTML5の要素にスタイルを効くようになります。実際のhtml5.jsはもっと複雑だけど基本的にはこんなことをやってます。詳しいことは下記スライド参照で。
<ul>
	<li><a href="http://prog.re-d.net/demo/slide/20101218/index.html">HTML5.jsの中身を見てみよう</a> by <a href="https://twitter.com/#!/kamiyam">@kamiyam</a></li>
</ul>
<h2>What's the difference?</h2>
そろそろHTML5でサイト作ってみっかーということでいろいろググってたら前述の問題に引っかかり、さらにググってみると同じ機能なのに名前が違う2つのスクリプトがあることを認識たのが今回の経緯です。
<ul>
	<li><a href="http://code.google.com/p/html5shim/">html5shim - HTML5 IE enabling script - Google Project Hosting</a></li>
	<li><a href="http://code.google.com/p/html5shiv/">html5shiv - HTML5 IE enabling script - Google Project Hosting </a></li>
</ul>
Google Codeにホスティングされている2つのコードを見比べても全く同じです。謎です。
<blockquote><strong>Common question:</strong> what's the difference between the html5shim and the html5shiv?

<strong>Answer:</strong> nothing, one has an m and one has a v - that's it.</blockquote>
と思ったら、似たような疑問を持つ人も多いのかよくある質問が用意されていました。

”違いなんて無いよ！片方はmで、片方がvなだけ。それだけ！”
<pre><code>&lt;!--[if lt IE 9]&gt;
 &lt;script src="/common/js/html5shiv.js"&gt;&lt;/script&gt;
&lt;![endif]--&gt;</code></pre>
※最近ではGoogle Codeにホスティングされているものを参照するのではなく、自鯖に落としてきて使用することが<a href="http://www.skyward-design.net/blog/archives/000134.html">推奨されています</a>。

お... また敷かれたレールを疑問も持たずに走ってればいいんだよ的な回答ですね。そんなの求めていないんだ！僕は！じゃーなぜ2つあるんだよ！どっち使えばいいんだよ！と遅れてきた反抗期によって僕はあきらめません。

まずは単語の意味から...
<blockquote>【名詞】【可算名詞】
(ものを水平にしたり，すき間などに入れる)詰め木[金]
<a href="http://ejje.weblio.jp/content/shim"> shimの意味 - 英和辞典 Weblio辞書 </a></blockquote>
<blockquote>【名詞】【可算名詞】
《米俗》 (ジャック)ナイフ
<a href="http://ejje.weblio.jp/content/shiv"> shivの意味 - 英和辞典 Weblio辞書 </a></blockquote>
ふむふむ、"shim" の方は詰め木ということで足りない機能を補完（カバー）する意味合いでも取れて、<a href="https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills">polyfill</a>みたいな感じですかね？。"shiv" はナイフ...どーゆこっちゃ＞＜
<h2>The Story of the HTML5 Shiv</h2>
行き詰まり感たっぷりだったところに、<a href="http://t32k.me/mol/log/trackhtml5inga-with-modernizr/">Modernizr</a> の開発者でも有名なPaul Irishさんが、<a href="http://paulirish.com/2011/the-history-of-the-html5-shiv/">The Story of the HTML5 Shiv </a>というドンピシャなタイトルの記事をあげていました。

この記事の前半部分をざっくりまとめてみると、

<strong>2007年くらい</strong>

■ developers:
新要素にCSS効かなくね？やばくねｗ？あれれｗｗ？

<strong>2008年</strong>

■ <a href="http://intertwingly.net/blog/2008/01/22/Best-Standards-Support#c1201006277"> Sjoerd Visscher</a>（初めてこのテクニックを披露した人）：
createElementしたらええで〜ｗｗｗ

■ <a href="http://ln.hixie.ch/?start=1201080691&amp;count=1"> Ian Hickson</a>（HTML5のエライ人）：
これマジパネェｗｗｗこれ使ったらIE7の互換shim簡単に作れるわーｗｗｗｗ

■ <a href="http://ejohn.org/blog/html5-shiv/">John Resig</a>（jQuery作った人）：
CSS効かせる方法、HTML5 Shivって名前つけたわーｗｗ（shimだけど）

<strong>2009年</strong>

■ <a href="http://remysharp.com/2009/01/07/html5-enabling-script/"> Remy Sharp</a>（初めてhtml5.jsをディストリビュートした人）：
HTML5 ShivのやつGoogle Codeにホスティングしといたわーｗｗ

<strong>2010年</strong>

■ <a href="http://code.google.com/p/html5shim/source/detail?r=2">Remy Sharp</a>：
html5shimでミラー作っておいたわーｗｗｗ

だいたいこんな感じですな。
<h2>Shiv?</h2>
ここで問題なのは、なんでRemy Sharpさんあとからhtml5shimのミラーを 公開したのか？ということですね。

"shiv" って単語がコンピューター用語で言う互換性のため回避策といった意味が一般認識されていなかったのではないかという仮説が僕の中で湧いてきました。

試しに<a href="https://github.com/">GitHub</a>で <a href="https://github.com/search?q=shiv&amp;type=Everything&amp;repo=&amp;langOverride=&amp;start_value=1">"shiv" で レポジトリ検索</a>をしてみると17件、<a href="https://github.com/search?type=Everything&amp;language=&amp;q=shim&amp;repo=&amp;langOverride=&amp;x=0&amp;y=0&amp;start_value=1">"shim"で検索</a>すると93件ヒットしました。"shiv" に関してはhtml5shivに関しての内容ばかりで、他のものも新しいライブラリです。

<a href="http://ejohn.org/blog/html5-shiv/#comment-296934">2008年のJohn Resig氏のエントリのコメント</a>においても、「shimじゃなくてshiv?」といった内容が見受けられます。

しかし、Wikipediaの<a href="http://en.wikipedia.org/wiki/Shim_(computing)">Shim (computing)</a>の項目には、"a shim (from shim) or <strong>shiv</strong> is a small library which..."とまぁなんか互換性のため回避策の意味として記述されています...

え、そうなの？なんでじゃ！ということで、例によって反抗期の僕には<a href="http://en.wikipedia.org/w/index.php?title=Shim_(computing)&amp;action=history">wikiの変更履歴</a>を見てみるとありました。21:20, 16 November 2011‎ までは Shim (computing)の項目に "shiv" って単語はなかった。なんだ最近、追記されてんじゃん！

まぁ少なくとも2008年のJohn Resigが書いたエントリの時点では "shiv" に「互換性のため回避策」といった意味がなかったのではないかと推測できます。
<h2>Conclusion</h2>
で結局、<strong>ここからは妄想</strong>になるんだけど、

<strong>2008年
</strong>

■ <a href="http://ejohn.org/blog/html5-shiv/">John Resig</a>（jQuery作った人）：
CSS効かせる方法、HTML5 Shivって名前つけたわーｗｗ
やってることはshimだけど、shivの方が武器っぽくって強そうじゃんｗｗｗドヤｗｗ

■ developers1:
shivじゃなくてshimだろｗｗワロスｗｗｗ

■ developers2:
html5shivいいねｗｗｗｗｗイカスｗｗｗｗｗ

<strong>2010年</strong>

■ <a href="http://code.google.com/p/html5shim/source/detail?r=2">Remy Sharp</a>：
html5shivでホスティングしたったーけどｗｗｗｗ
html5shimの方が意味的に分かりやすいし一応こっちも作っとくかーｗｗ

そんな経緯ですかね...<strong>”なぜ”</strong>そうしたのかって部分が言及されて（見つから）なかったので、あくまで上記は僕の<strong>妄想</strong>ですからあしからず。知ってる人いたら教えてください。

てか、<a href="http://www.modernizr.com/download/">Modernizrにバンドリングされてる</a>し、そっち使ったらいいんじゃないっすかねー（by <a href="https://twitter.com/#!/5509">@5509</a>）
<h2>参考</h2>
<ul>
	<li><a href="http://en.wikipedia.org/wiki/HTML5_Shiv">HTML5 Shiv - Wikipedia, the free encyclopedia </a></li>
	<li><a href="http://ejohn.org/blog/html5-shiv/">John Resig - HTML5 Shiv </a></li>
	<li><a href="http://remysharp.com/2009/01/07/html5-enabling-script/">HTML5 enabling script | remy sharp's b:log</a></li>
	<li><a href="http://paulirish.com/2011/the-history-of-the-html5-shiv/">The Story of the HTML5 Shiv « Paul Irish </a></li>
	<li><a href="http://en.wikipedia.org/wiki/Shim_(computing)">Shim (computing) - Wikipedia, the free encyclopedia </a></li>
</ul>
