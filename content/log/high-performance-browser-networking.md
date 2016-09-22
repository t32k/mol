---
date: 2014-05-23
title: ハイパフォーマンス ブラウザネットワーキング
subtitle: ネットワークアプリケーションのためのパフォーマンス最適化
categories: 
    - books
excerpt: "『ハイパフォーマンス ブラウザネットワーキング――ネットワークアプリケーションのためのパフォーマンス最適化』を読んだ、というか読んでいる、読まないわけがない"
---

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/51x2sA8N%2BTL._SL160_.jpg" alt="ハイパフォーマンス ブラウザネットワーキング ―ネットワークアプリケーションのためのパフォーマンス最適化" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/" name="azlinklink" target="_blank">ハイパフォーマンス ブラウザネットワーキング</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.1.16</div></div><div class="azlink-detail">Ilya Grigorik,和田 祐一郎,株式会社プログラミングシステム社<br />オライリージャパン<br />売り上げランキング: 113860<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>


Ilya Grigorik氏の『ハイパフォーマンス ブラウザネットワーキング』が発売されたので流し読んでみた感想。

## Design Fast Websites

<div class="fluid"><iframe src="//www.youtube.com/embed/7HC3OV1dDZ4" allowfullscreen></iframe></div>

思い起こせば、僕がWebパフォーマンスに興味を持ったのは2008年にYUI Theaterで公開されたNicole Sullivan氏の『Design Fast Websites』の動画を見てからだ。

当時Webデザイナーだった僕にとってデザインもWebパフォーマンスに貢献出来るんだ！決してバックエンドのエンジニアだけの問題じゃないんだと知ったのは衝撃的であり、それと同時にやりがいのあることだと感じモチベーションが上がったのを今でも覚えている。クリスマス・イブの夜のことだった。

## High Performance Web Sites

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/51hIDIWHmYL._SL160_.jpg" alt="ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" name="azlinklink" target="_blank">ハイパフォーマンスWebサイト</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.1.16</div></div><div class="azlink-detail">Steve Souders,スティーブ サウダーズ<br />オライリージャパン<br />売り上げランキング: 216930<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

それから、フロントエンドのパフォーマンスつながりで、Steve Souders氏の『ハイパフォーマンスWebサイト』を手にとって夢中で読んだのが5年前。以後、僕の口癖は『HTTPリクエストを減らす』になった。

## Perfmatters

![](/mol/images/2014/05-23-fig01.png)

最近ではフロントエンドのパフォーマンスも細分化されてきて、Network、Render、Computeの3つに大別されるようになってきたが、僕はやっぱり『HTTPリクエストを減らす』の精神でネットワークの分野に一番興味があるし、大抵の場合においてネットワークが問題の主要な要因になってるのは間違いないと思っている。

+ [HTTPリクエストを減らすために【序章】HTTPリクエストは甘え — MOL](https://t32k.me/mol/log/reduce-http-requests-overview/)
+ [HTTPリクエストを減らすために【終章】我々には1000msの猶予しか残されていない — MOL](https://t32k.me/mol/log/reduce-http-requests-one-second/)

そんなとき、いつも参考にしてきたのがIlya Grigorik氏の記事であったりスライド・動画だ。

+ [Ilya Grigorik - YouTube](https://www.youtube.com/user/igrigorik/videos)

彼はとてもスマートでしっかりとした根拠を持って、いつも発表しているので、とても尊敬しているのだが、なにぶん難しいテーマなので、今回、『High Performance Browser Networking』が邦訳されて日本語として理解できるのは喜ばしいことだ（日本語でも難しいが...）。彼の近年の発表の詳細がこの本には詰まっているから。

> + パケットを送信しないことより速くパケットを送信する方法は存在しない
+ パケットをより速く進ませることは不可能だが、より近い場所からの送信は可能

結局のところは、上記に尽きる。

> 1. HTTPリクエストを減らす
2. CDNを使う

ハイパフォーマンスWebサイトで最も効果のある上位2つはネットワークに関することであり、ハイパフォーマンスブラウザネットワーキングでは、なぜそれがコストのかかることなのか、事細かに書かれている。

ネットワークを本気で学ぼうと思ったら一体何冊の本を読んだら良いかわからないが、本書はパフォーマンスとネットワークに絞ることで350Pと比較的コンパクトにまとまっている。けど、やっぱり重いので[電子書籍](http://www.oreilly.co.jp/books/9784873116761/)のほうを買ったほうがいいと思う、安いし。

また僕のバイブルが増えた。