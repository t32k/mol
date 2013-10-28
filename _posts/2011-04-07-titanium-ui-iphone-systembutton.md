---
layout: post
title: Titanium.UI.iPhone.SystemButton
categories:
- Titanium Mobile
tags:
- iphone
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '25694'
  _aioseop_description: "var button = Titanium.UI.createButton({\r\n       systemButton:
    Titanium.UI.iPhone.SystemButton.CAMERA\r\n});"
---
<a href="http://t32k.me/mol/file/2011/04/Titanium.UI_.iPhone.SystemButton.png"><img class="alignleft size-medium wp-image-2818" title="Titanium.UI.iPhone.SystemButton" src="http://t32k.me/mol/file/2011/04/Titanium.UI_.iPhone.SystemButton-160x300.png" alt="" width="160" height="300"/></a>

みなさん、タイタンやってまっかぁ？わい？ わいタイタンやで(・∀・)ｲｲ!!

てことで、先週 <a href="http://m2.cap-ut.co.jp/un/">Untitled!!!!!!!! </a>で講演してきたわけですが、Twitterでの反響を見てますとTitanium Mobileやってみたい！って声もちらほら見受けられて、僕も話して良かったと感じていますです。で、皆さんはこれからTitanium勉強して僕におしえてくっさい！

そんなわけで、今回は自分的にメモ的なメモ。Titanium Mobile はネィティブなUIが使えますので、それをフル活用していこうぜってのが今回のエントリの主旨。

<!--more-->

ボタンとかアイコン作ったりするのめんどいので、システムボタン使おーぜってことす。そのほうが下記コードのような感じで、プロパティの部分が1行で定義できたり、組み込みのアプリと同じ振る舞いをするだろうとユーザーも理解しやすいだろうってことです。さて、そのシステムボタン、どんなのあるのか一覧にしてみた。文字だけじゃ分からないのでキャプチャ撮った。
<pre><code>var button = Titanium.UI.createButton({
       systemButton: Titanium.UI.iPhone.SystemButton.CAMERA
});</code></pre>
上記画像のコードはGistに貼っておいたので、シュミレータで確認してみるのOKかと。
<ul>
	<li><a href="https://gist.github.com/905474">A set of constants for the system button style for buttons. — Gist</a></li>
</ul>
<h2>Titanium.UI.iPhone.SystemButton</h2>

<strong>ACTION</strong>
<a href="http://t32k.me/mol/file/2011/04/ACTION.png"><img style="vertical-align: middle;" title="ACTION" src="http://t32k.me/mol/file/2011/04/ACTION.png" alt="" width="42" height="38"/></a> アクションアイコン。toolbarとnavbarでのみ使用可能。

<strong>ACTIVITY</strong>
<img style="vertical-align: middle;" title="ACTIVITY_SPINNER" src="http://t32k.me/mol/file/2011/04/ACTIVITY_SPINNER.png" alt="" width="42" height="38"/> アクティビティインディケーターを表す特別なスタイル。

<strong>ADD</strong>
<img style="vertical-align: middle;" title="ADD" src="http://t32k.me/mol/file/2011/04/ADD.png" alt="" width="42" height="38"/> 追加アイコン。toolbarとnavbarでのみ使用可能。

<strong>BOOKMARKS</strong>
<img style="vertical-align: middle;" title="BOOKMARKS" src="http://t32k.me/mol/file/2011/04/BOOKMARKS.png" alt="" width="42" height="38"/> ブックマークアイコン。toolbarとnavbarでのみ使用可能。

<strong>CAMERA</strong>
<img style="vertical-align: middle;" title="CAMERA" src="http://t32k.me/mol/file/2011/04/CAMERA.png" alt="" width="42" height="38"/> カメラアイコン。toolbarとnavbarでのみ使用可能。

<strong>CANCEL</strong>
<img style="vertical-align: middle;" title="CANCEL" src="http://t32k.me/mol/file/2011/04/CANCEL.png" alt="" width="70" height="38"/> キャンセルアイコン。ローカライズ。toolbarとnavbarでのみ使用可能。

<strong>COMPOSE</strong>
<img style="vertical-align: middle;" title="COMPOSE" src="http://t32k.me/mol/file/2011/04/COMPOSE.png" alt="" width="42" height="38"/> 作成アイコン。toolbarとnavbarでのみ使用可能。

<strong>CONTACT_ADD</strong>
<img style="vertical-align: middle;" title="CONTACT_ADD" src="http://t32k.me/mol/file/2011/04/CONTACT_ADD.png" alt="" width="42" height="38"/> 青色のプラスアイコン。

<strong>DISCLOSURE</strong>
<img style="vertical-align: middle;" title="DISCLOSURE" src="http://t32k.me/mol/file/2011/04/DISCLOSURE.png" alt="" width="42" height="38"/> 開示スタイルアイコン。

