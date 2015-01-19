---
date: 2013-08-19
title: HTTPリクエストを減らすために【序章】HTTPリクエストは甘え
subtitle: You have to reduce number of HTTTP requests.
categories: performance
excerpt: 1日目は、HTTPリクエストの概要について説明します。
ogimage: http://t32k.me/static/blog/2013/08/requests.gif
---

このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっている。

+ __【序章】HTTPリクエストは甘え__
+ [【CSS Sprite編】スプライト地獄からの解放](/mol/log/reduce-http-requests-css-sprite/)
+ [【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ](/mol/log/reduce-http-requests-webfont/)
+ [【DataURI編】遅延ロードでレンダリングブロックを回避](/mol/log/reduce-http-requests-datauri/)
+ [【終章】我々には1000msの猶予しか残されていない](/mol/log/reduce-http-requests-one-second/)

1日目は、HTTPリクエストの概要について説明する。

例えに、私の[ポートフォリオページ](http://t32k.me/)（t32k.me）が表示されるまでの流れを見ていく。まず、検索からでも方法はなんでもよいが、ブラウザのURLバーにt32k.meと打ち込んでアクセスする。そのページを見にいくということは、つまりt32k.meに対してHTTPスキームでリクエストするということを意味している。

![HTTPリクエストの流れ](http://t32k.me/static/blog/2013/08/requests.gif)

クライアントであるブラウザは入力されたURLを判断して、リソース（この場合、HTMLファイル）を要求しにいきます。このとき、t32k.meというドメインはあくまで人間が覚えやすいように考えられた名前なので、ブラウザはこれだけではリソースに到達出来ない。

そこで、この名前であるドメインをIPアドレス（eg. 192.0.2.0）に正引き（変換）する必要性がある。この作業を__DNS Lookup__（名前解決）という。たいていISPのDNSサーバーに問い合わせたりして解決する。

+ DNS - Domain Name System

IPアドレスが分かったので今度はサーバーに接続しにいく。クライアントは『サーバーさんいる？』と聞き、サーバーは『いるで！』と答える。このやりとりを__Connecting__といい、ソケット接続が確立することを意味する。

なぜ最初からリクエストを通さないのかというと、それだと受け手の状況がわからないので通信の信頼性が担保されないからだ。詳しくはTCPの[スリーウェイハンドシェイク](http://ja.wikipedia.org/wiki/3%E3%82%A6%E3%82%A7%E3%82%A4%E3%83%BB%E3%83%8F%E3%83%B3%E3%83%89%E3%82%B7%E3%82%A7%E3%82%A4%E3%82%AF)という仕組みを参照。

+ TCP - Transmission Control Protocol

サーバーとの接続が確立したので、ここでやっとHTTPリクエスト、つまり、`index.html`を要求する。このとき、動的ファイルだったらファイル生成などプロセスが走る。そのあと見つけた・生成したファイルをクライアントに送信する。送信した最初のパケットがクライアントに届いた時点までが、__Waiting__の時間になる。

そして最後のパケットが送り終えた時点までが、__Receiving__の時間になる。ここがいわゆるファイルのダウンロード時間にかかる時間。

![リクエストの段階](http://t32k.me/static/blog/2013/08/network1.png)

ちなみに、これらのタイミングにかかる時間は[Google ChromeのDeveloper ToolsのNetworkパネル](https://developer.chrome.com/devtools/docs/network?hl=ja)のTimingタブで確認できる。

このHTTPリクエストの中身を確認して言えることは、クライアントとサーバーとのやりとりにかかる時間、ラウンドトリップタイム(RTT)と、リソースのダウンロードにかかる時間（DL）が重要だということ。

+ RTT - Round Trip Time

t32k.meのネットワークにかかる情報をまとめたHARファイルに保存して（DevToolsのネットワークパネルで右クリック保存）、[HAR Viewr](http://www.softwareishard.com/har/viewer/)で見たものが以下。分かりやすくするために、3G回線でエミュレートした結果を表示している。

+ HAR - [HTTP Archive format](http://www.softwareishard.com/blog/har-12-spec/)

![HAR例](http://t32k.me/static/blog/2013/08/har.png)

どうだろうか、見た感じで紫色のバーが多いことに気づくことだろう。つまり__Watitingに多くの時間がかかっている__ことが理解できる。これは単純にサーバーの処理が遅くて時間がかかっているのではなく（かかっているあるが）、たいていはホスト名ごとの同時接続数に起因するものだ。

ひとつの完全修飾ドメイン名 (FQDN: Fully Qualified Domain Name)に対して、同時接続できる数はたいてい6つまでだ。これを超える数のリクエストがくると、7つ目のリクエストは、最初の6つのリクエスト処理がどれかが完了される間、待たなければならない。この時間も待ち時間になる。

![各ブラウザの接続数上限](http://t32k.me/static/blog/2013/08/connections.png)

このような制限のため、静的ファイルはstatic.t32k.meなどの別ドメインから読み込むことによって、この同時接続数の上限を最大化しようとするのがドメイン・シャーディング（Domain Sharding）という手法が一般的にとられる。

このおかげで並列ダウンロードできる数を増やし、リソースのWaitingを可能な限り少なくしている。並列ダウンロード数が増えるからといって、例えば10個の違うドメインから読み込んだとすれば、クライアントの最大コネクション数を大きく超えて意味がなかったり、また最初に説明したDNSルックアップの時間が増えたりして、逆に弊害をもたらすようになるので、2,3つあたりのドメインを使うのが無難だろう。

すべてのHTTPリクエストで以上のようなことが行われているかというと、そうでもないだろうが、HTTPリクエストをするということは非常にコストの高い行為だということが分かって頂けたかと思う。

ネイティブアプリは初回のアプリダウンロードで、アプリ内にリソースがまとめているので、このようなことは気にしなくてもほぼ良いだろう。しかしWebアプリとなると、いかにサーバーとクライアントのやりとりを減らすか、がボトルネックとなる。特にRTTに関しては、根本的に改善するにはサーバーをユーザーの近くに置く(Akamai等)ことしかできないので、フロントエンドの人間にとっては__ラウンドトリップさせない__ということが重要になってくる。

次回からはCSSスプライト、Webフォント、DataURIなど実践的なテクニックを使ってHTTPリクエストの減らし方について学んでいきます。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51hIDIWHmYL._SL160_.jpg" alt="ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" name="azlinklink" target="_blank">ハイパフォーマンスWebサイト</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.1.18</div></div><div class="azlink-detail">Steve Souders<br />オライリージャパン<br />売り上げランキング: 156067<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>