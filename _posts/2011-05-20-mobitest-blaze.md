---
layout: post
title: Mobitestでモバイルパフォーマンス計測!
categories:
- analytics
- performance
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _aioseop_description: どーも、モバイルで1発当てたい@t32kでございます。今日はですね、モバイルのパフォーマンス計測について書きたいと思います。
  pvc_views: '6187'
---
<a href="http://www.blaze.io/mobile/"><img title="MOBITEST" src="http://t32k.me/mol/file/2011/05/mobitest.png" alt="" width="470" height="250" /></a>

今日はモバイルのパフォーマンス計測について書きたいと思います。パフォーマンスといえばPCなら分かってるつもりなのですが、ことモバイルになってくるとあんまり分かっておりません。「HTTPリクエストを減らす」って原則は変わらないのですが、PCとはいろいろ勝手が違うぜって話です。

パフォーマンス対策に当たってまず始めることは、それをビジュアライズすることです。パフォーマンスというのは目には見えないものですから、なにか対策しても「なんか速くなった…じゃね？」じゃ、どうしようもないです。

<!--more-->

そこでPCサイトであれば、Firefox:Firebugのネットタブ、Chrome:開発者ツールのNetWorkなどのツールを使い、ウォーターフォールチャートというものが確認します。このチャートではページのコンポーネント（部品）の読み込まれ方が確認でき、どこがボトルネックなのかといったことが発見することができます。なんてクールなんざんしょ♪
<h2>Mobitest</h2>
はい、しかしiPhoneやAndroidのブラウザではこんな開発者ツール使うことできませんね。どしたらえーねん？ってゆーことで今回紹介する<a href="http://www.blaze.io/mobile/"><strong>Mobitest</strong></a>です。Mobitestは<a href="http://www.blaze.io/">Blaze</a>という会社のモバイルデバイス用のパフォーマンス計測ツールです。
<ul>
	<li><a href="http://www.blaze.io/mobile/">Mobitest – Mobile Web Performance Tool | Blaze.io </a></li>
</ul>
現在はベータ版ということですが、カナダのオタワからhigh-speed Wi-Fi connectionで、下記デバイスで計測ができます。
<ul>
	<li>iPhone 4.3 (iPhone 4)</li>
	<li>Android 2.3 (Nexus S)</li>
	<li>Android 2.2 (Samsung Galaxy S)</li>
</ul>
ということで、Android 2.3で<a href="http://kanazawajs.tumblr.com/v1-0/">kanazawa.js v1.0</a>のページを計測したこんな感じになりました。

<a href="http://www.blaze.io/mobile/result/?testid=110519_TW_JA&amp;vidid=110519_bd4c6d38a168cf5599410026d937f7df762a7eb4"><img class="alignnone size-full wp-image-3219" title="Performance Result" src="http://t32k.me/mol/file/2011/05/result1.png" alt="" width="470" height="250" /></a>

読み込み時間、読み込みサイズ。そしてこのページはこれまで計測されたページの50%より速いぜって言ってます。もちろん、ウォーターフォールチャートも確認できます。

<img class="alignnone size-full wp-image-3220" title="Waterfall Chart" src="http://t32k.me/mol/file/2011/05/chart.png" alt="" width="470" height="250" />

各チャートの細かな段階（DNS LookupやWaitngなど）見たければ、<strong>View HAR file </strong>のリンクをクリックしましょう。

<img class="alignnone size-full wp-image-3221" title="HAR File" src="http://t32k.me/mol/file/2011/05/har.png" alt="" width="470" height="278" />

<a href="http://www.softwareishard.com/blog/har-viewer/">HAR viewer</a>で確認できます。
<h2>WebPagetest</h2>
はい、では同じページをPCで計測したらどうなるかというと今度は<a href="http://www.webpagetest.org/">WebPagetest</a>を使用します。MobitestもベースはWebPagetestで動いてます。条件をできるだけ同じようにするために、New York, NY - Chrome - DSLで計測した結果が以下です。

<a href="http://www.webpagetest.org/result/110519_GA_MXB3/1/details/"><img class="alignnone size-full wp-image-3224" title="WebPagetest" src="http://t32k.me/mol/file/2011/05/webpagetest.png" alt="" width="470" height="261" /></a>

先程のMobitestと比べてどうでしょうか？はい、なんか違うような気がします。
<h2>Browserscope</h2>
<img class="alignnone size-full wp-image-3225" title="browserscope" src="http://t32k.me/mol/file/2011/05/browserscope.png" alt="" width="470" height="252" />
<ul>
	<li><a href="http://www.browserscope.org/">Browserscope </a></li>
</ul>
ここでは各コンポーネントの読み込み時間は気にしていません。それよりもコンポーネントの読み込まれ方について比較しててみましょう。Browserscopeで調べてみると、どうやらMax Connectionsが違うらしいです。AndroidのBrowserはChromeのようでChromeではないということで、上記図よりAndroid2.3(2.2も)最大接続数が4つなっています。a.example.com, b.example.comとドメインが違っても同時に接続できるのが4つということです。つまり、Android2.x系は並列ダウンロードの恩恵があまり受けれない悲しいブラウザとなっていますね。代わって、Chromeは35と一杯接続可能です。同時に接続できる数が多ければそれだけ接続する待ち時間が少なくてよいので、読み込み完了が早くなるということですね。
<h2>HTTP Archive mobile</h2>
今回は、各ウォーターフォールチャートの違いからPC(Chrome)とモバイル(Android)のブラウザでは最大接続数が違うってことが分かりました。しかし、これだけでPCとモバイルブラウザの違いは説明できるとは思っていません。まだまだ知らなければいけないことがたくさんありそうです。

ということで、モバイルサイトではどのようなリソースが使われているかなどの統計データが<strong><a href="http://mobile.httparchive.org/interesting.php">HTTP Archive mobile</a></strong>というところで確認できます。このデータはiPhone4.3で計測したMobitestのデータを収集したものになってますので、みなさんもじゃんじゃん計測してみてはどうでしょうか。
