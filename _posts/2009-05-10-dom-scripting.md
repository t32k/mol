---
layout: post
title: DOMから始めるJavaScriptモダン・スクリプティング　6 〜9回まで
categories:
- javascript
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/05/dom-scripting-futomi-02.html
  _edit_last: '1'
  pvc_views: '4179'
---
<a href="http://itpro.nikkeibp.co.jp/article/COLUMN/20070626/275913/">DOMから始めるJavaScriptモダン・スクリプティング</a> より
サイ本はちょっと休憩
<h5>イベントハンドラ</h5>
<pre><code>HTML要素内にイベントハンドラをセットする場合
&lt;div id="box" onclick="javascript:alert('Clicked!')"&gt;hogehoge&lt;div&gt;</code></pre>
<pre><code>↑はHTML内にJSのコードが混在するので分離。
window.onload = function() {
var box = document.getElementById('box');
box.onclick = function() {
alert("Clicked!");
　}
};</code></pre>
windowオブジェクトにonloadイベントハンドラをセットすることで，HTMLがブラウザにロードされてから実行したい処理を指定することができる。
<h5>イベントハンドラの問題点</h5>
<pre><code>HTML
&lt;script type="text/javascript" src="cs1.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="cs2.js"&gt;&lt;/script&gt;

cs1.js
window.onload = function() { alert('cs1');}

cs2.js
window.onload = function() { alert('cs2');}</code></pre>
イベントハンドラは，同じ要素に同じイベントハンドラを複数定義しようとすると，後から定義したもので上書きされてしまう。だから上のコードは<span style="font-weight: bold;">'cs2'としかアラートされない。
複数の人間で広範囲・複雑な処理をJSで開発すると考えればこれは無視できない問題。
<h5>イベントハンドラからW3C DOMイベントモデルへ</h5>
<pre><code>&lt;div id="outer"&gt;
　外側のボックス
　&lt;div id="inner"&gt;
　　内側のボックス
　&lt;/div&gt;
&lt;/div&gt;</code></pre>
キャプチャーフェーズ→ターゲットフェーズ→バブリングフェーズ
W3C DOMイベントモデルではドキュメントツリーの上からイベント発生源まで伝搬し、そして今度は逆の方向に伝搬するという概念を持っています。イベントは，そのイベントが発生した部分だけでしか認識されないわけではない
<h5>イベント・リスナ</h5>
<span style="font-weight: bold;">addEventListener(<span style="font-style: italic;">イベント、<span style="font-style: italic;">処理、<span style="font-style: italic;">フェーズ)
フェーズ
<ul>
	<li><span style="font-weight: bold;">true：キャブチャーフェーズ</span></li>
	<li><span style="font-weight: bold;">false：バブリングフェーズ</span></li>
</ul>
<h5>ブラウザの互換性</h5>
<ul>
	<li><span style="font-weight: bold;">IEはaddEventListenerに対応していない</span></li>
	<li><span style="font-weight: bold;">キャプチャーフェーズすらない</span></li>
	<li>IEは独自の<span style="font-weight: bold;">attachEventメソッドを使用</span></li>
</ul>
<h5>クロスブラウズ対策のイベントリスナ</h5>
<pre><code>var addListener = function(elm, type, func) {
if (! elem) { return false; }
if (elm.addEventListener) { /* W3C準拠ブラウザ */
elm.addEventListener(type, func, false);
} else if(elem.attachEvent) { /* IE用 */
elem.attachEvent('on' +type. func);
} else {
return false;
}
return true;
};</code></pre>
addListenerという関数オブジェクトを事前に用意
バブリング・フェーズのみで処理する仕組み
<pre><code>var div = document.getElemenetById('box');
var popup = function() { alert('clicked!'); };
addlistener(div, "click", popup);</code></pre>
<h5>JavaScriptの完全分離</h5>
<pre><code>&lt;div id="box"&gt;××××&lt;/div&gt;</code></pre>
id属性に"box"がセットされたdiv要素をマウスでクリックしたら"clicked!"と表示されたアラートウィンドをポップアップさせるアプリケーションを想定します。
<pre><code>/* イベント・リスナのセット関数オブジェクトを定義 */
var addListener = function(elem, type, func) {
　if(! elem) { return  false; }
　if(elem.addEventListener) { /* 準拠用 */
　　elem.addEventListener(type, func, false);
　} else if (elem.attachEvent) { /* IE用 */
　  elem.attachEvent('on'+type, func);
　} else {
return false;
　}
　return true;
};

/* HTMLがブラウザにロードされたときに実行する処理 */
var init = function() {
　var div = document.getElementById('box');
　var popup = function() { alert("clicked!"); };
　addListener(div, "click", popup);
};

/* windowオブジェクトにloadイベントが発生したらinit関数を実行 */
addListener(window, "load", init);</code></pre>
この枠組みを簡単に整理すると，次のようになる。
<pre><code>/* イベント・リスナのセット関数オブジェクトを定義 */
var addListener = function(elem, type, func) {...};

/* HTMLがブラウザにロードされたときに実行する処理 */
var init = function)() {
/* ここに、実行させたいコードを記述*/
}

/* windowオブジェクトにloadイベントが発生したらinit関数を実行 */
addlistener(window, "load", init);</code></pre>
<h5>イベント・ハンドラの問題点の克服</h5>
<pre><code>/* イベント・リスナのセット関数オブジェクトを定義 */
var addListener = function(elem, type, func) {...};

/* HTMLがブラウザにロードされたときに実行する処理 */
var init = function)() {
　var div = document.getElementById('box');
　var popup1 = function() { alert("clicked1"); };
　addListener(div, "click", popup1);
　var popup2 = function() { alert("clicked2");};
　addListener(div, "click", popup2);
};

