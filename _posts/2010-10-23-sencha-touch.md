---
layout: post
title: Sencha 導入前の事前準備：SwapSkills Vol.9
categories:
- javascript
- report
tags:
- sencha
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '4625'
  _oembed_7b6cd8021d09f2f6daa57e8cc5acd00e: '{{unknown}}'
  _oembed_447ddd237ef1839aedd9b78ed9db15bf: '{{unknown}}'
  _oembed_aedca5f54b3aeedaac6b58e5c50c6d4f: '{{unknown}}'
  _oembed_8218b133bfea3e7744ace5dc75067607: '{{unknown}}'
---
<img class="alignnone size-full wp-image-1884" title="ss9_2" src="/static/blog/2010/10/ss9_2.jpg" alt="" width="470" height="250" />

<a href="http://swapskills.info/sessions/html5-sencha.html">HTML5モバイルアプリ用フレームワーク：Sencha導入前の事前準備：SwapSKills vol.9</a>

本日ですが、弊社にて上記セミナーをサテライト開催しました。Senchaについては<a href="http://www.extjs.co.jp/">こちらを参照</a>。

Sencha導入前の準備ということで、セッションの内容はSencha TouchというよりもSencha Touchを使うためのJavaScript/CSSの基礎知識を身につけようというものでした。

<!--more-->

というのも、「Sencha Touch/Ext.JSのサンプルなりをコピペしてつくれば、数時間でそれなりのものを作れるだろう。しかし、なにかバグなど発生したり、プロジェクトが複雑になってくれば対処できなくなる。結局はそれを修正するために余計に時間がかかったりするわけで基礎の知識を学ぶことを怠ってはいけない」と講演者の小堤 一弘（<a href="http://twitter.com/kotsutsumi">@kotsutsumi</a>）さんおしゃっていました。

うーん。耳が痛いです＞＜ jQueryにしてもそうですが、ネットにはいろいろ便利なプラグイン・サンプルがあってよく分からないまま使っていることがあります。拡張・修正とか考えれば、JavaScript自体についても理解が必要になってきますもんね。ということで、デザイナーであろうとも、変数の型やクロージャやプロトタイプについては最低限知っておいて欲しいとのことでお勉強しました。そのような知識はSencha以外でも役に立ちますし。
<ul>
	<li><a href="https://developer.mozilla.org/ja/javascript">JavaScript - MDC</a></li>
</ul>
無料で正しいJSの知識を得たければ一読すべし。
<ul>
	<li><a href="http://dev.sencha.com/deploy/touch/docs/">Sencha Touch API Documentation</a></li>
</ul>
すぐにアプリを作るんじゃなくて、APIをひと通り眺めてから作りなさい。

<img class="alignnone size-full wp-image-1883" title="ss9_1" src="/static/blog/2010/10/ss9_1.jpg" alt="" width="470" height="250" />

そんんわけで、やっぱり基本は大事だと身に染みた良いセッションでした。がんばります。ありがとうございましった！！
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114616/warikiru-22/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51qb8cLjHyL._SL160_.jpg" border="0" alt="iPhoneアプリケーション開発ガイド　―HTML+CSS+JavaScript による開発手法" width="125" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/iPhone%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E9%96%8B%E7%99%BA%E3%82%AC%E3%82%A4%E3%83%89-%E2%80%95HTML-JavaScript-%E3%81%AB%E3%82%88%E3%82%8B%E9%96%8B%E7%99%BA%E6%89%8B%E6%B3%95-Jonathan-Stark/dp/4873114616%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114616" target="_blank">iPhoneアプリケーション開発ガイド　―HTML+CSS+JavaScript による開発手法</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
Jonathan Stark 増井 俊之 </span>

<span>オライリージャパン  2010-08-07
売り上げランキング : 3135
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-0.gif" alt="" /></span>

