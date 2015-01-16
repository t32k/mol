---
date: 2009-12-04
title: 高速ウェブアプリのためのCSSパフォーマンス - CSS Performance for Fast Web Applications
categories: report
---
<img class="aligncenter" src="http://lh5.ggpht.com/_1drnogi3vdg/SxOxWE0x8BI/AAAAAAAAAuY/xEaJ1qjOsUA/nicole-sulivan.jpg" alt="Nicole Sullivan" width="512" height="148" /><a href="http://east.webdirections.org/wde/2009/program/">Web Directions East 2009 カンファレンス</a> 11月13日 15:00–16:00

<h2>Nicole Sullivan（ニコール・サリバン）</h2>
3000以上にも昇る大規模サイトの最適化に携わって来た Nicole Sullivan は、現在 Yahoo! のパフォーマンスエンジニアと最適化のエバンジェリストとして国内外のセミナーで講演。Webサイトに関する研究だけでなく、プロジェクト管理もこなすマルチタスクなリーダーシップを発揮。フロントエンドエンジニアとしての高いスキルを持つ。

<!--more-->
<h2>Contacts</h2>
<ul>
	<li><a href="http://www.stubbornella.org/content/">Stubbornella - Blog</a></li>
	<li><a href="http://twitter.com/stubbornella">Nicole Sullivan (stubbornella) on Twitter</a></li>
	<li><a href="http://www.slideshare.net/stubbornella">Nicole Sullivan | SlideShare</a></li>
</ul>
<h2>高速ウェブアプリのためのCSSパフォーマンス - CSS Performance for Fast Web Applications</h2>
<h3>UNDERSTANDING THE CASCADE</h3>
デフォルトのスタイルがブラウザ毎で存在しそれは全て違う
<a href="http://developer.yahoo.com/yui/reset/">YUIのrecet.css</a>を使うと良い

クラスの順序に違いはない
プロパティと値の順序
スペルミスはエラーにならない（無視されるだけ）
<pre><code>color:red, colour:blue
</code></pre>

スタイルの順序
<pre><code>.foo {color: red;}
.foo {color: blue;}
</code></pre>
この場合、blueが勝つ
<pre><code>&lt;link rel="stylesheet" type="text/css" href="styles.css" /&gt;
&lt;link rel="stylesheet" type="text/css" href="moreStyles.css" /&gt;
</code></pre>
この場合、moreStyles.cssの方が勝つ

同じ詳細度なら最後に出てきた方が勝つ

詳細度は速く計算される必要がある

IDとクラス
<pre><code>#nav p {color: red }
.nav p {color: blue }
</code></pre>

INLINE STYLES
<pre><code>&lt;p style=”color: green;”&gt;My page&lt;/p&gt;
</code></pre>

!IMPORTANT
<pre><code>p{color: red !important}
&lt;p style="color: green;”&gt;My page&lt;/p&gt;
</code></pre>
この場合、redになる

継承
<pre><code>body{font-size: 18px;}
&lt;body&gt;
&lt;p&gt;This text is 18px.&lt;/p&gt;
&lt;/body&gt;
</code></pre>
P要素も18pxになる

うまくいかなかったらスパゲッティコードになってしまう

<strong>CSS IS AWESOME</strong>

コードは脆い　人が変われば壊されてしまう
熟練度が必要
コードの再利用はほとんどない　人の書いたコードは信用しない
ファイルサイズが増大していく　修正を繰り返していけばどんどん増える
<h3>HOW TO ARCHITECT GOOD CSS?</h3>
Object Oriented CSS
プロパティではなくセレクタに注目する

<a title="Nicole Sullivan by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/4103194252/"><img src="http://farm3.static.flickr.com/2714/4103194252_b84da463f6.jpg" alt="Nicole Sullivan" width="500" height="375" /></a>
用語の使い方に注意する（ex.クラスって何よ？）
<a href="http://wiki.github.com/stubbornella/oocss/">Home - oocss - GitHub</a>

見出しについて
デベロッパーじゃデザインの意味が分からない

再利用はパフォーマンスに良い

冗長性は避ける
似たようなものはまとめろ

ロケーションの依存性を避ける
<pre><code>#weatherModule h3{color:red;}
#tabs h3{color:blue}
</code></pre>

本当に必要なのか考える
<a href="http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/">
</a>
<h3><a href="http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/">REFLOWS and rendering time</a></h3>
CSSパフォーマンスで重要なのはCSSファイルのサイズとHTTPリクエスト数
リフローとレンダリング時間は大した問題ではない
<ul>
	<li>Toggle classes as low in the dom tree as possible</li>
	<li>Avoid setting multiple inline styles</li>
	<li>Apply animations to elements that are position fixed or absolute</li>
	<li>Trade smoothness for speed</li>
	<li>Avoid tables for date</li>
	<li>Avoid JavaScript expressions in the CSS (IE only)</li>
</ul>
<h3>Apply programming best practices to style sheets</h3>
デフォルト値を設定する
<pre><code>×　#tabs h3{color:blue}
</code></pre>

クラスに構造を定義する
<pre><code>×　div.error{...}
</code></pre>

要素にスタイル付けしない
<pre><code>×　p{..}
</code></pre>

同じ詳細度にする

セレクタによるハックは控えめに
<pre><code>×　.ie .mod .hd{...}　→　.mod .hd{_zoom:1;}
</code></pre>

ロケーションによる詳細度の指定は避ける
<pre><code>×　.sidebar ul{...}
×　.header ul {...}
</code></pre>

過度に特定なクラス名は避ける
<pre><code>×　.niXcolesDucatiMonster620{...}
</code></pre>

シングルトンは避ける（IDは避ける）
<pre><code>×　#myUniqueIdentifier{...}
</code></pre>

ミックスインを使う
<pre><code>○ class="media" class="media extended"
</code></pre>

カプセル化
オブジェクトのサブノードにアクセスさせない
<h2>セッション感想</h2>
前半はCSSの基礎的なことでだったので、エンジニアさんにCSSを説明するときに便利だと思った。全体としてはOO（オブジェクト指向）CSS入門のようなセッションで、複数人でのコーディング、修正の多い大規模サイト運用において、どのようにCSSのパフォーマンスを発揮していくのかといった内容だった。

まさしく大規模サイトにOOCSSは最適だと思う。ただ、OOCSSを導入するにあたっては既存のCSSでマークアップしたページとの兼ね合いを考えると難しいものがある。CSS自体、スパゲッティコード（ごちゃごちゃになったコード）化しやすい傾向もあって、使用していない/しているコードの把握、CSSのコードを設計するために現在どのようなデザインエレメントが存在するのか調査・カタログ化、デザイン部内のコーディングルールの周知などを既存のコードを運用しつつ考えれば、かなりのリソースが割かれるのは確実だ。

逆に、Webデザイナー1人で管理できるレベル程度の小規模サイトではOOCSSのメリットはあまり享受できないかもしれない。いや、でも修正に修正重ねていったら使わないコードが増えていくのかもしれない。

結局、OOCSSの理念としてCSSコード量をむやみに増やさないというところに重きが置いてあるのかなと理解した。
