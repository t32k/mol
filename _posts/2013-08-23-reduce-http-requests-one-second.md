---
layout: post
title: HTTPリクエストを減らすために【終章】我々には1000msの猶予しか残されていない
categories:
- performance
tags: []
status: publish
type: post
published: true
excerpt: "このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっております。"
author:
  name: Koji Ishimoto
  twitter: t32k
  gplus: 104886596569728254273 
  bio: Front-end Developer
  image: t32k.png
---
このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっております。
<ul>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-overview/">【序章】HTTPリクエストは甘え</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-css-sprite/">【CSS Sprite編】スプライト地獄からの解放</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-webfont/">【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-datauri/">【DataURI編】遅延ロードでレンダリングブロックを回避</a></li>
	<li><strong>【終章】我々には1000msの猶予しか残されていない</strong></li>
</ul>
最終日は、我々フロントエンドデベロッパーに課せられた理想と現実のはざまについて冷静と情熱のあいだらへんで考えていきます。まずは下記のブログを読んでくださいませ。
<ul>
	<li><strong><a href="http://googlewebmastercentral-ja.blogspot.jp/2013/08/making-smartphone-sites-load-fast.html">スマートフォンサイトの読み込み速度を改善するために : Googleウェブマスターブログ</a></strong></li>
</ul>
まぁ読まなくてもいいのですが、ここで述べられている重要なことは2つです。
<ol>
	<li><strong>モバイルの平均読み込み時間は7秒</strong></li>
	<li><strong>しかし、ユーザーは1秒未満を求めている</strong></li>
</ol>
ということです。

平均読み込み時間は7秒というのは、<a href="http://t32k.me/mol/log/no-more-stopwatch/">Googleアナリティクスのサイトの速度</a>という機能がありまして、そこから集計、出されたデータによるものです。
<blockquote>入力に対して0.1秒以上1秒未満でコンピューターからの応答があるとき、我々はその間にコンピューターが結果を表示しようとしているように感じる。ユーザーは多少遅いとは思っても、1秒間は進行中の一連の自分の考えに集中したままでいる。

<a href="http://www.usability.gr.jp/alertbox/20091005_timeframes.html">http://www.usability.gr.jp/alertbox/20091005_timeframes.html</a></blockquote>
1秒未満というのは、ヤコブ・ニールセン博士というユーザビリティの偉い人がいるのですが、彼のブログで述べられていたことです。要は1秒以内にコンピューターから応答があった場合は、自分がそれをダイレクトに操作している感覚をあたえ、ユーザーエクスペリエンス的によろしいということです。それ以上の時間をかかってしまうとユーザーはストレスを抱え、タスクを放棄しかねないと言っています。

ということで、今回は1000msに挑戦してみよう！という内容です。

<img class="aligncenter size-full wp-image-5292" alt="life" src="/static/blog/2013/08/life.png" width="900" height="200" />
<ul>
	<li><a href=" http://www.webpagetest.org/result/130820_P5_K2H/"> WebPagetest Test Result - Tokyo : t32k.me</a></li>
</ul>
上記は私のサイトをWebPagetestにかけた結果（TOKYOリージョン、Chrome 3G回線をエミュレート）です。分かりやすくするために読み込むリソースをHTMLだけにしています（Image/CSS/JavaScript読み込んでいません）。しかし、それでも1.7秒近く読み込みに時間がかかっています。

※ 括弧内の文字はDevToolsでの名称を記述

<img class="aligncenter size-full wp-image-5295" alt="1stimeline" src="/static/blog/2013/08/1stimeline.png" width="824" height="243" />
<ul>
	<li><a href="https://developers.google.com/speed/docs/insights/mobile"><strong>Mobile Analysis in PageSpeed Insights - PageSpeed Insights</strong></a></li>
</ul>
さすがに1秒以内に読み込み完了するのは不可能に近いので、レンダリングを1秒以内にしようというのがGoogleさんの教えです。

ここに書かれていることに、3G回線だとラウンドトリップタイムが約200~300msかかると言われており、仮に200msとした場合、DNS Lookupに1回ラウンドトリップ、TCPコネクション接続に1回ラウンドトリップ、HTTPリクエストとレスポンスで1回ラウンドトリップと合計3回のラウンドトリップで必ず600msは消費します。Serverレスポンスタイムは完全のバックエンドのエンジニアさんの領域なので、 <a href="http://newrelic.com/">New Relic</a>とか使ってボトルネック見つけてね！としか言えません。