<span><a href="http://www.amazon.co.jp/iPhone%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E9%96%8B%E7%99%BA%E3%82%AC%E3%82%A4%E3%83%89-%E2%80%95HTML-JavaScript-%E3%81%AB%E3%82%88%E3%82%8B%E9%96%8B%E7%99%BA%E6%89%8B%E6%B3%95-Jonathan-Stark/dp/4873114616%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114616" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
あと、ちなみにSenchaの会社は非常に大きく成長していて、<a href="http://www.jqtouch.com/">jQTouch</a>の開発者（iPhoneアプリケーション開発ガイドのちょしゃでもある）<a href="http://twitter.com/#!/jonathanstark">Jonathan Stark</a>がSenchaに加わったり、有名な開発者がどんどん集まってきているのでSenchaはより総合的なフレームワークになっていくだろうとのことでした。期待大ですね。

ちなみにちなみに、Jonathan Starkさんは11/15の<a href="http://east.webdirections.org/2010/">Web Directions East 2010</a>で講演するということなので、こちらもチェキしておくと良いですね。
<ul>
	<li><a href="http://east.webdirections.org/2010/speaker/jonathan-stark/">Jonathan Stark | Web Directions East 2010</a></li>
</ul>
<h3>Tweets #swapskills</h3>
--
<table class="twitter_matome">
<tbody>
<tr id="28481509585" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">WDEではjQTouchの開発者のジョナサン・スタークくるで！ワークショップあるで！</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28481509585">16:49:32</a></td>
</tr>
<tr id="28481506309" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">クロージャーって何？が多少なりともわかったのは収穫でした。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28481506309">16:49:28</a></td>
</tr>
<tr id="28481466294" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Senchaはどんどん大きな会社になってきて、いろいろ優秀な技術者が集まってきているので、総合的なフレームワークになってきている</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28481466294">16:48:32</a></td>
</tr>
<tr id="28480939193" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">うーん。後半はちょっと飛躍してた感じです。やはり Extはむずかしいという印象</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28480939193">16:36:29</a></td>
</tr>
<tr id="28480872273" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">11月のカンファレンスの時にでもSench Touch正式リリースされるのではないだろうかとのこと</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28480872273">16:34:59</a></td>
</tr>
<tr id="28480459620" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">うーん。。一気にレベルあがった。デザイナーには厳しす＞＜</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28480459620">16:25:39</a></td>
</tr>
<tr id="28480165733" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Ext.Eventmanager http://bit.ly/94yZBg ブラウザイベントを管理、らしい</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28480165733">16:19:07</a></td>
</tr>
<tr id="28479952272" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">ボタン押された、タップされた、などは カスタムイベント。ユーザが自分で発生させてイベントハンドラを記述することができるのがカスタムイベント</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479952272">16:14:23</a></td>
</tr>
<tr id="28479938357" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">ブラウザイベント、カスタム（Ext）イベントがある。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28479938357">16:14:05</a></td>
</tr>
<tr id="28479916148" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">イベント生成の話。ブラウザイベント、Extイベント、カスタムイベント。 Extとカスタムはほぼ同一。 違いを知らないとリークも起きうる</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479916148">16:13:34</a></td>
</tr>
<tr id="28479757630" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">htmlを生成する方法 http://bit.ly/98wadN  Ext.DomHelper タグを動的に生成できる</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479757630">16:10:04</a></td>
</tr>
<tr id="28479474309" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">同じような効果のExt.queryは配列を返す</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28479474309">16:03:53</a></td>
</tr>
<tr id="28479472103" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Ext.query は 指定したセレクタのDOMオブジェクトが返されます、らしい</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479472103">16:03:50</a></td>
</tr>
<tr id="28479361392" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">CSSセレクタライクに使うにはExt.select();で。コンポジットエレメントを返す。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28479361392">16:01:30</a></td>
</tr>
<tr id="28479346759" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">compositeElement に対して一気に同じ処理、かな。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479346759">16:01:10</a></td>
</tr>
<tr id="28479325879" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Ext.select の話。 CSSセレクタを引数に指定 Ext.CompositeElement が返ってくる 同じインターフェースを通して同じ処理を一気にできる。みたいな</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479325879">16:00:44</a></td>
</tr>
<tr id="28479165887" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">get/flyなぜ2つあるのか？getはnewするからコスト高。flyはしない。ワンライナーだとflyがいい。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28479165887">15:57:12</a></td>
</tr>
<tr id="28479158458" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">どこか部分的にぱぱっとひからせたいとかそういうときにブラウザに負荷かけたくないときに fly  one liner がfly</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479158458">15:57:02</a></td>
</tr>
<tr id="28479098057" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Ext.flyのはなし .文字大きくしてくれてありがとうすみません。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28479098057">15:55:43</a></td>
</tr>
<tr id="28479089407" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">CSSセレクタをJavaScriptでも利用したい -&gt;Ext.get(), Ext.fly()あるよ</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28479089407">15:55:32</a></td>
</tr>
<tr id="28478915793" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">画面の文字がちっちゃすぎですねー</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28478915793">15:51:45</a></td>
</tr>
<tr id="28478779908" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/zenich"><img src="http://img.tweetimag.es/i/zenich_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">getElementByIdで取得することはありえません</td>
<td class="twitter_matome_date"><a href="http://twitter.com/zenich/statuses/28478779908">15:48:47</a></td>
</tr>
<tr id="28478553094" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">詳細度の話だね</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28478553094">15:43:49</a></td>
</tr>
<tr id="28478393831" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/shirokuro331"><img src="http://img.tweetimag.es/i/shirokuro331_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">RT @t32k: 要チェキ！ http://www.xenophy.com/technology/ux/pdg/css_selector/</td>
<td class="twitter_matome_date"><a href="http://twitter.com/shirokuro331/statuses/28478393831">15:40:23</a></td>
</tr>
<tr id="28478350020" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">要チェキ！ http://www.xenophy.com/technology/ux/pdg/css_selector/</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28478350020">15:39:28</a></td>
</tr>
<tr id="28478344620" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/tmshin"><img src="http://img.tweetimag.es/i/tmshin_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">双方向だって今知った。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/tmshin/statuses/28478344620">15:39:21</a></td>
</tr>
<tr id="28477458722" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">RT @t32k: CSSファイルにスタイルを記述するだけがCSSだと思っていないか？
http://www.w3.org/TR/CSS2/selector.html</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28477458722">15:20:34</a></td>
</tr>
<tr id="28477426837" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">CSSセレクタ：DOM構造の中から、高速にHTMLエレメントを特定する手段！</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28477426837">15:19:55</a></td>
</tr>
<tr id="28477420587" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">階層が深くなると大変！cssセレクタ</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28477420587">15:19:47</a></td>
</tr>
<tr id="28477350759" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">CSSファイルにスタイルを記述するだけがCSSだと思っていないか？
http://www.w3.org/TR/CSS2/selector.html</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28477350759">15:18:19</a></td>
</tr>
<tr id="28477289638" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">@t32k domも関係しますね！</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28477289638">15:17:03</a></td>
</tr>
<tr id="28477210526" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">CSSセレクタきた！こっからデザイナーのターン</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28477210526">15:15:25</a></td>
</tr>
<tr id="28477141514" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">ここまでは。という内容も実は奥深い</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28477141514">15:14:02</a></td>
</tr>
<tr id="28477107147" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">サンプルコピペ良くない！基礎しっかりが今回のテーマだね。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28477107147">15:13:19</a></td>
</tr>
<tr id="28476500796" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">無名関数の即時実行。jQueryとかやってる。 (function(){alert("hello!");})();</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28476500796">15:01:13</a></td>
</tr>
<tr id="28476302436" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">前回のJS講座で習った事が入っていた。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28476302436">14:57:17</a></td>
</tr>
<tr id="28476254209" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">JavaScriptはガベージコレクション気にしなくてもいいけど、IEがたまにメモリリークする。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28476254209">14:56:18</a></td>
</tr>
<tr id="28476107274" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">意味分からんクロージャーキタ！</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28476107274">14:53:23</a></td>
</tr>
<tr id="28476049193" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">基礎を怠るとプロジェクトが破綻する（変数系とExtオブジェクトはしっかり！）</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28476049193">14:52:14</a></td>
</tr>
<tr id="28476002816" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">extファイルを利用してプログラムを簡素化する</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28476002816">14:51:18</a></td>
</tr>
<tr id="28475916731" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Sencha触る前にAPI見とけよー Sencha Touch API Documentation http://dev.sencha.com/deploy/touch/docs/</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475916731">14:49:36</a></td>
</tr>
<tr id="28475797157" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Sencha Touch/ Ext JS はグローバルスコープにExtオブジェクトがある</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475797157">14:47:12</a></td>
</tr>
<tr id="28475711607" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/shirokuro331"><img src="http://img.tweetimag.es/i/shirokuro331_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">今日はあとで2つのハッシュタグを追う。　#hokunet</td>
<td class="twitter_matome_date"><a href="http://twitter.com/shirokuro331/statuses/28475711607">14:45:30</a></td>
</tr>
<tr id="28475639489" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">変数の代入が、参照なのか、参照でないのか確認する必要がある</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475639489">14:44:05</a></td>
</tr>
<tr id="28475564434" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">型の確認はtypeofで確認しなさいな</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475564434">14:42:36</a></td>
</tr>
<tr id="28475528832" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">型の種類：Numbers, Array, Strings, null, Booleans, undefined, Functions, Data, Objects, Error</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475528832">14:41:55</a></td>
</tr>
<tr id="28475392447" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">JavaScript学ぶんなら、まずはこれ見とけ！→ http://j.mp/c3QmIk 無料・正しい知識を得られる。</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475392447">14:39:15</a></td>
</tr>
<tr id="28475278578" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">Sencha Touchを使うにはモダンJavaScriptを習得すべし！</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475278578">14:37:02</a></td>
</tr>
<tr id="28475162960" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/allWeb_akane"><img src="http://img.tweetimag.es/i/allWeb_akane_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">開始いたしました。  http://twitpic.com/30093g</td>
<td class="twitter_matome_date"><a href="http://twitter.com/allWeb_akane/statuses/28475162960">14:34:49</a></td>
</tr>
<tr id="28475161927" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">EXT(いーえくすてぃー).jsって言うんだ</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28475161927">14:34:48</a></td>
</tr>
<tr id="28474495463" class="twitter_matome_status">
<td class="twitter_matome_image"><a href="http://twitter.com/t32k"><img src="http://img.tweetimag.es/i/t32k_n" alt="" width="48" /></a></td>
<td class="twitter_matome_text">もうすぐはじまる！"HTML5モバイルアプリ用フレームワーク：Sencha導入前の事前準備：SwapSKills vol.9" - http://j.mp/c1YxZA</td>
<td class="twitter_matome_date"><a href="http://twitter.com/t32k/statuses/28474495463">14:22:07</a></td>
</tr>
</tbody>
</table>
--
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873113296/warikiru-22/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/413amOWGgvL._SL160_.jpg" border="0" alt="JavaScript 第5版" width="123" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/JavaScript-%E7%AC%AC5%E7%89%88-David-Flanagan/dp/4873113296%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113296" target="_blank">JavaScript 第5版</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
David Flanagan 村上 列 </span>

<span>オライリー・ジャパン  2007-08-14
売り上げランキング : 11196
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-5.gif" alt="" /></span>

<span><a href="http://www.amazon.co.jp/JavaScript-%E7%AC%AC5%E7%89%88-David-Flanagan/dp/4873113296%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113296" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
そんわけで、サイ本は何度も何度も読み返すべきだと感じました！
