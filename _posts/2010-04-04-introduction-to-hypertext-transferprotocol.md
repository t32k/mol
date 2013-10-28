---
layout: post
title: 今夜わかるHTTP (Network)
categories:
- books
tags:
- http　
status: publish
type: post
published: true
meta:
  pvc_views: '3768'
  _edit_last: '1'
---
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798108200/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51T8HRW0XCL._SL160_.jpg" border="0" alt="今夜わかるHTTP (Network)" width="112" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E4%BB%8A%E5%A4%9C%E3%82%8F%E3%81%8B%E3%82%8BHTTP-Network-%E4%B8%8A%E9%87%8E-%E5%AE%A3/dp/4798108200%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4798108200" target="_blank">今夜わかるHTTP (Network)</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" /></span>

<span>翔泳社  2004-12-09
売り上げランキング : 96819
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-5.gif" alt="" /></span>

<span><a href="http://www.amazon.co.jp/%E4%BB%8A%E5%A4%9C%E3%82%8F%E3%81%8B%E3%82%8BHTTP-Network-%E4%B8%8A%E9%87%8E-%E5%AE%A3/dp/4798108200%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4798108200" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
ちょっと「今夜」で読み切れるほどのページ量(約300P)でないので、若干うろたえたが、易しい解説のおかげでなんとか読み切ることができたー。

<a href="http://t32k.me/mol/2010/03/http-and-web/">前回の本</a>があんまりだったのだが、今回はまさしくコレ！って感じのことが知ることができて満足。ほかにもTCP/IPの本を読んだのだが、専門外も甚だしくさっぱりだったので、HTTPプロトコルに的を絞ったこの本が僕にはちょうどよかった。

<!--more-->

一応、TCP/IPプロトコル群についても軽く説明しぃーの、URLってなんぞいねって言いつつ、HTTPの仕組み、ヘッダーフィールド・ステータスコードをわっさー解説、セキュリティと負荷分散についても触れ触れな感じの内容です。

絶対に負荷分散とかもっと奥の深いもんだと思うけど、全体的に広ーく浅ーく説明していてがちょうどよかったし、例えのイラストも分かりやすく、文系デザイナーでも理解できる仕様になっている。うん、やっぱりデザイナーは「絵」で物事を考えるからイラストが多いのは非常に助かるんだ。

「<a href="http://t32k.me/mol/2010/03/techniques-of-enhance-seo/">SEO を強化する技術</a>」が難しいって人はこっちから読んだら理解しやすくるんじゃないかなとも思ったり。

あ、そうそう挿絵のキャラがかなりシュールでしたｗ
以下メモメモ。
<blockquote style="font-size: 90%; line-height: 1;">
<h4>HTTPメッセージの構造</h4>
<ul>
	<li>メッセージヘッダー
<ul>
	<li>（リクエスト|ステータス）ライン</li>
	<li>（リクエスト|レスポンス）ヘッダーフィールド</li>
	<li>汎用ヘッダーフィールド</li>
	<li>エンティティヘッダーフィールド</li>
	<li>その他</li>
</ul>
</li>
	<li>空行（CR+LF）</li>
	<li>メッセージボディ</li>
</ul>
<h4>HTTPヘッダーフィールド</h4>
<ul>
	<li>汎用ヘッダーフィールド
<ul>
	<li>Cache-Control</li>
	<li>Connection</li>
	<li>Date</li>
	<li>Pragma</li>
	<li>Trailer</li>
	<li>Transfer-Encoding</li>
	<li>Upgrade</li>
	<li>Via</li>
	<li>Warning</li>
</ul>
</li>
	<li>リクエストヘッダーフィールド
<ul>
	<li>Accept</li>
	<li>Accept-Charset</li>
	<li>Accept-Encoding</li>
	<li>Accept-Language</li>
	<li>Authorization</li>
	<li>Expect</li>
	<li>From</li>
	<li>Host</li>
	<li>If-Match</li>
	<li>If-Modified-Since</li>
	<li>If-None-Match</li>
	<li>If-Range</li>
	<li>If-Unmodified-Since</li>
	<li>Max-Forwards</li>
	<li>Proxy-Authorization</li>
	<li>Range</li>
	<li>Referer</li>
	<li>TE</li>
	<li>User-Agent</li>
</ul>
</li>
	<li>レスポンスヘッダーフィールド
<ul>
	<li>Accept-Ranges</li>
	<li>Age</li>
	<li>ETag</li>
	<li>Location</li>
	<li>Proxy-Authenticate</li>
	<li>Retry-After</li>
	<li>Server</li>
	<li>Vary</li>
	<li>WWW-Authenticate</li>
</ul>
</li>
	<li>エンティティヘッダーフィールド
<ul>
	<li>Allow</li>
	<li>Content-Encoding</li>
	<li>Content-Language</li>
	<li>Content-Length</li>
	<li>Content-Location</li>
	<li>Content-MD5</li>
	<li>Content-Range</li>
	<li>Content-Type</li>
	<li>Expires</li>
	<li>Last-Modified</li>
</ul>
</li>
</ul>
</blockquote>
