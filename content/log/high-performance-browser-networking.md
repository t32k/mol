---
date: 2014-05-23
title: High Performance Browser Networking 読むでしょ！
categories: books
cover_image: "/2014/05-23-cover.jpg"
excerpt: "『ハイパフォーマンス ブラウザネットワーキング――ネットワークアプリケーションのためのパフォーマンス最適化』を読んだ、というか読んでいる、読まないわけがない"
---

<table  border="0" cellpadding="5"><tr><td valign="top"><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9-%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AD%E3%83%B3%E3%82%B0-%E2%80%95%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9%E6%9C%80%E9%81%A9%E5%8C%96-Ilya-Grigorik/dp/4873116767%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873116767" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51x2sA8N%2BTL._SL160_.jpg" border="0" alt="ハイパフォーマンス ブラウザネットワーキング ―ネットワークアプリケーションのためのパフォーマンス最適化" /></a></td><td valign="top"><font size="-1"><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9-%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AD%E3%83%B3%E3%82%B0-%E2%80%95%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9%E6%9C%80%E9%81%A9%E5%8C%96-Ilya-Grigorik/dp/4873116767%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873116767" target="_blank">ハイパフォーマンス ブラウザネットワーキング<br />―ネットワークアプリケーションのためのパフォーマンス最適化</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&l=ur2&o=9" width="1" height="1" style="border: none;" alt="" /><br />Ilya Grigorik 和田 祐一郎<br />オライリージャパン  2014-05-16<br />売り上げランキング : 3048<br /><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9-%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AD%E3%83%B3%E3%82%B0-%E2%80%95%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9%E6%9C%80%E9%81%A9%E5%8C%96-Ilya-Grigorik/dp/4873116767%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873116767" target="_blank">Amazonで詳しく見る</a></font><font size="-2"> by <a href="http://www.goodpic.com/mt/aws/index.html" >G-Tools</a></font></td></tr></table>

Ilya Grigorik氏の『ハイパフォーマンス ブラウザネットワーキング』が発売されたので流し読んでみた感想。

## Design Fast Websites

<div class="fluid"><iframe src="//www.youtube.com/embed/7HC3OV1dDZ4" allowfullscreen></iframe></div>

思い起こせば、僕がWebパフォーマンスに興味を持ったのは2008年にYUI Theaterで公開されたNicole Sullivan氏の『Design Fast Websites』の動画を見てからだ。

当時Webデザイナーだった僕にとってデザインもWebパフォーマンスに貢献出来るんだ！決してバックエンドのエンジニアだけの問題じゃないんだと知ったのは衝撃的であり、それと同時にやりがいのあることだと感じモチベーションが上がったのを今でも覚えている。クリスマス・イブの夜のことだった。

## High Performance Web Sites

<table  border="0" cellpadding="5"><tr><td valign="top"><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51hIDIWHmYL._SL160_.jpg" border="0" alt="ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール" /></a></td><td valign="top"><font size="-1"><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank">ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&l=ur2&o=9" width="1" height="1" style="border: none;" alt="" /><br />Steve Souders スティーブ サウダーズ 武舎 広幸 <br /><br />オライリージャパン  2008-04-11<br />売り上げランキング : 56034<br /><br /><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank">Amazonで詳しく見る</a></font><font size="-2"> by <a href="http://www.goodpic.com/mt/aws/index.html" >G-Tools</a></font></td></tr></table>

それから、フロントエンドのパフォーマンスつながりで、Steve Souders氏の『ハイパフォーマンスWebサイト』を手にとって夢中で読んだのが5年前。以後、僕の口癖は『HTTPリクエストを減らす』になった。

## Perfmatters

![](/mol/images/2014/05-23-fig01.png)

最近ではフロントエンドのパフォーマンスも細分化されてきて、Network、Render、Computeの3つに大別されるようになってきたが、僕はやっぱり『HTTPリクエストを減らす』の精神でネットワークの分野に一番興味があるし、大抵の場合においてネットワークが問題の主要な要因になってるのは間違いないと思っている。

+ [HTTPリクエストを減らすために【序章】HTTPリクエストは甘え — MOL](http://t32k.me/mol/log/reduce-http-requests-overview/)
+ [HTTPリクエストを減らすために【終章】我々には1000msの猶予しか残されていない — MOL](http://t32k.me/mol/log/reduce-http-requests-one-second/)

そんなとき、いつも参考にしてきたのがIlya Grigorik氏の記事であったりスライド・動画だ。

+ [Ilya Grigorik - YouTube](https://www.youtube.com/user/igrigorik/videos)

彼はとてもスマートでしっかりとした根拠を持って、いつも発表しているので、とても尊敬しているのだが、なにぶん難しいテーマなので、今回、『High Performance Browser Networking』が邦訳されて日本語として理解できるのは喜ばしいことだ（日本語でも難しいが...）。彼の近年の発表の詳細がこの本には詰まっているから。

+ パケットを送信しないことより速くパケットを送信する方法は存在しない
+ パケットをより速く進ませることは不可能だが、より近い場所からの送信は可能
<div style="text-align:right">2章 TCPの構成要素より</div>

結局のところは、上記に尽きる。

1. HTTPリクエストを減らす
2. CDNを使う
<div style="text-align:right">高速サイトを実現する14のルール</div>

ハイパフォーマンスWebサイトで最も効果のある上位2つはネットワークに関することであり、ハイパフォーマンスブラウザネットワーキングでは、なぜそれがコストのかかることなのか、事細かに書かれている。

ネットワークを本気で学ぼうと思ったら一体何冊の本を読んだら良いかわからないが、本書はパフォーマンスとネットワークに絞ることで350Pと比較的コンパクトにまとまっている。けど、やっぱり重いので[電子書籍](http://www.oreilly.co.jp/books/9784873116761/)のほうを買ったほうがいいと思う、安いし。

また僕のバイブルが増えた。

---

Photo Credit: [Steppekiekendief (Circus macrourus) | Flickr](https://www.flickr.com/photos/rob_zweers/14091847074/in/photolist-ntfpbA-dZzrZ6-dibguj-diXabS-dibgmy-dibgFm-dibgaQ-dibiBk)