/* windowオブジェクトにloadイベントが発生したらinit関数を実行 */
addlistener(window, "load", init);</code></pre>
W3C DOMイベントモデルだとご覧のように同じ要素に対して複数イベントハンドラをセットできる。
<h5>jsファイルを処理ごとに分離する</h5>
<pre><code>HTML
&lt;script type="text/javascript" src="cs1.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="cs2.js"&gt;&lt;/script&gt;

cs1.js
var msg = 'cs1';
var init = function() { alert(msg); };
var addListener = function(...){...};
addListener(window, "load", init);

cs2.js
var msg = 'cs2';
var init = function() { alert(msg); };
var addListener = function(...) {...};
addListener(window, "load", init);</code></pre>
JavaScriptでは，jsファイルを分離したとしても，実際には，それらを一つに連結したものとして解釈される。故に上記のコードは変数msgがバッティングする。
<h5>オブジェクトによるラッピング</h5>
<pre><code>オブジェクトを定義
var obj = new Object();
/* mynameという名前のプロパティを定義 */
obj.myname = '太郎';
/* saynameという名前のメソッドを定義 */
obj.sayname = function() { alert(obj.myname); };


オブジェクトリテラルで定義
var obj = {
　myname: '太郎',
　sayname: function() {alert(obj.myname);}
};


オブジェクトに定義したメソッドの呼び出し方
obj.sayname(); /* 太郎 と表示されたアラート・ウィンドウがポップアップ */


さっきのサンプルをオブジェクトでラッピングする

cs1.js
var cs1 = {
　msg = 'cs1',
　init: function() { alert(cs1.msg); },
　addListener: function(...) {...}
};
cs1.addListener(window, "load", cs1.init);

cs2.js
var cs2 = {
　msg = 'cs1',
　init: function() { alert(cs1.msg); },
　addListener: function(...) {...}
};
cs1.addListener(window, "load", cs1.init);</code></pre>
こうすることで、変数の重複を防げる！
<h5>使い回せるコード</h5>
さっきのコードを改良
<pre><code>HTML
&lt;script type="text/javascript" src="dom.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="cs1.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="cs2.js"&gt;&lt;/script&gt;


dom.js
var dom = {
addListener: function(elem, type, func) {
if(! elem) { return false; }
if(elem.addEventListener) { /* W3C用 */
elem.addEventListner(type, func,  false);
} else if (elem.attachEvent) {/* IE用 */
elm.attachEvent('on' +type, func);
} else {
return true;
}
};


cs1.js
var cs1 = {
msg: 'cs1',
init: function() { alert(cs1.msg); }
};
dom.addListener(window, "load", cs1.init);


cs2.js
var cs2 = {
msg: 'cs2',
init: function() { alert(cs1.msg); }
};
dom.addListener(window, "load", cs1.init);</code></pre>
dom.jsにメソッドを追加する場合は，次のように記述
<pre><code>var dom = {
　addListener: function(elm, type, func) {
　　...
　},
　removeListener: function(...) {
　　...
　},
　removeChildNodes: function(...) {
　　...
　}
};<span style="font-family: sans-serif;">
</span></code></pre>
<h5>Unobtrusive Scripting</h5>
でしゃばらない 〜 JavaScriptの完全分離 〜
<ul>
	<li>Behavior : JavaScript</li>
	<li>Prezentation : CSS</li>
	<li>Content : HTML</li>
</ul>
<h5>BehaviorにPresentationが混在した例</h5>
<pre><code>HTML
&lt;div id="box"&gt;&lt;/div&gt;

JavaScript
var box = document.getElementById("box");
box.style.backgroundColor = "#ffeeee";
box.style.border = "1px solid #4c4c4c";
box.style.color = "dd8888";
box.style.fontWeight = "bold";</code></pre>
上記はBehaviorであるJSにPrezentationのCSSの設定が混在してる、良くない！
<h5>BehaviorとPresentationを分離した例</h5>
<pre><code>CSS
.boxstyle2 {
background-color: #ffeeee;
・・・
}

JavaScript
var box = document.getElementById("box");
box.className = "boxstyle2";</code></pre>
あらかじめスタイルを設定しておき、class名を変更する方法。
てかContentが王様なのでJavaScriptは「わき役」に徹するべき。
<pre><code>&lt;a href="javascript:history.back()" id="bk"&gt;戻る&lt;/a&gt;</code></pre>
これはJSオフ時には何も動作しないので良くない！
<pre><code>&lt;a href="../index.html" id="bk"&gt;戻る&lt;/a&gt;


/* イベントリスナーをセットする処理 */
var addListener = function(elm, type, func) {
　if(! elm) { return false; }
　if(elm.addEventListener) { /* W3C準拠ブラウザ用 */
　　elm.addEventListener(type, func, false);
　} else if(elm.attachEvent) { /* Internet Explorer用 */
　　elm.attachEvent('on'+type, func);
　} else {
　　return false;
　}
　return true;
};

/* HTMLがブラウザにロードされたときに実行する処理 */
var init = function() {
/* a要素のノードオブジェクト */
var bk = document.getElementById("bk");
/* 前ページに移動する処理関数 */
var backLink = function(evt) {
　history.back();
　if(evt.preventDefault) { evt.preventDefault(); }
　return false;
};
/* a要素にclickイベントのリスナーをセット */
addListener(bk, "click", backLink);
};
addListener(window, "load", init);</code></pre>
JavaScriptが動作しないブラウザに対しては固定的ではあるものの，リンクという機能は提供できる！

TODO
<ul>
	<li>バブリングフェーズとかよくわかんない！</li>
</ul></span></span></span></span></span>
