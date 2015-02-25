---
date: 2012-07-12
title: パフォーマンスからみるSass/Compass 第1回：Nestingと@import
categories: performance
---


<a href="http://sass-lang.com/">Sass</a>とかいろんな機能ありますよね、でもぶっちゃけそんなにいっぱい機能あっても使わないし( ･´ω･｀)　案外、//ダブスラでコメントアウトできるのが一番嬉しかったりもします今日このごろです。

## @import

というわけで、そんな僕がSassを使うと思ったのも@importを使いたかったからという至極単純な動機によるものです。@import自体は普通のCSSでも使えますが、パフォーマンス的に難がありまして、あんまり使う気になれない、かといってファイル管理はページ単位やコンポーネント単位でちゃんとやらないと後々めんどいなというジレンマもあります。

そうゆうわけで、なんで普通の@importがダメなのか説明します。
<blockquote>IEにおいて@importはページ下部に置いた&lt;link&gt;タグのような挙動をします。

<a href="http://developer.yahoo.com/performance/rules.html/rules.html#csslink">Best Practices for Speeding Up Your Web Site </a></blockquote>
Yahoo!のパフォーマンスベスト・プラクティスにおいて、上記のような記述がありました。Styleの情報というのはできる限りページ上部に置いてレンダリングを早く開始させる必要があるのでこれは頂けませぬ。

まぁ基本的に@importのパフォーマンス的問題はIE以外ならOKであれば使ってもいいのかなと思ってたんですけど、よくよく調べてみるとそうでもなかったですという話。
<pre><code>/* first.css */
@import url("second.css")</code></pre>
まぁ上記のような&lt;link&gt;で読み込んだfirst.cssでsecond.cssを@importするといった例があるとします。これがどのような挙動をするのかと言いますと、
<blockquote>ブラウザーはsecond.cssをダウンロード可能と発見する前に、必ずfirst.cssのダウンロード、パース、実行をする。

<a href="https://developers.google.com/speed/docs/best-practices/rtt#AvoidCssImport">Minimize round-trip times - Make the Web Faster — Google Developers</a></blockquote>
Googleの方には上記のようなことが書かれていました。つまり、first.cssを読み込み完了してからsecond.cssを読み込みに行くので並列ダウンロードができないってことです。これってIEに限ったことではなくてすべてのブラウザーで起こりうることらしいです。マジかいや！てことで、<a href="http://stevesouders.com/tests/atimport/link-with-import.php">Steve Soudersセンセのテストケース</a>を最新のChromeのNetworkパネルで見てみると本当にそうでした。さーせん！ということで、やっぱり普通の@importは使うべきではないですな。

詳しくは下記ブログ読むと良いよ。
<ul>
	<li><a href="http://www.stevesouders.com/blog/2009/04/09/dont-use-import/">don’t use @import | High Performance Web Sites </a></li>
</ul>
まぁ、そうゆうわけでSassの@importですよ。基本ローカル環境でコンパイルして一つのCSSファイルにまとめるので、読み込むのは実質1ファイルだけになるんですね。それでいて、ページ単位やコンポーネント単位でファイル分割できるのでコードの見通しも悪くならない、素敵です。sass --watchとか<a href="http://mhs.github.com/scout-app/">Scout</a>とか使えば毎回手動でコンパイルしなくても更新があれば自動的にコンパイルしてくれます。
<pre><code>// Sass
 @import "_reset";
 @import "_common";
 @import "_header";
 @import "_main";
 @import "_footer";</code></pre>