結局、我々フロントエンドに残された時間は200msしかありませんでした(´・ω・`)

<img class="aligncenter size-full wp-image-5296" alt="ps" src="/static/blog/2013/08/ps.png" width="970" height="430" />
<ul>
	<li><a href="https://developers.google.com/speed/pagespeed/insights/"><strong>PageSpeed Insights </strong></a></li>
</ul>
最近リニューアルしたPageSpeed Insightではモバイル版も評価してくれるようになりました。当然モバイル環境はシビアなのでデスクトップ評価と比べて点数は下がってしまいます。そこでは、モバイル版ならではのアドバイスもあり、200msでレンダリングするヒントになります。
<ul>
	<li><a href="https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent">Reduce the size of the above-the-fold content - PageSpeed Insights</a></li>
	<li><a href="https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery">Optimize CSS Delivery - PageSpeed Insights</a></li>
</ul>
これらが言っていることは、<a href="http://www.suzukikenichi.com/blog/above-the-fold%E3%81%A8%E3%81%AF/">above-the-fold</a> コンテンツを速く見せろと言っています。

above-the-fold 内にサードパーティなど重いコンテンツがあるのはアウトです。可能な限り軽くしなければなりません。ちなみにHTTPリクエスト・レスポンス、この場合、HTMLが200ms内でダウンロードされる前提ですが、Initial <a href="http://yougo.ascii.jp/caltar/%E3%82%A6%E3%82%A3%E3%83%B3%E3%83%89%E3%82%A6%E3%82%B5%E3%82%A4%E3%82%BA">TCP Window Size</a>が10の場合、<a href="http://yougo.ascii.jp/caltar/%E3%82%B9%E3%83%AD%E3%83%BC%E3%82%B9%E3%82%BF%E3%83%BC%E3%83%88">TCPスロースタート</a>のため1回目のレスポンスで送信できるサイズは<strong>14KB</strong>までです。それ以上のサイズとなると1回のラウンドトリップで収まりません。ですから、HTMLに重いインライン画像を記述するのはもってのほかであり、CSS/JSだけでなくHTMLのMinifyも考えなければなりません。
<p style="text-align: center;"><a href="http://chimera.labs.oreilly.com/books/1230000000545/ch02.html#SLOW_START"><img class="aligncenter size-full wp-image-5310" alt="tcp" src="/static/blog/2013/08/tcp.png" width="800" height="450" /></a></p>
HTMLが無事に1回のラウンドトリップで取得できても、残り200ms内にabove-the-foldのレンダリングを完成しなければなりません。ここでCSSファイルが必要となってくるのですが、CSSファイルがダウンロードされるまでレンダリングはブロックされます。あと200msしかないのにHTTPリクエストなんかできません。そう、HTTPリクエストは甘えです。そこで、above-the-foldエリアで必要なスタイルの記述だけをHTML内のstyle要素に記述し、残りのスタイルはlink要素で遅延読み込みするといったことが提案されています。前回の記事でやったようなことですね。

このように、ここまでやって初めて1000msでレンダリングが完成できるのです。サイトの運用上全てのページでこのような手法を取り入れることは不可能かもしれませんが、求められる理想を実現するにはここまでやらなければならない現実を認識してもらえればと思います。

初回の記事にHTTPリクエスト甘えと書きましたが、今回の手法は基本的にはHTMLのリクエスト1回しかしていません。そもそも、いかにリクエスト数を減らすか？と考えるのではなく、リクエストさせずにどうするか？と初めから考えといたほうがちょうど良いのかもしれません（それはそれは難しいことですが...）。

また、単純に読み込み時間を短縮するのではなく、体感速度をあげるのかといった視点からリソースの優先度を考えたり、あえてCSSを遅延読み込みするなどといったテクニックも必要なんだなと今回記事を書いていて勉強になりました。本当にありがとうございます（誰）

とはいっても<a href="http://d.hatena.ne.jp/Jxck/20130723/1374535593">QUIC, SPDY</a>や<a href="http://d.hatena.ne.jp/Jxck/20130815/1376571387">HTTP 2.0</a>が普及してくると、また話が違ってきますので、その辺もちゃんとキャッチアップしていかなければなりません。
<p style="text-align: center;"><a href="http://www.unisys.co.jp/services/usability/concept.html"><img class="size-full wp-image-5329 aligncenter" title="The Elements of User Experience　（Web UX 5階層モデル）via 日本ユニシス株式会社" alt="The Elements of User Experience" src="/static/blog/2013/08/concept_2.jpg" width="700" height="396" /></a></p>
一連の記事で最も言いたかったのはWebパフォーマンス対策において、これさえやっておけばよい！という銀の弾丸はないということです。HTTPリクエストの削減さえHTTPの仕様が変われば、気にしなくても良いかもしれません。また、レンダリングブロックされているのにもかかわらず読み込み時間だけ見ていて、読み込み時間は速くなったけど、体感速度は遅くなったってゆうことも十分ありえます。

1000msレンダリングに関してもabove-the-foldのデザインから考え直さないといけませんし、above-the-foldに何を載せるかなどはコンテンツ設計の段階からデベロッパーが関わらないと実現できません。ユーザーエクスペリエンスにおいてWebパフォーマンスを考慮することは、すべての段階、すべての役割の人間が責任をもっていかなければなりません。

日々の改善はミクロに行いつつも、時には一歩下がって全体から評価してみる。

なにごともバランスが重要です。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/1449344763/warikiru-22/" target="_blank"><img alt="High Performance Browser Networking: What Every Web Developer Should Know About Networking and Web Performance" src="http://ecx.images-amazon.com/images/I/51qXHNzsmhL._SL160_.jpg" border="0" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/High-Performance-Browser-Networking-Developer/dp/1449344763%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D1449344763" target="_blank">High Performance Browser Networking</a>
Ilya Grigorik </span>Oreilly &amp; Associates Inc

2013-08-22

<a style="line-height: 19px;" href="http://www.amazon.co.jp/High-Performance-Browser-Networking-Developer/dp/1449344763%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D1449344763" target="_blank">Amazonで詳しく見る</a><span style="line-height: 19px;">by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
