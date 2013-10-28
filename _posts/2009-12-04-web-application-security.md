---
layout: post
title: Ajaxアプリケーションの安全性 - Web Application Security
categories:
- report
tags:
- wde09
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/12/douglas-crockford.html
  _edit_last: '1'
  pvc_views: '2382'
---
<img src="http://lh5.ggpht.com/_1drnogi3vdg/SxOxSFOByEI/AAAAAAAAAuU/Rsuy0uB-Jnk/douglas-crockford.jpg" alt="Douglas Crockford" />
<span style="font-size: 85%;"><a href="http://east.webdirections.org/wde/2009/program/">Web Directions East 2009 カンファレンス</a> 11月13日 14:00–14:55</span>
<h3>Douglas Crockford（ダグラス・クロックフォード）</h3>
現在 Yahoo! の JavaScript アーキテクトとして所属している Crockford 氏は、JavaScript Object Notation (JSON) を紹介した人。長くテクノロジー関連の仕事に携わっており、Atari, Paramount, Lucasfilm など様々な企業の IT 化への協力。JavaScript 開発の第一人者として JavaScript の安全性や異なるブラウザに対する対処方法について数々のセミナーで講演。
<h4>Contacts</h4>
<ul>
	<li><a href="http://www.crockford.com/">Douglas Crockford's Wrrrld Wide Web</a></li>
</ul>
<h3>Ajaxアプリケーションの安全性 - Web Application Security</h3>
<h4>The SAMY Saga 問題</h4>
MySpace(2005)
サミーのページを見た全ての人がフレンドリストに追加された
サミーは良い人でしたがアタッカーだったらどうなるでしょうか？
すべてのドキュメントを読める
サーバーにリクエストを作れる
データーベースにアクセスできる
ブラウザはこれを防ぐことはできない
機械には良いか悪いかなんて理解できない

クロスサイトスクリプティング（1995）
Web標準では解決できない
セキュリティの必要条件ではあるが十分条件ではない
HTML5も解決してくれない
後々に改善はしてはいけるがゴールにはならない
デベロッパーがセキュリティについての完全な知識を身につけることは無理
セキュリティは改善するには大きすぎる。たぶん失敗するだろう
Flash/Silverlight　←オープンじゃない
なぜ間違ってたのか？標準が間違っている！The Standard Mistake
<span style="font-weight: bold;">セキュリティ2.0 <span style="color: #330099;">×</span></span> 最初から考えとく必要がある
セキュリティはモジュール化できない
セキュリティ関連の委員会が細かすぎる
暗号化することで全てが解決するわけではない
DLA（Digital Living Room）でネットワークを統一すると家電にまでウィルスが入って大変なことになる

アイデンティティやオーソリティが問題
Userを守る必要性がある
Webはカジュアルで自動的だ
ブラウザはUserとSystemの区別をできない
WebもHTML/CSS/JavaScriptいろいろなものが混在している
これらはWeb2.0の問題ではない
広告が標的になる
JavaScriptはセキュリティが高い
新しいセキュリティモデルが必要
<h4>Object Capabilities</h4>
There are exactly three ways to obtain a reference.
<ul>
	<li>By Creation.</li>
	<li>By Construction.</li>
	<li>By Introduction.</li>
</ul>
W3C反対方向へ行っている
HTML5はリセットするべき
DOMは危険
複雑性はセキュリティの敵

広告は深刻な問題

<a title="Douglas Crockford by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/4102432089/"><img src="http://farm3.static.flickr.com/2539/4102432089_fe2a6eca09.jpg" alt="Douglas Crockford" width="375" height="500" /></a>
<span style="color: #666666; font-size: 85%;">(Douglas先生大っきい！)</span>

質問：Caja とは？ GoogleのJavaScriptを安全なものに書き換えるプロジェクト
<a href="http://code.google.com/p/google-caja/">google-caja - Project Hosting on Google Code</a>
<h3>セッション感想</h3>
AJAX自体、よく理解していないので高度なセキュリティの話にはついていけなかった。とりあえず、他のサービスとマッシュアップしたりしなければ、Webデザイナーとしては、特にそこまで気にする必要はないのかと思った。とはいえ、DOMは危険と何度も繰り返し言われていたので、そのあたりは注意する必要があるかと思う。セキュリティの仕様、ECMAScript5 の仕様の推移を見守りたい。

個人的には JavaScript Good Partsに基づいたセッション内容が聞きたかったかな。いやセキュリティは大事だと思うんですけど、ちょっとあの空気感は異様なものがあったと思う...
<h4>スライド資料</h4>
<div id="__ss_630645" style="width: 425px; text-align: left;"><a style="margin: 12px 0pt 3px; font-family: Helvetica,Arial,Sans-serif; font-style: normal; font-variant: normal; font-weight: normal; font-size: 14px; line-height: normal; font-size-adjust: none; font-stretch: normal; display: block; text-decoration: underline;" title="Douglas Crockford - Ajax Security" href="http://www.slideshare.net/webdirections/douglas-crockford-ajax-security-presentation">Douglas Crockford - Ajax Security（旧バージョン）</a><object style="margin: 0px;" classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="425" height="355" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="src" value="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=douglascrockford-1222903962429701-9&amp;stripped_title=douglas-crockford-ajax-security-presentation" /><param name="allowfullscreen" value="true" /><embed style="margin: 0px;" type="application/x-shockwave-flash" width="425" height="355" src="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=douglascrockford-1222903962429701-9&amp;stripped_title=douglas-crockford-ajax-security-presentation" allowscriptaccess="always" allowfullscreen="true"></embed></object>
<div style="font-size: 11px; font-family: tahoma,arial; height: 26px; padding-top: 2px;">View more <a style="text-decoration: underline;" href="http://www.slideshare.net/">presentations</a> from <a style="text-decoration: underline;" href="http://www.slideshare.net/webdirections">webdirections</a>.</div>
</div>
<a href="http://east.webdirections.org/wde/2009/resources/web-application-security/">『Ajaxアプリケーションの安全性』Douglas Crockford | Web Directions East</a>
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873113911/warikiru-22/ref=nosim/" target="_blank"><img class="fig" style="border: 0pt none;" src="http://ecx.images-amazon.com/images/I/41H0Dk-K3PL._SL160_.jpg" border="0" alt="JavaScript: The Good Parts ―「良いパーツ」によるベストプラクティス" width="124" height="160" /></a></td>
<td valign="top"><span style="font-size: 85%;"><a href="http://www.amazon.co.jp/JavaScript%253a-Parts-%E2%80%95%E3%80%8C%E8%89%AF%E3%81%84%E3%83%91%E3%83%BC%E3%83%84%E3%80%8D%E3%81%AB%E3%82%88%E3%82%8B%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Douglas-Crockford/dp/4873113911%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113911" target="_blank">JavaScript: The Good Parts ―「良いパーツ」によるベストプラクティス</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" border="0" alt="" width="1" height="1" />
Douglas Crockford (著), 水野 貴明 (翻訳)オライリージャパン  2008-12-22
売り上げランキング : 6464
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-5-0.gif" alt="" /><a href="http://www.amazon.co.jp/JavaScript%253a-Parts-%E2%80%95%E3%80%8C%E8%89%AF%E3%81%84%E3%83%91%E3%83%BC%E3%83%84%E3%80%8D%E3%81%AB%E3%82%88%E3%82%8B%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Douglas-Crockford/dp/4873113911%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113911" target="_blank">Amazonで詳しく見る</a>

</span><span style="font-size: 85%;">by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
