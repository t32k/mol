---
layout: post
title: Webパフォーマンス改善のためのChrome開発者ツール
categories:
- performance
tags:
- chrome
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '1637'
---
気づいたら夏終わってたわー、俺の夏が一番最初に終わったわー、t32kだよ。
<h2>Webパフォーマンス改善のためのChrome開発者ツール</h2>
この前社内勉強会したスライド公開しとくよ。「パフォーマンス改善のためのChrome開発者ツール」と題して、簡単なDevToolの紹介と、拡張機能PageSpeedの使い方の説明したよ。

ほとんどデモでスライドにはあまり意味が無いんだけど、せっかくなので、
<a href="https://developers.google.com/speed/docs/best-practices/rules_intro">Web Performance Best Practices — Google Developers</a>ココ訳したやつも載っけておくね。まだ全部訳しきれてないんだけど、一応、PageSpeedで提案される対策に関しては訳してあると思う（意味わからん日本語もあるけど）。

あとで追記する、多分。

<script async class="speakerdeck-embed" data-id="503cd1bede4a4f0002052f08" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

<a href="https://speakerdeck.com/u/t32k/p/improve-web-performance-with-chrome-dev-tools">Improve web performance with chrome dev tools // Speaker Deck</a>
<h2>すべての人に知っておいてほしい スマートフォンサイトデザインの基本原則</h2>
あと、ムック本だけど本書いたよ。よかったら買ってね。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td colspan="2"><a href="http://www.amazon.co.jp/%E3%81%99%E3%81%B9%E3%81%A6%E3%81%AE%E4%BA%BA%E3%81%AB%E7%9F%A5%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%84%E3%81%A6%E3%81%BB%E3%81%97%E3%81%84-%E3%82%B9%E3%83%9E%E3%83%BC%E3%83%88%E3%83%95%E3%82%A9%E3%83%B3%E3%82%B5%E3%82%A4%E3%83%88%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3%E3%81%AE%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%89%87-%E7%9F%B3%E6%9C%AC%E5%85%89%E5%8F%B8/dp/4844362844%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4844362844" target="_blank">すべての人に知っておいてほしい スマートフォンサイトデザインの基本原則</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" /></td>
</tr>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/%E3%81%99%E3%81%B9%E3%81%A6%E3%81%AE%E4%BA%BA%E3%81%AB%E7%9F%A5%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%84%E3%81%A6%E3%81%BB%E3%81%97%E3%81%84-%E3%82%B9%E3%83%9E%E3%83%BC%E3%83%88%E3%83%95%E3%82%A9%E3%83%B3%E3%82%B5%E3%82%A4%E3%83%88%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3%E3%81%AE%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%89%87-%E7%9F%B3%E6%9C%AC%E5%85%89%E5%8F%B8/dp/4844362844%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4844362844" target="_blank"><img class="fig" style="border: 0px;" src="http://ecx.images-amazon.com/images/I/51bIbmljsJL._SL160_.jpg" alt="すべての人に知っておいてほしい スマートフォンサイトデザインの基本原則" width="118" height="160" border="0" /></a></td>
<td valign="top"><span>石本光司 いちがみトモロヲ 外間かおり 矢野りん 加藤善規 小林信次 斉藤祐也 境 祐司 谷 拓樹 豊沢泰尚 古籏一浩 </span>エムディエヌコーポレーション 2012-08-27売り上げランキング : 2410

<a href="http://www.amazon.co.jp/%E3%81%99%E3%81%B9%E3%81%A6%E3%81%AE%E4%BA%BA%E3%81%AB%E7%9F%A5%E3%81%A3%E3%81%A6%E3%81%8A%E3%81%84%E3%81%A6%E3%81%BB%E3%81%97%E3%81%84-%E3%82%B9%E3%83%9E%E3%83%BC%E3%83%88%E3%83%95%E3%82%A9%E3%83%B3%E3%82%B5%E3%82%A4%E3%83%88%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3%E3%81%AE%E5%9F%BA%E6%9C%AC%E5%8E%9F%E5%89%87-%E7%9F%B3%E6%9C%AC%E5%85%89%E5%8F%B8/dp/4844362844%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4844362844" target="_blank">Amazonで詳しく見る</a><span> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
