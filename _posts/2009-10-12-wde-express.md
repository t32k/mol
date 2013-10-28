---
layout: post
title: パフォーマンスアップのウェブ技術：WDE-Express
categories:
- performance
- report
tags:
- apple
status: publish
type: post
published: true
meta:
  pvc_views: '3010'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/10/wdeexpress.html
  _edit_last: '1'
---
<img src="http://lh6.ggpht.com/_1drnogi3vdg/StHWY9u5e5I/AAAAAAAAAno/hd0S_BDebxw/wpo.jpg" alt="'" />
<ul>
	<li><a href="http://atnd.org/events/1412">パフォーマンスアップのウェブ技術：WDE-Express</a></li>
</ul>
<blockquote><span style="font-size: 85%;">不況下、企業はコスト削減を強いられるようになりました。人件費削減・広告/宣伝費はもとより、大手企業では、社内のアプリケーション費用・サーバーコストまで削減を求められます。
また、ユーザーエクスペリエンス（UX）の側面から考えても、”ウェブサイトの表示が2秒以上の時間を要する”ことで、ページからの離脱率が高くなります。
このセッションでは、ウェブサイトのパフォーマンスを向上させる必要性と方法をご紹介いたします。</span></blockquote>
<img src="http://lh3.ggpht.com/_1drnogi3vdg/StLopxhZpqI/AAAAAAAAAns/VxjqP-aq5SU/WDE-ex-parform-200.jpg" alt="" />

<a href="http://warikiru.blogspot.com/2009/10/pecha-kucha-night-in-nagoya-vol2.html">前日の名古屋</a>から、10日は<a href="http://twitter.com/mantangs">菊池さん</a>のお話を聞きにApple Store 心斎橋に行ってきました。Apple Store 心斎橋は初めて入ったけど、とても広い空間で落ち着ける場所でした。以下、メモメモ。

表示スピードを上げることで、CVやPVが増加するデータを紹介
<ul>
	<li><a href="http://money.aol.com/">AOL Money &amp; Finance</a></li>
	<li><a href="http://shopping.aol.com/">AOL Shopping</a></li>
	<li><a href="http://www.bing.com/">Bing</a></li>
	<li><a href="http://www.google.co.jp/">Google</a></li>
	<li><a href="http://www.shopzilla.com/">Shopzilla</a></li>
</ul>
<span style="font-weight: bold;">速いことは品質</span>
ShopzillaではCVが2.5-3.5%UP、PVで25%UPというデータも。

画像の最適化
<a href="http://www.gracepointafterfive.com/punypng/">punypng</a>が一番使い勝手・圧縮率が良いと感じる
（<a href="http://www.atmarkit.co.jp/news/200903/17/turbo.html">Opera Turbo</a>にも見られるように画像の最適化は重要）

PNG8を使え(Fireworksがいろいろ便利)
AlphaImageLoaderは最悪フリーズする可能性もあり危険

JSとCSSはちゃんとおけ

CSSファイル最適化
CSSスプライトは<a href="http://spritegen.website-performance.org/">CSS Sprite Generator</a>が使い勝手が良い

Data URI
IE6/7はサポート外（コンディショナルコメントで回避）

Web Fonts
（ちょっと僕にはややこしかった＞＜）

CSSセレクタを最適化
短く、使えるコードはリユース

<a href="http://github.com/stubbornella/oocss/downloads">OOCSS</a> (Object Oriented CSS)
<a href="http://east.webdirections.org/speaker/nicole-sullivan/">Nicole Sullivan</a>が開発
YUI Grid.cssの半分のファイルサイズ
<ul>
	<li>モジュール化</li>
	<li>構造と表現の分離</li>
	<li>箱と中身の分離</li>
</ul>
（Demoは怖いなーと感じました。）

プロファイリングツールを使え
<ul>
	<li><a href="http://sourceforge.net/apps/mediawiki/pagetest/index.php?title=Main_Page">AOL Pagetest</a></li>
	<li><a href="http://www.fiddler2.com/fiddler2/">MS Fiddler</a></li>
	<li><a href="http://validator.w3.org/checklink">W3C Link Checker</a>（実はファイル取得にかかった時間を表示してある）</li>
</ul>
<h3>感想</h3>
OOCSSに関しては、Webサイトのパフォーマンスというよりかは、開発者のパフォーマンス向上に有効かと思った。クラス名を憶えなければならないコストもあるが、ページのレイアウト変更も容易にできるのは捨てがたいメリットだ。この辺はもうちょっと勉強せねば。。

全体として、<a href="http://en.oreilly.com/velocity2009">Velocity</a>や<a href="http://www.amazon.co.jp/gp/product/0596522304?ie=UTF8&amp;tag=warikiru-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=0596522304">Even Faster Web Sites</a>などからの情報が多く、まだまだ知らないところが多いなと感じた。また、画像圧縮・パフォーマンスツールなどの類が多く、それらの特性を理解するのにも時間がかかるなと。けれども、僕らの目的はツールを使いこなすことではなく、Webサイトのパフォーマンスを上げてユーザーにまた使ってもらおうということが本来の目的なのでそこのところを自覚せねばとも感じさせられたセミナーだった。
<span style="font-size: 85%;"> </span>
