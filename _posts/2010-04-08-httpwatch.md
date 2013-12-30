---
layout: post
title: HttpWatch 6.2 Basic Edtion
categories:
- performance
- translate
tags:
- http
status: publish
type: post
published: true
meta:
  pvc_views: '9859'
  _edit_last: '1'
  _wp_old_slug: httpwatch-6-2-basic-edtion
---
<img class="alignnone size-full wp-image-976" src="/static/blog/2010/04/httpwatch.png" alt="" width="210" height="205" />
<a href="http://www.httpwatch.com/">HttpWatch: An HTTP Viewer and HTTP Sniffer for IE and Firefox</a>

HttpWatchというWindowsのIE, Fxで動くツールがありまして、何をするもんかと言いますと、HTTPリクエストの流れをウォータホールチャートで確認できる代物です(Basic Editionは無料)。こんな具合に↓

<!--more-->

<img class="fig" src="/static/blog/2010/04/chart.png" alt="" width="442" height="246" />

んで、この赤いのやら緑ぃのやらはどうゆう意味やねんと思いまして、ツールヘルプを参照したら英語で書いてあったので、日本語でメモしといたのが以下。
<h3>Request Level Time Charts</h3>
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/blocked.png" alt="" width="75" height="18" /> Blocked</h4>
<strong>ブロックキング</strong>はプリプロセッシング（キャッシュを探したりなど）の時間を含んだり、ネットワーク接続が確立するまでの時間です。IE7とFirefox2は1つのホスト名（すなわちwww.microsoft.com）に対して、最大で2つの同時ネットワーク接続しかできないので、接続が確立するまでリクエストを待ち続けます。しばしば、ブロックキングは画像を含んだウェブページのダウンロード時間の最も重要な要因となります。
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/DNS.png" alt="" width="75" height="18" /> DNS Lookup</h4>
<strong>DNSルックアップ</strong>はホスト名（例：www.google.com）を数値であるIPアドレス（例：216.239.59.99）に変換するのに要する時間です。
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/connect.png" alt="" width="75" height="18" /> Connect</h4>
<strong>接続</strong>はWeb（もしくはProxy）サーバとTCP接続を確立するのに要する時間です。もし、セキュアなHTTPS接続ならば、これに<span style="color: #ff00ff;">*</span><em>SSLハンドシェイク</em>時間も含みます。Keep-Alive接続は一定時間Webサーバと接続することによって、必要以上の接続終了の負荷を回避します。

<span style="color: #888888;"><span style="color: #ff00ff;">*</span>認証／暗号化を含んだ一連の処理</span>
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/send.png" alt="" width="75" height="18" /> Send</h4>
<strong>送信</strong>はHTTPリクエストメッセージをサーバに送信するために必要な時間であり、送信するデータ量に依存します。例えば、長い送信時間の場合、HTTP POSTを使ってファイルをアップロードしていることが考えられます。
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/wait.png" alt="" width="75" height="18" /> Wait</h4>
<strong>待機</strong>はサーバからのレスポンスメッセージを待っている時間です。この値にはネットワークの遅延やHTTPリクエストをサーバに送る時間も含まれます。

<span style="color: #888888;">※ <strong>TTFB </strong>(Time To First Byte) = Connect + Send + Wait</span>
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/receive.png" alt="" width="75" height="18" /> Receive</h4>
<strong>受信</strong>はサーバからのレスポンスメッセージを読み込む時間です。この値は返されるコンテンツのサイズ、帯域幅、HTTP圧縮の使用の有無によって変化します。
<h4><img style="vertical-align: middle;" src="/static/blog/2010/04/cr.png" alt="" width="75" height="18" /> Cache Read</h4>
<strong>キャッシュ読み込み</strong>はブラウザキャッシュが存在する場合、もしくは304レスポンスが返された場合のコンテンツを読み込む時間です。

--

HTTPWatch以外にもこうゆうツールいっぱいあるわけだけど、リクエストのフロー自体はおんなじものを計測しているわけだから、他のツール理解にもつながったかなと。
<h3>参考サイト</h3>
<ul>
	<li>Safari のリソースパネルについての解説あり<a href="http://webkit.org/blog/197/web-inspector-redesign/">
Surfin’ Safari - Blog Archive » Web Inspector Redesign</a></li>
	<li>Firebug 接続タブの解説あり<a href="http://rensodevelopment.blogspot.com/2009/06/firebug-network-monitoring-quick.html">
Software Development Practices: Firebug Network Monitoring Quick Reference Guide</a></li>
</ul>
