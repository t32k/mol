---
date: 2013-08-23
title: HTTPリクエストを減らすために【終章】我々には1000msの猶予しか残されていない
subtitle: Optimize CSS Delivery
categories: performance
excerpt: 最終日は、我々フロントエンドデベロッパーに課せられた理想と現実のはざまについて冷静と情熱のあいだらへんで考えていきます。まずは下記のブログを読んでくださいませ。
ogimage: http://t32k.me/static/blog/2013/08/tcp.png
---

このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっている。

+ [【序章】HTTPリクエストは甘え](/mol/log/reduce-http-requests-overview/)
+ [【CSS Sprite編】スプライト地獄からの解放](/mol/log/reduce-http-requests-css-sprite/)
+ [【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ](/mol/log/reduce-http-requests-webfont/)
+ [【DataURI編】遅延ロードでレンダリングブロックを回避](/mol/log/reduce-http-requests-datauri/)
+ __【終章】我々には1000msの猶予しか残されていない__


最終日は、我々フロントエンドデベロッパーに課せられた理想と現実のはざまについて冷静と情熱のあいだらへんで考えていく。まずは下記のブログを読んでもらいたい。

+ [Google ウェブマスター向け公式ブログ: スマートフォンサイトの読み込み速度を改善するために](http://googlewebmastercentral-ja.blogspot.jp/2013/08/making-smartphone-sites-load-fast.html)

まぁ読まなくてもいいのだが、ここで述べられている重要なことは2つ。

1. __モバイルの平均読み込み時間は7秒__
2. __しかし、ユーザーは1秒未満を求めている__

平均読み込み時間の7秒というのは、[Googleアナリティクスのサイトの速度](/mol/log/no-more-stopwatch/)という機能があって、そこから集計し出されたデータによるものだ。

> 入力に対して0.1秒以上1秒未満でコンピューターからの応答があるとき、我々はその間にコンピューターが結果を表示しようとしているように感じる。ユーザーは多少遅いとは思っても、1秒間は進行中の一連の自分の考えに集中したままでいる。

+ [10の累乗： ユーザーエクスペリエンスにおける時間スケール － U-Site](http://www.usability.gr.jp/alertbox/20091005_timeframes.html)

1秒未満というのはヤコブ・ニールセン博士というユーザビリティの偉い人がいるのだが、彼のブログで述べられていたことだ。要は1秒以内にコンピューターから応答があった場合は、自分がそれをダイレクトに操作している感覚をあたえ、ユーザーエクスペリエンス的によろしいということ。それ以上の時間をかかってしまうとユーザーはストレスを抱え、タスクを放棄しかねないと言っている。

ということで、今回は1000msに挑戦してみよう！という内容。

![](http://t32k.me/static/blog/2013/08/life.png)

※ 括弧内の文字はDevToolsでの名称を記述

+ [WebPagetest Test Result - Tokyo : t32k.me/ - 08/20/13 05:04:45](http://www.webpagetest.org/result/130820_P5_K2H/)

上記は私のサイトをWebPagetestにかけた結果（TOKYOリージョン、Chrome 3G回線をエミュレート）。分かりやすくするために読み込むリソースをHTMLだけにしている（Image/CSS/JavaScript読み込んでいない）。しかし、それでも1.7秒近く読み込みに時間がかかっている。

![](http://t32k.me/static/blog/2013/08/1stimeline.png)

+ [PageSpeed Insights でのモバイル解析 — Google Developers](https://developers.google.com/speed/docs/insights/mobile)

さすがに1秒以内に読み込み完了するのは不可能に近いので、レンダリングを1秒以内にしようというのがGoogleさんの教え。

ここに書かれていることに、3G回線だとラウンドトリップタイムが約200~300msかかると言われており、仮に200msとした場合、DNS Lookupに1回ラウンドトリップ、TCPコネクション接続に1回ラウンドトリップ、HTTPリクエストとレスポンスで1回ラウンドトリップと合計3回のラウンドトリップで必ず600msは消費する。

Serverレスポンスタイムは完全のバックエンドのエンジニアさんの領域なので、 New Relicとか使ってボトルネック見つけてね！としか僕からは言えない。

結局、我々フロントエンドに残された時間は200msしかない(´・ω・`)

[![PageSpeed Insights](http://t32k.me/static/blog/2013/08/ps.png)](https://developers.google.com/speed/pagespeed/insights/)

最近リニューアルしたPageSpeed Insightではモバイル版も評価してくれる。当然モバイル環境はシビアなのでデスクトップ評価と比べて点数は下がってしまう。そこではモバイル版ならではのアドバイスもあり、200msでレンダリングするヒントになる。

+ [スクロールせずに見える範囲のコンテンツのサイズを削減する — Google Developers](https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent)
+ [CSS の配信を最適化する — Google Developers](https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery)

これらの記事で述べられていることは、[above-the-fold](https://www.suzukikenichi.com/blog/above-the-fold%E3%81%A8%E3%81%AF/)コンテンツを速く見せろということ。

above-the-fold内にサードパーティなど重いコンテンツがあるのはアウト。可能な限り軽くしなければならない。ちなみにHTTPリクエスト・レスポンス、この場合、HTMLが200ms内でダウンロードされる前提だが、[InitialTCP Window Size](http://yougo.ascii.jp/caltar/%E3%82%A6%E3%82%A3%E3%83%B3%E3%83%89%E3%82%A6%E3%82%B5%E3%82%A4%E3%82%BA)が10の場合、[TCPスロースタート](http://yougo.ascii.jp/caltar/%E3%82%B9%E3%83%AD%E3%83%BC%E3%82%B9%E3%82%BF%E3%83%BC%E3%83%88)のため1回目のレスポンスで送信できるサイズは__14KB__まで。それ以上のサイズとなると1回のラウンドトリップで収まらない。だから、HTMLに重いインライン画像を記述するのはもってのほかであり、CSS/JSだけでなくHTMLのMinifyも考えなければならない。

![](http://t32k.me/static/blog/2013/08/tcp.png)

HTMLが無事に1回のラウンドトリップで取得できても、残り200ms内にabove-the-foldのレンダリングを完成しなければならない。ここでCSSファイルが必要となってくるのだが、CSSファイルがダウンロードされるまでレンダリングはブロックされる。

あと200msしかないのにHTTPリクエストなんかできない。そう、HTTPリクエストは甘えだ。そこで、above-the-foldエリアで必要なスタイルの記述だけをHTML内のstyle要素に記述し、残りのスタイルはlink要素で遅延読み込みするといったことが提案されている。前回の記事でやったようなことだ。

このように、ここまでやって初めて1000msでレンダリングが完成できるのだ。サイトの運用上全てのページでこのような手法を取り入れることは不可能かもしれないが、求められる理想を実現するにはここまでやらなければならない現実を認識してもらえればと思う。

初回の記事にHTTPリクエスト甘えと書いたが、今回の手法は基本的にはHTMLのリクエスト1回しかしていない。そもそも、いかにリクエスト数を減らすか？と考えるのではなく、リクエストさせずにどうするか？と初めから考えといたほうがちょうど良いのかもしれない（それはそれは難しいことだが…）。

また、単純に読み込み時間を短縮するのではなく、体感速度をあげるのかといった視点からリソースの優先度を考えたり、あえてCSSを遅延読み込みするなどといったテクニックも必要なんだなとも感じる。

とはいってもQUIC, SPDYやHTTP 2.0が普及してくると、また話が違ってくるので、その辺もちゃんとキャッチアップしていかなければならない。

![](http://t32k.me/static/blog/2013/08/concept_2.jpg)

一連の記事で最も言いたかったのはWebパフォーマンス対策において、これさえやっておけばよい！という銀の弾丸はないということだ。HTTPリクエストの削減さえHTTPの仕様が変われば、気にしなくても良いかもしれない。

またレンダリングブロックされているのにもかかわらず読み込み時間だけ見ていて、読み込み時間は速くなったけど、体感速度は遅くなったってゆうことも十分ありえる。

1000msレンダリングに関してもabove-the-foldのデザインから考え直さないといけないし、above-the-foldに何を載せるかなどはコンテンツ設計の段階からデベロッパーが関わらないと実現できない。ユーザーエクスペリエンスにおいてWebパフォーマンスを考慮することは、すべての段階、すべての役割の人間が責任をもっていかなければならない。

日々の改善はミクロに行いつつも、時には一歩下がって全体から評価してみる。なにごともバランスが重要だ。


<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51x2sA8N%2BTL._SL160_.jpg" alt="ハイパフォーマンス ブラウザネットワーキング ―ネットワークアプリケーションのためのパフォーマンス最適化" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/" name="azlinklink" target="_blank">ハイパフォーマンス ブラウザネットワーキング</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.1.26</div></div><div class="azlink-detail">Ilya Grigorik,和田 祐一郎,株式会社プログラミングシステム社<br />オライリージャパン<br />売り上げランキング: 169563<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>




