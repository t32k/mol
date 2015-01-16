---
date: 2013-08-06
title: Chrome CanaryとAndroid Debug BridgeとChrome for Android betaでReverse Port Forwarding
categories: development
---
<img class="alignnone size-full wp-image-5100" title="debug" src="/static/blog/2013/08/debug.png" alt="" width="900" height="200" />

最近、横文字タイトルがマイブームです、@t32kです。要はReverse Port Forwardingしたいのです。

<a href="http://t32k.me/mol/log/charles-bandwidth-throttling/">前回の記事で</a>久しぶりに、<a href="https://developers.google.com/chrome-developer-tools/docs/remote-debugging?hl=ja#reverse-port-forwarding">Remote Debugging on Androidの記事を読んでたらReverse Port Forwarding</a>って新しい項目ができてるのを見つけたじゃないですかー、気になるじゃないですかー、ためしてみるじゃないですかー。
<blockquote>Commonly you have a web server running on your local development machine, and you want to connect to that site from your device. If the mobile device and the development machine are on the same network, this is straightforward.</blockquote>
Reverse Port Forwardingってのがなんなのかはよくわかってないですが、よくローカルに静的なサーバーたちあげてマークアップして、iOSシミュレータとかで確認してるんですけど、これ実機で確認できればなーと思ってたんですよね。Chromeだとできるってよ、これ。
<ul>
	<li>デスクトップにChrome Canary</li>
	<li>Android Debug Bridge (ADBPlugin or full Android SDK)</li>
	<li>検証端末にChrome for Android beta</li>
</ul>
必要な物は上記です、Canaryとbetaが必要なんですね。ADBPluginって書いてあるけど、拡張機能からだとうまくいかなかったので、おとなしくコマンド叩いた。とりあえずADBを起動させておく。

<img class="alignnone size-full wp-image-5102" title="flag" src="/static/blog/2013/08/flag.png" alt="" width="850" height="134" />

まず、Canaryで<strong> chrome://flags</strong> を開いて、『<strong>デベロッパー ツールのテストを有効にする</strong>』にします。<strong>#enable-devtools-experiments</strong> で検索すればいいよ。再起動もしておく。

<img class="alignnone size-full wp-image-5103" title="port" src="/static/blog/2013/08/port.png" alt="" width="768" height="423" />

<strong>chrome://inspect</strong> を開くと、USBで繋いだChrome for Android betaで開いているサイトが出てくるので、そこの上の『<strong>Enable port forwarding</strong>』にチェック！（記事にはDevToolsのSettings Panelって書いてあってフェイントくらった）Configure port forwardingで、port:8080, IP adrress andport: 127.0.0.1:8080をにする。

あとは、開発環境で<strong>python -m SimpleHTTPServer 8080</strong>とかでサーバー立てたり、<a href="https://github.com/t32k/maple#-grunt-tasks">Maple使ってる人はgrunt developす</a>るだけで立っちゃう！で、あとは端末で、http://localhost:8080/にアクセスすれば、実機で開発マシンのファイルを検証することができるよ！！！！

<img class="alignnone size-full wp-image-5105" title="xperia" src="/static/blog/2013/08/xperia.jpg" alt="" width="800" height="450" />
