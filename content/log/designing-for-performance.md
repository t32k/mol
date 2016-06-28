---
date: 2016-06-28
title: パフォーマンス向上のためのデザイン設計
subtitle: Designing for Performance
categories: 
    - books
hero: /mol/images/2016/0628-hero.jpg
excerpt: Webサイトのパフォーマンスは、「9:1でフロントエンド側のパフォーマンスが重要」だと言われています。パフォーマンスの向上には、インフラ側だけでなくフロントエンドの設計が大いに影響します。
ogimage: http://ecx.images-amazon.com/images/I/51ckdAnKBoL.jpg
---

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873117550/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="http://ecx.images-amazon.com/images/I/51ckdAnKBoL._SL160_.jpg" alt="パフォーマンス向上のためのデザイン設計" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873117550/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">パフォーマンス向上のためのデザイン設計</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2016.6.27</div></div><div class="azlink-detail">Lara Callender Hogan,西脇 靖紘,星野 靖子<br />オライリージャパン<br />売り上げランキング: 4769<br /></div><div class="azlink-review" style="margin-top:10px;margin-bottom:10px"></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873117550/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

<small>画像： [Tufted coquette - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Tufted_coquette)</small>

ハンドメイドマーケットプレイスを運営し、Webパフォーマンスの取り組みが素晴らしいことでも有名な[Etsy社のエンジニアリング](https://codeascraft.com/)マネージャーが書いた本。フロントエンドのパフォーマンスと言うと、Steve Souders氏の『[ハイパフォーマンスWebサイト](https://www.amazon.co.jp/dp/487311361X/?tag=warikiru-22)』は有名で基本的なことは原則は変わってはいないが、原著が出版されたのが2007年と考えるといささか古い。

『Googleの検索結果で何秒遅れたら〜』、『Amazonのサイトで何秒遅れたら〜』と言った聞き飽きた事例などが本書ではアップデートされ、新しい事例や、比較的最近のフロントエンド技術が紹介されており、とっつきやすくなっている。ただ原著の出版されたのが2014年12月なので[AMP](https://www.ampproject.org/)みたいな最新のものは解説されていないが、監訳者著の付録でHTTP2の話にも触れてあるので、良いと思う。

まぁ、特に目新しい内容はないが、本書はデザイナーに向けて書かれていることに意味がある。Webデザイナーと呼ばれる職種の人が本書に記載されてる内容を実装まで理解する必要はないと思うが（実装はフロントエンドエンジニアに任せればいい）、Webサイト・アプリケーションをデザインする上で一般教養として知ってほしい内容ばかりだと思う。フロントエンドエンジニアはさらっと読んで知らない・見逃してる技術がないか確認するために読んでもいいと思う。

目新しかったのは、Webパフォーマンス対策していくにあたって、8章の『**組織の風土を変えていく**』だ。フロントエンドのパフォーマンスというが、実際のところはフロントエンドエンジニアとして、できることは少ないと感じている。いや、効果のある対策は他の職種と協力しなければならないことが多い。例えば、バナー画像がファイルサイズが重ければ、デザイナーさんに画質の調整や保存形式を変更するようお願いしたり、キャッシュ制御のためexpireやgzip設定をインフラエンジニアさんにお願いしたりと、組織全体の協力が必要だし、実際そうゆうことを何度もしてきた。

そうゆうわけで、本書では偉い人を巻き込んだりする方法が書かれてたりする。百聞には一見にしかずというが、やっぱり、そうゆう人たちには比較動画やfilmstrip的なものを見せると良い。本書に書かれていることは、たいてい実践してきたつもりなので、自分のブログのPerformanceタグの記事を参考にしてもらいたい。

- [Performance - MOL](http://localhost:1313/mol/categories/performance/)

コンパクトに比較的最近のパフォーマンス事情が分かる良い書籍なので、ぜひ組織に一冊、部署ごとに一冊置いておくと良いかと思う。
