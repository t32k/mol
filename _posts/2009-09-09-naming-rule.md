---
layout: post
title: ネーミングの掟と極意　開発を失敗させる名前の付け方、成功させる名前の付け方
categories:
- books
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/09/naming-rule.html
  _edit_last: '1'
  pvc_views: '3899'
---
<table border="0" cellpadding="5"><tbody><tr><td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4798114332/warikiru-22/ref=nosim/" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51NBqyKkEFL._SL160_.jpg" alt="ネーミングの掟と極意 (エンジニア道場)" border="0" /></a></td><td valign="top"><span style=""><a href="http://www.amazon.co.jp/%E3%83%8D%E3%83%BC%E3%83%9F%E3%83%B3%E3%82%B0%E3%81%AE%E6%8E%9F%E3%81%A8%E6%A5%B5%E6%84%8F-%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E9%81%93%E5%A0%B4-%E9%96%8B%E7%B1%B3-%E7%91%9E%E6%B5%A9/dp/4798114332%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4798114332" target="_blank">ネーミングの掟と極意 (エンジニア道場)</a><img src="http://www.blogger.com/%27http://www.assoc-amazon.jp/e/ir?t=" l="ur2&amp;o=" 9="" alt="''" border="0" height="1" width="1" /><br /><br />翔泳社  2007-11-06<br />売り上げランキング : 61183<br />おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-5.gif" /><br /><br /><a href="http://www.amazon.co.jp/%E3%83%8D%E3%83%BC%E3%83%9F%E3%83%B3%E3%82%B0%E3%81%AE%E6%8E%9F%E3%81%A8%E6%A5%B5%E6%84%8F-%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E9%81%93%E5%A0%B4-%E9%96%8B%E7%B1%B3-%E7%91%9E%E6%B5%A9/dp/4798114332%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4798114332" target="_blank">Amazonで詳しく見る</a></span> <span style="">by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td></tr></tbody></table><br />名前の付け方がどうしよもなく下手です、はい。それで何か良い本はないかと探してたら、この本が評価が高かったので読んでみました。<br /><br />本書はエンジニア向けですが、デザイナーである自分も十分理解できました。読む前はメソッド名の付け方（getElementByIdみたいな）など説明した本かなと思ってましたけど、ほとんどはもっと根本的な名前の付け方に関して説明です。<br /><br />例えば、ソフトウェア製品に新機能が付いたのでその名前はどうしよう？「音声認識機能」じゃない？いや「音声コントロール機能」だよ。などというやりとりで本書は進んでいきますので、Webディレクター、いやWebに携わる者なら読んでおいて損はしないです。<br /><br />そして、最も良い名前の付け方なんてものはなく、その名前を扱う環境、人によって最適な名前の付け方は変化します。一見、スマートじゃない名前を見てもそのドキュメントなり、そのプログラム全体で見れば筋の通った名前かもしれませんし、また言語によっては慣習的な名前の付け方があるのでそういった慣習に従うのも良いと言っています。<br /><br />唯一言えることは、「<span style="font-weight: bold;">その基本動作を１つ１つ意識して、抜かりなくやろうよ</span>」ってことらしいです。はい、名前付けに近道なんて甘いことは通じませんねｗ<br /><br />名前を考えるうえで、意識しておいた方が良い事なんかも紹介してあります。<br /><br /><ul><li>ビジュアライズ（図解、構造化）</li><li>サマライズ（要約、仮ネーミング）</li><li>ループバックチェック</li><li>用例列挙チェック</li><li>あいまい用語チェック</li><li>識別効果チェック</li><li>コトバ関係チェック</li></ul><br />まず、名前の付ける機能を理解・把握するために図解し構造化して考えてみる。そして、それを見ながら要約する。名前というのは究極の要約なのでちょっと長い仮ネーミングみたいなものをつけてループバック（名前からその機能を理解できるか、またその逆も可能か）チェックしてみたり、あいまいでないかチェックする方法です。<br /><br />本書の後半は、ネーミング道場乱取りタイムと称して、２０例ほどケースが紹介されているので、頭の汗をかくにはもってこいです（笑）
