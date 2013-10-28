---
layout: post
title: HTTPリクエストを減らすために【序章】HTTPリクエストは甘え
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
	<li><strong>【序章】HTTPリクエストは甘え</strong></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-css-sprite/">【CSS Sprite編】スプライト地獄からの解放</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-webfont/">【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-datauri/">【DataURI編】遅延ロードでレンダリングブロックを回避</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-one-second/">【終章】我々には1000msの猶予しか残されていない</a></li>
</ul>
1日目は、HTTPリクエストの概要について説明します。

例えに、私のポートフォリオページ（<a href="http://t32k.me/">http://t32k.me/</a>）が表示されるまでの流れを見て行きましょう。まず、ブラウザのURLバーにt32k.meと打ち込んで、アクセスします。検索からでも方法はなんでもよいのですが、そのページを見に行くということは、結局はt32k.meに対してhttpスキームでリクエストするということを意味しています。

<a href="http://www.slideshare.net/t32k/ss-15915114/27"><img class="size-full wp-image-5128 aligncenter" alt="HTTPリクエストの中身" src="http://t32k.me/mol/file/2013/08/requests.gif" width="640" height="400" /></a>

クライアントであるブラウザは、入力されたURLを判断して、リソース（この場合HTMLファイル）を要求しにいきます。このとき、t32k.meというドメインはあくまで人間が覚えやすいように考えられた仕組みなので、ブラウザはこれだけではリソースに到達出来ません。そこでドメインをIPアドレス（192.0.2.0とかそうゆうの）に正引き（変換）する必要性があります。この作業を<b>DNS Lookup</b>（名前解決）といいます。たいてい、ISPのDNSサーバーに問い合わせたりして解決します。

* DNS - Domain Name System

サーバーのIPアドレスが分かったので今度は、サーバーさんに接続しに行きます。クライアントは『サーバーさんいる？』と聞き、『サーバーはいるで！』と答えます。このやりとりを<strong>Connecting</strong>といいソケット接続が確立します。なぜ一発目からリクエストを通さないのかというと、それだと受け手の状況がわからないので通信の信頼性が担保されないからです。詳しくはTCPの<a href="http://ja.wikipedia.org/wiki/3%E3%82%A6%E3%82%A7%E3%82%A4%E3%83%BB%E3%83%8F%E3%83%B3%E3%83%89%E3%82%B7%E3%82%A7%E3%82%A4%E3%82%AF">スリーウェイハンドシェイク</a>という仕組みを調べてみてください。

* TCP - Transmission Control Protocol

サーバーとの接続が確立したので、ここでやっとHTTPリクエスト、つまりここでは、<span class="code">http://t32k.me/index.html</span>を要求します。動的ファイルだったらファイル生成などプロセスが走ります。それで見つけた・生成したファイルをクライアントに送信します。送信した最初のパケットがクライアントに届いた時点までが、<strong>Waiting</strong>の時間になります。

そして、最後のパケットが送り終えた時点までが、<strong>Receiving</strong>の時間になります。ここがいわゆるファイルのダウンロード時間にかかる時間です。

<img class="aligncenter size-full wp-image-5134" alt="network" src="http://t32k.me/mol/file/2013/08/network1.png" width="639" height="220" />

ちなみに、これらのタイミングにかかる時間は、<a href="https://developers.google.com/chrome-developer-tools/docs/network?hl=ja">Google ChromeのDeveloper ToolsのNetworkパネル</a>のTimingタブで確認出来ます。

このHTTPリクエストの中身を確認して重要なのは、クライアントとサーバーとのやりとりにかかる時間、ラウンドトリップタイム(RTT)と、リソースのダウンロードにかかる時間（DL）です。

* RTT - Round Trip Time

t32k.meのネットワークにかかる情報をまとめたHARファイルに保存して（DevToolsのネットワークパネル右クリックで保存）、<a href="http://www.softwareishard.com/har/viewer/">HAR Viewr</a>で見たものが以下です。分かりやすくするために、3G回線でエミュレートした結果を表示しています。

* HAR - <a href="http://www.softwareishard.com/blog/har-12-spec/">HTTP Archive format</a>

<img class="aligncenter size-full wp-image-5140" alt="har" src="http://t32k.me/mol/file/2013/08/har.png" width="977" height="366" />

どうでしょう、見た感じで、紫色のバーが多いことに気づきますよね。つまりWatitingに多くの時間がかかっていることが理解出来ます。これは、単純にサーバーの処理が遅くて時間がかかっているのではなく（かかっていることもありますが）、たいていはホスト名ごとの同時接続数に起因するものです。

ひとつの完全修飾ドメイン名 (FQDN: Fully Qualified Domain Name)に対して、同時接続できる数はたいてい6つまでです。これを超える数のリクエストがくると、7つ目のリクエストは、最初の6つのリクエスト処理がどれかが完了される間、待たなければなりません。この時間もWatitngにあたります。

<a href="http://www.browserscope.org/?category=network&amp;v=top-m&amp;ua=Android%202.3%2CAndroid%204%2CiPhone%205"><img class="aligncenter size-full wp-image-5138" alt="connections" src="http://t32k.me/mol/file/2013/08/connections.png" width="640" height="225" /></a>

このような仕組みのため、一般的に静的ファイルはstatic.t32k.meなどの別ドメインから読み込むことによって、この同時接続数の上限を最大化しようとするのがドメイン・シャーディング（Domain Sharding）という手法です。これにより並列ダウンロードできる数を増やし、リソースのWaitingを可能な限り少なくしています。並列ダウンロード数が増えるからと言って10個の違うドメインから読み込んだとすれば、クライアントの最大コネクション数を大きく超えて意味がなかったり、また最初に説明したDNSルックアップの時間が増えたりして逆に弊害をもたらすようになるので、2,3つあたりのドメインを使うのが無難です。

全てのHTTPリクエストで以上のようなことが行われているかというと、そうでもありませんが、HTTPリクエストをするということは非常にコストの高い行為だということがお分かり頂けたかと思います。

ネイティブアプリは初回のアプリダウンロードで、アプリ内にリソースがまとめているので、このようなことは気にしなくてもほぼ良いのですが、Webアプリとなると、いかにサーバーとクライアントのやりとりを減らすか、が問題になってきます。特にRTTに関しては、根本的に改善するにはサーバーをユーザーの近くに置く(Akamaiさんなど)ことしかできないので、フロントエンドの人間にとってはラウンドトリップさせないということが重要になってきます。

次回からはCSSスプライト、Webフォント、DataURIなど実践的なテクニックを使ってHTTPリクエストの減らし方について学んでいきます。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" target="_blank"><img alt="ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール" src="http://ecx.images-amazon.com/images/I/51hIDIWHmYL._SL160_.jpg" border="0" /></a></td>
<td valign="top"><span><span><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank">ハイパフォーマンスWebサイト</a>
Steve Souders </span></span>オライリージャパン2008-04-11

<a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank">Amazonで詳しく見る</a>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></td>
</tr>
</tbody>
</table>
