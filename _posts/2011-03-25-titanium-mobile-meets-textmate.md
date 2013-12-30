---
layout: post
title: TextMate で Titanium Mobile!!
categories:
- javascript
- Titanium Mobile
tags:
- Titanium
status: publish
type: post
published: true
meta:
  pvc_views: '7156'
  _edit_last: '1'
  _aioseop_description: 前回よりインストールしましたTitanium Developer 1.2.2ですがこれはIDE（統合開発環境）ではないです。ただビルドしてくれるだけですので、エディタは自前で用意しなければなりません。
---
<img class="alignnone size-full wp-image-2575" title="tt" src="/static/blog/2011/03/tt.png" alt="" width="468" height="135" />

<a href="http://t32k.me/mol/2011/03/hello-titanium-mobile/">前回</a>、インストールしました<a href="http://www.appcelerator.com/">Titanium Developer</a> 1.2.2ですがこれはIDE（統合開発環境）ではないです。ただビルドしてくれるだけですので、エディタは自前で用意しなければなりません。

普段、私が使っているエディタは<a href="http://macromates.com/">TextMate</a>ですので、Titanium Mobile用のBundle（拡張機能）ないかなぁと思ったら、案の定探したらありましたｗ
<ul>
	<li><a href="http://developer.appcelerator.com/blog/2010/06/titanium-mobile-textmate-bundle.html">Titanium Mobile TextMate Bundle « Appcelerator Developer Center</a></li>
</ul>
<!--more-->

<a href="http://jonathanstark.com/blog/">Jonathan Stark</a>さんや<a href="http://ejohn.org/category/blog/">John Resig</a>さんもそうでしたが、モバイル業界のエンジニアさんはTextMate愛用者が多いのかしら？

Gitからのインストール方法書いてありますが、よくわからんので困ったなと思ったらページ下部に手動でのインスコ方法書いてあったヽ(・∀・ )ﾉ
<ul>
	<li><a href="https://github.com/subtleGradient/JavaScript-Appcelerator-Titanium-Mobile.tmbundle">subtleGradient/JavaScript-Appcelerator-Titanium-Mobile.tmbundle - GitHub</a></li>
</ul>
<h3>インストール方法</h3>
<ol>
	<li>TextMate をインストールしましょう！(当たり前か...)</li>
	<li> <a href="http://github.com/subtleGradient/JavaScript-Appcelerator-Titanium-Mobile.tmbundle/zipball/master">JavaScript-Appcelerator-Titanium-Mobile.tmbundle.zip</a> をダンロード</li>
	<li>zip解凍</li>
	<li>解凍したフォルダの名前を ti-mo.tmbundle に変更
<ul>
	<li>.tmbundle として認識させたいだけなので名前に特別な意味はないです。</li>
</ul>
</li>
	<li>だぼーくりっく！！</li>
	<li>インストール JSON
<ul>
	<li>
<pre>sudo gem install json</pre>
</li>
</ul>
</li>
	<li>いんじょい！！</li>
</ol>
これなんでJSONインスコしてるんですかね？だれか教えてください！

とはいえ、無事インスコできたのでTextMateを開いてみるとファイル形式の部分に Titanium Mobile JavaScript と項目が新しく追加されています。
<h3>使い方</h3>
<img title="補完" src="/static/blog/2011/03/tb.png" alt="" width="470" height="162" />
<ul>
	<li>option + escape で補完</li>
	<li>option + F1 でツールチップ</li>
	<li>Ti. とタイプしても補完するよ（最終行だと出ないよ）</li>
	<li>inc + tab で <code>Ti.include()</code></li>
	<li>d + tab で <code>Ti.API.debug()</code></li>
</ul>
んなわけで、これで開発に集中できますね。というか私はまだサンプルコードを切り貼りしてる程度なので、そこまで特に必要なかった気もしないわけでもないですが....
<h3>Titanium Studio</h3>
最後にTextMateとは関係ないですが、Webデザイナーでもおなじみの <a href="http://www.aptana.com/">Aptana Studio</a> が、今年の1月にTitaniumを開発しているAppcelerator社に買収されたもんで、そのおかげで今月中にでもTitanium StudioなるIDEが出るそうです。こちらがリリースされたら、TextMateいらなくなるかも。いや重さにもよりますね。なににせよ待ち遠しいでっす（ゝω・）
<ul>
	<li><a href="https://skitch.com/appcelerator/">appcelerator | skitch.com</a></li>
</ul>
[追記]
<blockquote>And speaking of Aptana Studio 3, download it now if you haven’t already —<a href="http://aptana.com/products/studio3/download">http://aptana.com/products/studio3/download</a>. We’re also looking forward to integrating it into our Titanium Studio product later this year. Stay tuned for more Appcelerator/Aptana goodness!

<span style="font-size: x-small;">"<a href="http://developer.appcelerator.com/blog/2011/03/appcelerator%e2%80%99s-aptana-pydev-wins-%e2%80%9cbest-developer-tool%e2%80%9d-from-the-eclipse-foundation.html">Appcelerator’s Aptana PyDev wins “Best Developer Tool” from the Eclipse Foundation « Appcelerator Developer Center</a>" </span></blockquote>
リリース延期みたい？今年中になってる・・・
