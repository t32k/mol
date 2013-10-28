---
layout: post
title: Sencha Touch ちょっと触ってみた所感2
categories:
- javascript
tags:
- senchajp
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '5580'
---
ちっす、無職のt32kです。今日は<a href="http://www.sencha.com/products/touch/">Sencha Touch2</a>触ってみた感想など綴っていくよ。久しぶりのブログだからキャラ掴めてないよ。

事の発端は、愛しの<a href="http://tumblrgear.tumblr.com/">tumblr gear</a>さんが立ち上げるとすぐシャットダウンしてしまう不具合（v1.6.4で治りました：）が長らく続いておりまして、なんとか打開策がないもんかと考えた結果、自分で作ろうぜってことになって作ってみた（デモアプリだけど）。Titanium Mobileでもありかと思ったけど、Webアプリも作ってみたいと考えていたのでjQuery Mobileの紹介時によく引き合いに出されるだけ出されてそれっきりのSencha Touchで作ってみることにした。

<a href="http://t32k.me/mol/file/2012/05/t1.jpg"><img class="aligncenter size-full wp-image-4028" title="t1" src="http://t32k.me/mol/file/2012/05/t1.jpg" alt="" width="500" height="375" /></a>

僕がtumblr gear が好きなのはその操作性。タップによる画面遷移です。なんかスマホとかになるとフリックとかスワイプとかもてはやされてる感があるんだけど、やっぱクリック・タップが個人的に一番慣れてる。しかもtumblr gearはタップする毎にいち画面いちアイテムで表示されるからフリックし過ぎちゃって戻ったりするロスもないわけでたくさんの<del>エロ</del>クールな画像など閲覧できるわけです。ぼくは残りの少ない人生のなかで一枚でも多くの<span style="color: #888888;"><del>エロ</del></span>クールな画像を見たいわけです。ということで、TumblrTouchというデモアプリを作りました。
<h2>TumblrTouch</h2>
<iframe style="float: left; margin-right: 24px;" frameborder="0" height="500" src="http://player.vimeo.com/video/42133470?byline=0&amp;portrait=0" width="250"></iframe>

というわけで、こんな感じのデモアプリができた。
<ul>
	<li><strong><a href="https://github.com/t32k/tumblrtouch">github:t32k/tumblrtouch</a></strong></li>
<ol>
	<li>Tumblr API (Photo Posts)の使用</li>
	<li>1画面1アイテム</li>
	<li>タップによる遷移</li>
</ol>
</ul>
要件としてはこんな感じで、Tumblr APIで画像のPostを取ってきて画像のURLをPanelの配列にぶち込んで、toolbarのbuttonにページ送りの関数をバインドする流れ。APIで取ってくるときに異なるドメインから取ってくるのでJSONPでやると思うんだけどなぜかエラーが出るので、一回自分のドメインにposts.jsonを保存してAJAXでそれを読み込んでる（無念...）.

<h2>Anatomy of an Application</h2>
<p style="text-align: center;"><img class="aligncenter" src="http://docs.sencha.com/touch/2-0/guides/apps_intro/architecture-overview.png" alt="" width="500" /></p>
TumblrTouch自体は簡単アプリだけども、Sencha Touchのドキュメント見ながら作ったら僕でもMVCでコードを分割管理することができた。

Model, View, Controller以外にもデータのやりとりのStore、タブレットかスマートフォンか管理するProfileなどのも用意されてるみたい。よく分かんないけど。

よくSench TouchはTitnaium Mobile と似てるなんて言われてて、僕もそうなんだーと思って実際のサンプルコードみたらなんか違う・・って印象でした。確かにUIコンポーネントとかはだいたいTitanium.createってとこがExt.createになるんですけど。こんなかんじ。
<pre><code>var button = Titanium.UI.createButton({
 title: 'Hello'
});</code></pre>
<pre><code>var button = Ext.create('Ext.Button', {
 text: 'Hello'
});</code></pre>
Sencha Touchはそれとは別にxtypeで指定するだけの方法もあります。ここが最初意味わからんかった。親コンポーネントの中の場合、その子要素はitemsで指定して、各コンポーネントはxtypeでcreateできるみたいです。ショートカットみたいな。
<pre><code>Ext.create('Ext.Container', {
    items: {
        xtype: 'button',
        text: 'Hello'
    }
});</code></pre>
<ul>
	<li><a href="http://docs.sencha.com/touch/2-0/#!/guide/components">Components - Sencha Docs - Touch 2.0 </a></li>
</ul>
最初からちゃんとドキュメント読んどけばすんなり理解できたんだけど、Titaniumの要領で〜って考えてから手間取った。
あとは、以下のビデオみたら順を追ってアプリ作成について説明しているのでsencha touchの取っ掛かりには良いと思う。

<ul>
	<li><a href="http://docs.sencha.com/touch/2-0/#!/video/mvc-part-1">MVC in Depth Part 1 - Sencha Docs - Touch 2.0 </a></li>
</ul>

結局、Webアプリなので最悪CSSでなんとかできるのがWebデザイナーとしてはチョーありがたい。あ、Sass触ってねーや。。

とりあえず、公式のドキュメントやサンプルが英語だけどかなり豊富なので、なんとか頑張れる。公式以外の情報をググろうとするとSencha Touch2が3月にリリースされたばかりでSencha Touch1の情報ばかりで混乱する。あと日本語の情報少ない。皆無。。。

ありえるえりあさんがシリーズものの勉強会を開催しているので今後は参加していきたい。
<ul>
	<li><a href="http://connpass.com/event/477/">ありえるえりあミニ勉強会#2 ～Sencha Touch - connpass </a></li>
</ul>
んで、TwitterでSencha Touchの情報をつぶやくときは<a href="https://twitter.com/#!/search/%23senchajp">#senchajp</a>のハッシュタグつけよーず。
<div id="__ss_12939909" style="width: 510px;">
<object id="__sse12939909" width="510" height="426" classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="wmode" value="transparent" /><param name="src" value="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=tumblrtouch-120515074530-phpapp01&amp;stripped_title=tumblrtouch&amp;userName=t32k" /><param name="allowscriptaccess" value="always" /><param name="allowfullscreen" value="true" /><embed id="__sse12939909" width="510" height="426" type="application/x-shockwave-flash" src="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=tumblrtouch-120515074530-phpapp01&amp;stripped_title=tumblrtouch&amp;userName=t32k" allowFullScreen="true" allowScriptAccess="always" wmode="transparent" allowscriptaccess="always" allowfullscreen="true" /> </object>
<div style="padding: 5px 0 12px;">View more <a href="http://www.slideshare.net/" target="_blank">presentations</a> from <a href="http://www.slideshare.net/t32k" target="_blank">Koji Ishimoto</a>

<h3>参考</h3>
<ul>
	<li><a href="http://hamalog.tumblr.com/post/6822986289/sencha-touch">Sencha Touch ちょっと触ってみた所感 - Takazudo hamalog </a></li>
</ul></div></div>
