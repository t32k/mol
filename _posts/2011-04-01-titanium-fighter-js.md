---
layout: post
title: Titanium Mobile でjQuery的な、それTiFighter!!!!!!!
categories:
- Titanium Mobile
tags:
- Titanium
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '8777'
  _aioseop_description: それでもjQueryに恋に恋焦がれ恋に泣いた方であれば、せめて、jQueryライクにコードを記述できればと思われるかもしれません。
---
<a href="http://www.imdb.com/title/tt0137523/"><img class="fig" title="『ファイト・クラブ』（Fight Club）は、1999年製作のアメリカ映画。日本では1999年12月11日に20世紀フォックス配給により、日比谷映画他、全国東宝洋画系にて公開された。チャック・パラニューク（Chuck Palahniuk）の同名小説の映画化。" src="http://t32k.me/mol/file/2011/03/fc.jpg" alt="Fight Club" width="470" height="250" /></a>

みなさんタイタンしてますか、わたし？わたしタイタイ(・∀・)！

てことで、前回はCSS的な話でしたが今回はjQuery的なお話。デザイナーであれば、jQueryの便利さに狂喜乱舞し使用したことが一度はあるのではないでしょうか？というか、JavaScriptってjQueryのことじゃないの？っていう方もいるかもしれません。
<!--more-->

当然、jQuery大好きっこであれば、Titanium Mobileでも使いたいと思うのが当然の考えでしょう。でも、Titanium MobileでjQueryをインクルードしますと、ビルドエラーが起こります。はい、documentとかDOMってモデルがないからですね。なので、使えません。

どうしても、使いたいという方は以下のリソースを参考にされると良いかも知れません。
<ul>
	<li><a href="http://higelog.brassworks.jp/?p=1148">TitaniumでjQueryを使う | ひげろぐ</a></li>
</ul>
個人的にはjQueryを使う利点はDOM操作のしやすさとクロスブラウザ対応を考えなくてよいことの2点だと考えています。Titanium Mobileにおいて、前者はそもそもDOM自体がないですし、後者はJavaScript 1.6に対応していますのでモダンブラウザ並の環境でクロスプラットフォームに関してはTitanium側がやってくれることですし、これまた特に考える必要がありません。

てことで、jQueryを使う意味があまりないのですが、それでもjQueryに恋に恋焦がれ恋に泣いた方であれば、せめて、jQueryライクにコードを記述できればと思われるかもしれません。

<strong>あるよ(・∀・)！jQueryあるよ(・∀・)！それTiFighterでできるよ(・∀・)！</strong>
<h3>TiFighter</h3>
てことで、TiFighterの説明をします。<a href="http://twitter.com/#!/itspriddle">@itspriddle</a>さんが作ったti-helper.jsを自身でさらに拡張し、Titanium Mobile上でjQueryライクで記述可能にしたのがti-fighter.jsというライブラリです。
<ul>
	<li><strong><a href="https://github.com/itspriddle/ti-fighter">itspriddle/ti-fighter - GitHub</a></strong></li>
</ul>
<a href="https://github.com/itspriddle/ti-fighter"></a>
Githubから落としてきて任意のディレクトリに配置
<pre><span style="color: #888888;">// TiFighterの読み込み</span>
Ti.include('lib/ti-fighter.js');

<span style="color: #888888;">// オブジェクトの生成とTiFighterのインスタンスを生成</span>
var my_window = Ti.Ui.createWindow();
var w = TiFighter('my_window');

<span style="color: #888888;">//TiFighterのメソッドで操作</span>
w.attr('title', 'My Window');
w.close();</pre>
そのほかに、以下のようなメソッドが使えます。(* elはTiFighterのインスタンス)
<ul style="column-count: 2;-webkit-column-count: 2;-moz-column-count: 2;">
	<li>el.bind</li>
	<li>el.unbind</li>
	<li>el.trigger</li>
	<li>el.click</li>
	<li>el.focus</li>
	<li>el.blur</li>
	<li>el.add</li>
	<li>el.remove</li>
	<li>el.hide</li>
	<li>el.show</li>
	<li>el.animate</li>
	<li>el.attr</li>
	<li>el.text</li>
</ul>
ユーティリティ関数も豊富
<ul style="column-count: 2;-webkit-column-count: 2;-moz-column-count: 2;">
	<li>TiFighter.console</li>
	<li>TiFighter.alert</li>
	<li>TiFighter.each</li>
	<li>TiFighter.map</li>
	<li>TiFighter.extend</li>
	<li>TiFighter.config</li>
	<li>TiFighter.development</li>
	<li>TiFighter.production</li>
	<li>TiFighter.iphone</li>
	<li>TiFighter.ipad</li>
	<li>TiFighter.android</li>
	<li>TiFighter.strftime</li>
	<li>TiFighter.relatizeDate</li>
	<li>TiFighter.trim</li>
	<li>TiFighter.isset</li>
	<li>TiFighter.ajax</li>
	<li>TiFighter.get</li>
	<li>TiFighter.post</li>
	<li>TiFighter.put</li>
	<li>TiFighter.del</li>
	<li>TiFighter.rater</li>
</ul>
拡張も可能ってことで、jQueryのプラグインみたいに書けますね。
<pre>TiFighter.fn.title = function(title) {
  if (title) {
    return this.attr('title', title);
  } else {
    return this.attr('title');
  }
};
var label = Ti.UI.createLabel({ title: "Hello!" });
<span style="color: #888888;">// Hello</span>
TiFighter(my_label).title() ;
<span style="color: #888888;">// label.title is now 'Goodbye'</span>
TiFighter(my_label).title('Goodbye');</pre>
そんなわけで、僕はjQuery全然分からないので大した説明もできていないのですが、たぶん開発スピードが上がるのでしょう。