これだけのためにでもSass導入してもいいんじゃないかと個人的には思っています。
<h2>Nesting</h2>
あと、便利っちゃー便利なのがネストです。下記のようにセレクタ、プロパティの重複する部分ってのを省略して書けます。
<pre><code>// Sass
table.hl {
  margin: 2em 0;
  td.ln {
    text-align: right;
  }
}
li {
  font: {
    family: serif;
    weight: bold;
    size: 1.2em;
  }
}</code></pre>
上記は下記のようにコンパイルされます。
<pre><code>/* CSS */
table.hl {
  margin: 2em 0;
}
table.hl td.ln {
  text-align: right;
}
li {
  font-family: serif;
  font-weight: bold;
  font-size: 1.2em;
}</code></pre>
子孫セレクタとか何回も同じセレクタを宣言するのはめんどいですよね。あとモジュール単位で、例えば.module{}以下に必要なスタイルをネストしておけば、そのモジュールが要らなくなったりとか修正が必要になった時とか対応が楽です。

とは言いつつも、そのモジュールの見通しが甘くて案外複雑なことをやらないとだめになりネストが3階層、4階層となってしまう時があります。そうなるとコンパイルされたCSSというのは子孫セレクタとかでつながった長いセレクタになってしまいます。

これってどーなのよ？って話ですよね。はじめに言っておきますが気にしなくてもいい。

世の中には<a href="https://developer.mozilla.org/ja/Writing_Efficient_CSS">CSSセレクタの最適化</a>というものがありまして、要はCSSセレクタの解釈というのは<strong>右から左へ</strong>とされていくわけでして、セレクタが長ければ長いほど解釈するのに時間がかかるので、単一のクラスセレクタとかにしたらいいよーみたいな話です。

これってどんだけの程度なのよ！？ってことが気になります。詳しくは下記翻訳でまとめられています。
<ul>
	<li><a href="http://t32k.me/mol/log/impact-of-css-selector/">CSSセレクタのパフォーマンスへの影響 | MOL </a></li>
</ul>
1000個のCSSセレクタを改善しても20msくらいしか変わらなかったという結論です。これは2009年の話でして、世の中進歩しています。
<ul>
	<li><a href="http://calendar.perfplanet.com/2011/css-selector-performance-has-changed-for-the-better/">Performance Calendar » CSS Selector Performance has changed! (For the better) </a></li>
</ul>
2011年の年末に書かれた上記の記事ではwebkitに関してですが、CSSセレクタのマッチング処理ってのはブラウザ側で最適化されているという話です。
<ol>
	<li>Style Sharing</li>
	<li>Rule Hashes</li>
	<li>Ancestor Filters</li>
	<li>Fast Path</li>
</ol>
上記のような改善がされていてるとのことでして、詳しいことは日本語で解説されてる以下のブログで（素敵！）
<ul>
	<li><a href=" http://memolog.org/2012/05/css_selector_performance.php  ">CSS Selector Performance - メモログ</a></li>
</ul>
まぁ要するに2009年段階でも気にしなくてもいいレベルだったのにそれから2年経ってさらに気にしなくてもいいレベルになってきた感じです。
<pre><code>/* Baseline 
　コード量の差をなくすためにマッチングしないセレクタが記述されている*/
.noclass0001 { background: #CFD; }

/* Descendant*/
DIV DIV DIV P A.class0001 { background: #CFD; }</code></pre>
<ul>
	<li><a href="http://stevesouders.com/tests/css-selectors/baseline.php">CSS Selectors: Baseline </a>（ベースライン）</li>
	<li><a href="http://stevesouders.com/tests/css-selectors/descendant.php">CSS Selectors: Descendant </a>（子孫セレクタ）</li>
</ul>
試しに、最新のChromeで上記のSoudersセンセのテストケースをもう一度やってみると、数ミリ秒しか変わんなかったです。1000個のセレクタ改善しても数ミリ秒しか違わないのは費用対効果悪すぎです。

ってことで、Sassでネストしまくって、それによるセレクタの解釈遅延ってのは気にしなくてもいいのかなという個人的結論。もちろん、ネストしまくったら何がなんだかわからないCSSになってしまうので、可読性のために、2,3階層程度でとどめておくほうが良いでしょう。
