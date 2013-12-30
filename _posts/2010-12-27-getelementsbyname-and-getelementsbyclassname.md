---
layout: post
title: getElementsByName と getElementsByClassName
categories:
- javascript
tags:
- dom
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '7522'
  _aioseop_keywords: 'dom,document.getElementsByName '
  _aioseop_description: 最近というか先々々月ぐらいのことですが、document.getElementsByName なるものを知りました。このメソッドはどんなものかと言いますと...
---
ちょっと気になったのでメモメモ。

普段、jQueryなど使っているときは特に気にしなくてもいいのですが、フレームワークなしでなんかしらの要素取ってくるのって結構大変というか、document.getElementById しか頭に思いつかないのです。

最近というか先々々月ぐらいのことですが、document.getElementsByName なるものを知りました。このメソッドはどんなものかと言いますと、

<!--more-->
<blockquote>document.getElementsByName は、name 属性に与えられた値を持つ全ての要素の NodeList を返します。
<a href="https://developer.mozilla.org/ja/DOM/document.getElementsByName"><span style="font-size: x-small;">document.getElementsByName - MDC Doc Center</span></a></blockquote>
ほうほう、なるほど。でも、これと似たような名前のメソッドなかったけ？
<blockquote>document.getElementsByClassNameは、与えられたクラス名で得られる要素の集合を返します。
<a href="https://developer.mozilla.org/ja/DOM/document.getElementsByClassName"><span style="font-size: x-small;">document.getElementsByClassName - MDC Doc Center</span></a></blockquote>
おう、これこれ。でも getElementsByClassName のほうはＩＥ対応してないっぽいし、どんな要素にでもname属性つけれたら、getElementsByName で十分じゃね？という疑問が湧いてきたのですが、そうでもないみたいです。

HTML4.01でname属性が設定できるのは以下の要素だけ。
<blockquote>
<ul style="-moz-column-count: 3; -webkit-column-count: 3;">
	<li>a</li>
	<li>applet</li>
	<li>button</li>
	<li>form</li>
	<li>frame</li>
	<li>iframe</li>
	<li>img</li>
	<li>input</li>
	<li>map</li>
	<li>meta</li>
	<li>object</li>
	<li>param</li>
	<li>select</li>
	<li>textarea</li>
</ul>
<a href="http://www.mitsue.co.jp/glossary/html/attribute/name.html"><span style="font-size: x-small;">name属性 | HTML用語集 | ミツエーリンクス</span></a></blockquote>
ぷらす...
<blockquote>IE、Netscape系共通で使えるのは、JavaScriptの基礎部分でname指定取りができるHTMLタグに限られます。 IMG、FORM、FORM部品、などです。ま、時代的にname属性はフォーム以外ではあり得ない時代でもありますので、使えなくても差し支えないでしょう。

<a href="http://www.artemis.ac/contents/javascript/javascript11.htm#names"><span style="font-size: x-small;">初心者のJavaScript HTMLエレメントのオブジェクト指定方法 各種 [ ARTEMIS ] </span></a></blockquote>
つまり、&lt;div name="hoge"&gt;の要素をgetElementsByNameで取りたいと思っても必ずしも全てのブラウザで正常に動作することもないし、そもそも文法的にやっちゃだめてことで。。。

そうなってくると、どんな要素にでもclass属性がつけれるので、getElementsByClassName がやっぱり重要というか、こっちを使っていくほうがベターなんだと理解しました。

ちなみに、getElementsByClassNameの各ブラウザのサポート状況はこんな感じ。IE以外OKってな感じで。
<blockquote><a href="/static/blog/2010/12/gebcn.png"><img class="alignnone size-medium wp-image-2240" title="gebcn" src="/static/blog/2010/12/gebcn-300x50.png" alt="" width="550" /></a>

<a href="http://www.quirksmode.org/dom/w3c_core.html"><span style="font-size: x-small;">W3C DOM Compatibility - Core</span></a></blockquote>
ちなみに、似たような名前のメソッドでgetElementsByTagNameてのもある。
<ul>
	<li><a href="https://developer.mozilla.org/ja/DOM/document.getElementsByTagName">document.getElementsByTagName - MDC Doc Center</a></li>
</ul>
結論：jQueryないと僕生きていけません :(
