---
layout: post
title: Google Analytics カスタム変数、パート1：なぜ？
categories:
- analytics
- translate
tags:
- google analytics
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '4684'
---
<cite>原文： <a href="http://www.lunametrics.com/blog/2010/04/15/google-analytics-custom-variables-part/">Google Analytics Custom Variables, Part I: Why?</a>
投稿日：2010-4-15　by Jonathan</cite>

Google Analaytics はユーザー情報をこれまで以上に継続してトラッキングする方法として、<a href="http://analytics.blogspot.com/2009/10/google-analytics-now-more-powerful.html">カスタム変数</a>を最近発表したんだ。
<h3>カスタム変数とは？</h3>
GAは、新規ユーザーだろうとリピーターであろうとも、ユーザーが閲覧している国や都市、さらにはどんなキャンペーンもしくはキーワード、リンクで来訪したのかなどの情報をすでに記録している。

<img class="alignright" title="クレヨン" src="http://www.lunametrics.com/wp-content/uploads/2010/04/g2FEl5-300x179.jpg" alt="" width="300" height="179" />

しかし、GAでは同じようにこれら以外の情報も得ることができるかもしれない。例えば、君のCRMシステムで顧客情報を持っているとしよう。（もう少し具体的な例は後述する。）もし、そのような情報を<a href="http://cutroni.com/blog/2008/10/22/google-analytics-advanced-segmentation/">詳細セグメント</a>を使ってGAに記憶させれば、25～45歳男性（子持ち）セグメントが18～25歳女性(子供もなし)セグメントよりも購入動機が強いかどうかといったことを、君は理解できるだろう。

<!--more-->
<h3>Google Analytics は既に持ってなかったけ？</h3>
"カスタム変数"以前、"ユーザー定義"というのがあったんだ。ここで注目したいのは1つのセグメント vs. 複数の変数ということ。かつてこの機能で１つ以上の値を持とうとすると、<a href="http://www.lunametrics.com/blog/2008/04/17/stuff-more-than-one-value-in-gas-user-defined-segment/">いろいろめんどくさいことをしなければならなかったんだ</a>。けれども、現在カスタム変数を使用すれば君は簡単に複数の値を持つことができる。

（※注　以前のユーザー定義を使用していても、Google はこの機能をすぐに廃止するとはアナウンスしなかった。しかし、明らかにカスタム変数はこの機能をに取って代わるものだ。）
<h3 id="scopes_and_how_to_use_them">使用方法とスコープ</h3>
僕らはカスタム変数のテクニカルな内容について話すつもりはない（この後の記事は別にして）。しかし、スコープと呼ばれるこの重要なプロパティについて話そうと思っている。

スコープは基本的にGoogle Analyticsにおける詳細レベルを指し示しており、それらは必ず適用されなければならない。スコープは<strong>ビジター</strong>、<strong>セッション</strong>、もしくは<strong>ページビュー</strong>のどれかだ。

<strong>ビジター</strong>レベル変数はユーザー定義にそっくりだ。ユーザーのクッキーに記録されサイトを訪れる度に適用される。このスコープはユーザーの本質的な性質、少なくとも半永久的なものを定義するのに最適だ。以下のようなものを記録するとよいでだろう。
<ul>
	<li>人口統計的な情報：年齢、性別、収入、家族構成、職業など</li>
	<li>顧客情報：会員、購読者、ゴールドメンバーといったもの</li>
	<li>最初の参照情報：どのように私たちを見つけたのか</li>
</ul>
<strong>セッション</strong>レベル変数は1つのセッションだけに適用される。この変数はセッション中に起きる特定のアクションを記録するのに適している。例えば以下のようなもの。
<ul>
	<li>商品をショッピングカートに入れた</li>
	<li>サイトの特定のセクションを閲覧した</li>
</ul>
<strong>ページビュー</strong>レベル変数で記録できるのは1回のページビューの間だけだ。以下のようなものに適用できるかもしれない。
<ul>
	<li>"お気に入り" ボタンを押した</li>
	<li>記事を友達に知らせた</li>
	<li>ページ内で別のタブを閲覧した</li>
</ul>
（※注 ページビューレベル変数は、<a href="http://t32k.me/mol/2009/09/google-analytics-event-tracking-guide/">イベントトラッキング</a>と場合によっては重複する部分があるかもしれない。どちらのモデルがユーザーのアクションをよりよく記録できるかは、君次第だ。）
<h3>カスタ変数についてもっと詳しく</h3>
今回、なぜカスタム変数を使用したらよいのか理解できたと思うので、次回は実際の使用方法について説明しようと思う。もう少しで次のシリーズの記事を書くのでチェックしてくれ！
