---
layout: post
title: Titanium Mobile でCSS的な、それJSS!!!!!!
categories:
- Titanium Mobile
tags:
- Titanium
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '10665'
  _aioseop_description: とにかく信じられない。
---
<a href="http://en.wikipedia.org/wiki/CSS_(band)"><img title="CSSとは、サンパウロ出身のブラジリアンロックバンドです。" src="/static/blog/2011/03/css.jpg" alt="" width="470" height="270" /></a>

Titanium Mobile での開発は当然JavaScriptオンリーですので、愛も憎しみもすべてこの中にではなくて、コンテンツであったり見た目の情報であったり振る舞いであったり全てJavaScript の中に書かれているわけです。

Webサイト制作ではあれば、HTML(content) + CSS(presentation) + JavaScript (behavior)のように役割を分けて制作するのが良いと言われております。JavaScriptオンリーのTitaniumでも然りです。せめてロジックとUIが分けることができれば、エンジニアさんとデザイナーさんが分業できるってもんです。

<!--more-->

<strong>あるよ(・∀・)！CSSあるよ(・∀・)！それJSSでできるよ(・∀・)！</strong>
<h3>JavaScript Stylesheets</h3>
てことで、Titanium Mobile 1.5以上の環境でなら、JavaScript StylesheetsなるJSSというものがありまして、CSSプロパティを使った、CSSライクな記述で任意の要素に対してスタイルを当てることが可能です。スタイルを分離したいJSファイル名と同名のJSSファイルに記述すれば勝手に認識してくれます。

app.js  &lt;--&gt; app.jss

hoge.js &lt;--&gt; hoge.jss

fuga.js  &lt;--&gt; fuga.jss

↑こんな感じの対応になってますので、わざわざ、&lt;link rel="stylesheet"  href="app.jss"&gt;とか読み込みのための記述を書く必要はないです。
<pre><code>//----------------- app.js
var window = Ti.UI.createWindow({
   id:"w"
});
var button = Ti.UI.createButton({
   id:"b",
   title:"Hello"
});
window.add(button);
window.open();</code></pre>
↑このJSファイルに対して↓このJSSファイルのスタイルがききます。
<pre><code>/*----------------- app.jss */
#w {
  background-color:"red";
}
button {
  width:100px;
  height:40px;
}</code></pre>
app.android.jssやapp.iphone,.jssのようにAndroid/iPhone用にJSSファイルを切り分けることができます。

また、global.jssのように全てのJSファイルにスタイルを当てることができます。

おー素晴らしいねって思ったけど、本当のCSSのような動きを期待すると結構意図せぬ挙動が多くてゲンナリします。

以下、とりとめなくかきつらねてみるとかしてみるとか。
<h3>Titanium Mobile 1.6.1 + iOS SDK 4.3 での検証</h3>
<ul>
	<li>global.jssが動かない（ <a href="https://appcelerator.lighthouseapp.com/projects/32238-titanium-mobile/tickets/3011">3011 iOS: JSS global.jss not supporrted</a> ）</li>
	<li>Resources/lib/app.jssのように、対象のJSファイルが同一ディレクトリになくても動く</li>
	<li>text-alignがtextAlignでも動く</li>
	<li>空のスタイル（プロパティと値のないセレクタ EX. #hoge{}）を書くとそれ以降のスタイルが適用されない</li>
	<li>単一セレクタしか認識しない（button.barとか無理）</li>
	<li>ショートハンド無理っぽい</li>
	<li>CSS以外のものも動く（EX. text: "iPhone!"）</li>
	<li>同一セレクタの場合、iphone.jssの方が強い。でもなんか微妙。。(下記表参照)</li>
	<li>ドキュメント少ない（サンプル少ない）</li>
	<li>というかサンプルのコードが正しく動かない</li>
	<li>CSSプロパティの値は文字列なのか数値でクオーテーションで囲まないといけないのかそうでないのかよくわからない。</li>
	<li>JSSファイルをダブルクリックするとVLCプレイヤーが立ち上がってイラっとする。</li>
	<li>JSとJSS絶対ごっちゃになる、空目率隆史。</li>
	<li>とにかく信じられない。</li>
</ul>
<table border="0" width="370">
<tbody>
<tr>
<th style="background-color: #aaa;" scope="col">app.jss</th>
<th style="background-color: #aaa;" scope="col">app.iphone.jss</th>
</tr>
<tr>
<td>× type-based</td>
<td>◯ type-based</td>
</tr>
<tr>
<td>× class-based</td>
<td>◯ class-based</td>
</tr>
<tr>
<td>× id-based</td>
<td>◯ id-based</td>
</tr>
<tr>
<td>× class-based</td>
<td>◯ type-based</td>
</tr>
<tr>
<td>◯ id-based</td>
<td>× type-based</td>
</tr>
<tr>
<td>◯ id-based</td>
<td>× class-based</td>
</tr>
<tr>
<td>× class-based</td>
<td>◯ id-based</td>
</tr>
</tbody>
</table>
とまぁ、そんなかんじで、現時点ではJSSは使いこなすには難があるなーといった印象ですな。1.7,1.8くらいまで待つか。。。
それか独自UIボタンなどはあきらめて、ネィティブのシステムボタンをフルに使って記述量減らすとか。

<a href="http://higelog.brassworks.jp/?p=1144">ひげろぐさんのよう</a>にスタイル用のJSファイルを必要に応じてincludeするやり方が今のところの現実解なのかもしれません。。
<ul>
	<li><a href="http://higelog.brassworks.jp/?p=1307">TitaniumのJSSという機能 | ひげろ</a>ぐ</li>
	<li><a href="http://wiki.appcelerator.org/display/guides/Designing+the+User+Interface#DesigningtheUserInterface-CrossplatformlayoutusingJSS">Designing the User Interface - Documentation Guides - Appcelerator Wiki</a></li>
</ul>
英語だけどここの質問にJSS関連の情報がいっぱいあるような。。
<ul>
	<li><a href="http://fx-gp.seesaa.net/article/179363988.html">第２回ウェブセミナー What's New in #Titanium Mobile 1.5 まとめ | 開発</a></li>
</ul>
そんなわけで、みんなもれっつたいたん！
