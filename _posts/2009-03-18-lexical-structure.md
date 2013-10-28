---
layout: post
title: JavaScript 第5版 2章 字句構造
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
  blogger_permalink: /2009/03/lexical-structure.html
  _edit_last: '1'
  pvc_views: '1882'
---
<ul>
	<li>JavaScriptはキーワード、変数、関数名、識別子で大文字、小文字区別する</li>
	<li>空白、タブ、改行は無視される</li>
	<li>セミコロンは文と文の区切りを示す</li>
	<li><code>// 単一行コメント</code></li>
	<li><code>/* 複数行コメント */</code></li>
	<li>リテラルとはJavaScriptでプログラムに直接記述するデータの値のこと</li>
	<li>識別子とは名前のこと（先頭の文字はUnicode文字、アンダースコア、ドル記号じゃないとだめ、後は数字もいい）</li>
	<li>予約語とはJavaScriptで特別な意味をもつ単語で、言い換えるならばJavaScript構文そのものに含まれる</li>
</ul>
<h2>JavaScriptの予約語</h2>
<ul>
	<li><code>break</code></li>
	<li><code>case</code></li>
	<li><code>catch</code></li>
	<li><code>continue</code></li>
	<li><code>default</code></li>
	<li><code>delete</code></li>
	<li><code>do</code></li>
	<li><code>else</code></li>
	<li><code>false</code></li>
	<li><code>finally</code></li>
	<li><code>for</code></li>
	<li><code>function</code></li>
	<li><code>if</code></li>
	<li><code>in</code></li>
	<li><code>instanceof</code></li>
	<li><code>new</code></li>
	<li><code>null</code></li>
	<li><code>return</code></li>
	<li><code>switch</code></li>
	<li><code>this</code></li>
	<li><code>throw</code></li>
	<li><code>true</code></li>
	<li><code>try</code></li>
	<li><code>typeof</code></li>
	<li><code>var</code></li>
	<li><code>void</code></li>
	<li><code>while</code></li>
	<li><code>with</code></li>
</ul>
<h2>ECMA拡張用の予約語</h2>
<ul>
	<li><code>abstract</code></li>
	<li><code>boolean</code></li>
	<li><code>byte</code></li>
	<li><code>char</code></li>
	<li><code>class</code></li>
	<li><code>const</code></li>
	<li><code>debugger</code></li>
	<li><code>double</code></li>
	<li><code>enum</code></li>
	<li><code>export</code></li>
	<li><code>extends</code></li>
	<li><code>final</code></li>
	<li><code>float</code></li>
	<li><code>goto</code></li>
	<li><code>implements</code></li>
	<li><code>import</code></li>
	<li><code>int</code></li>
	<li><code>interface</code></li>
	<li><code>long</code></li>
	<li><code>native</code></li>
	<li><code>package</code></li>
	<li><code>private</code></li>
	<li><code>protected</code></li>
	<li><code>public</code></li>
	<li><code>short</code></li>
	<li><code>static</code></li>
	<li><code>super</code></li>
	<li><code>synchronized</code></li>
	<li><code>throws</code></li>
	<li><code>transient</code></li>
	<li><code>volatil</code></li>
</ul>
<h2>そのほかの避けたい識別子</h2>
<ul>
	<li><code>arguments</code></li>
	<li><code>Array</code></li>
	<li><code>Boolean</code></li>
	<li><code>Date</code></li>
	<li><code>decodeURI</code></li>
	<li><code>decodeURIComponent</code></li>
	<li><code>encodeURI</code></li>
	<li><code>Error</code></li>
	<li><code>escape</code></li>
	<li><code>eval</code></li>
	<li><code>EvalError</code></li>
	<li><code>Infinity</code></li>
	<li><code>isFinite</code></li>
	<li><code>isNaN</code></li>
	<li><code>Math</code></li>
	<li><code>NaN</code></li>
	<li><code>Function</code></li>
	<li><code>Object</code></li>
	<li><code>parseFloat</code></li>
	<li><code>parseInt</code></li>
	<li><code>RangeError</code></li>
	<li><code>ReferenceError</code></li>
	<li><code>Number</code></li>
	<li><code>String</code></li>
	<li><code>SyntaxError</code></li>
	<li><code>TypeError</code></li>
	<li><code>undefined</code></li>
	<li><code>unescape</code></li>
	<li><code>RegExp URIError</code></li>
</ul>