<strong>DONE</strong>
<img style="vertical-align: middle;" title="DONE" src="http://t32k.me/mol/file/2011/04/DONE.png" alt="" width="70" height="38"/> 完了アイコン。ローカライズ。toolbarとnavbarでのみ使用可能。

<strong>EDIT</strong>
<img style="vertical-align: middle;" title="EDIT" src="http://t32k.me/mol/file/2011/04/EDIT.png" alt="" width="70" height="38"/> 編集アイコン。ローカライズ。toolbarとnavbarでのみ使用可能。

<strong>FAST_FORWARD</strong>
<img style="vertical-align: middle;" title="FAST_FORWARD" src="http://t32k.me/mol/file/2011/04/FAST_FORWARD.png" alt=""/> 早送りアイコン。toolbarとnavbarでのみ使用可能。

<strong>INFO_DARK</strong>
<img style="vertical-align: middle;" title="INFO_DARK" src="http://t32k.me/mol/file/2011/04/INFO_DARK.png" alt="" width="42" height="38"/> 暗めの情報アイコン。

<strong>INFO_LIGHT</strong>
<img style="vertical-align: middle;" title="INFO_LIGHT" src="http://t32k.me/mol/file/2011/04/INFO_LIGHT.png" alt="" width="42" height="38"/> 明るめの情報アイコン。

<strong>ORGANIZE</strong>
<img style="vertical-align: middle;" title="ORGANIZE" src="http://t32k.me/mol/file/2011/04/ORGANIZE.png" alt="" width="42" height="38"/> オーガナイズアイコン。toolbarとnavbarでのみ使用可能。

<strong>PAUSE</strong>
<img style="vertical-align: middle;" title="PAUSE" src="http://t32k.me/mol/file/2011/04/PAUSE.png" alt="" width="42" height="38"/> 停止アイコン。toolbarとnavbarでのみ使用可能。

<strong>PLAY</strong>
<img style="vertical-align: middle;" title="PLAY" src="http://t32k.me/mol/file/2011/04/PLAY.png" alt="" width="42" height="38"/> 再生アイコン。toolbarとnavbarでのみ使用可能。

<strong>REFRESH</strong>
<img style="vertical-align: middle;" title="REFRESH" src="http://t32k.me/mol/file/2011/04/REFRESH.png" alt="" width="42" height="38"/> 更新アイコン。toolbarとnavbarでのみ使用可能。

<strong>REPLY</strong>
<img style="vertical-align: middle;" title="REPLY" src="http://t32k.me/mol/file/2011/04/REPLY.png" alt="" width="42" height="38"/> 返信アイコン。toolbarとnavbarでのみ使用可能。

<strong>REWIND</strong>
<img style="vertical-align: middle;" title="REWIND" src="http://t32k.me/mol/file/2011/04/REWIND.png" alt="" width="42" height="38"/> 巻き戻しアイコン。toolbarとnavbarでのみ使用可能。

<strong>SAVE</strong>
<img style="vertical-align: middle;" title="SAVE" src="http://t32k.me/mol/file/2011/04/SAVE.png" alt="" width="70" height="38"/> 保存アイコン。toolbarとnavbarでのみ使用可能。

<strong>SPINNER</strong>
<img style="vertical-align: middle;" title="SPINNER" src="http://t32k.me/mol/file/2011/04/ACTIVITY_SPINNER.png" alt="" width="42" height="38"/> アクティビティと同じ。

<strong>STOP</strong>
<img style="vertical-align: middle;" title="STOP" src="http://t32k.me/mol/file/2011/04/STOP.png" alt="" width="42" height="38"/> 中止アイコン。toolbarとnavbarでのみ使用可能。

<strong>TRASH</strong>
<img style="vertical-align: middle;" title="TRASH" src="http://t32k.me/mol/file/2011/04/TRASH.png" alt="" width="42" height="38"/> ゴミ箱アイコン。toolbarとnavbarでのみ使用可能。

<strong>FIXED_SPACE,　FLEXIBLE_SPACE</strong>
あとボタンじゃないけど、createButtonで生成する空白スペース。FIXEDが固定スペースで任意のWidthも指定。FLEXIBLEはええ感じに等間隔な感じで調整してくれるナイススペース。
<pre><code>// 固定スペース
var fixed = Titanium.UI.createButton({
    systemButton: Titanium.UI.iPhone.SystemButton.FIXED_SPACE,
    width: '40'
});

// 可変スペース
var flexible = Titanium.UI.createButton({
    systemButton: Titanium.UI.iPhone.SystemButton.FLEXIBLE_SPACE
});</code></pre>
<h3>参照</h3>
<ul>
	<li><a href="http://developer.appcelerator.com/apidoc/mobile/1.6.0/Titanium.UI.iPhone.SystemButton-object">Appcelerator Developer Center - API for Titanium.UI.iPhone.SystemButton (version 1.6.0)</a></li>
</ul>
