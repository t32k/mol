---
date: 2013-08-06
title: Chrome CanaryとAndroid Debug BridgeとChrome for Android betaでReverse Port Forwarding
categories: 
    - development
---

![](/static/blog/2013/08/debug.png)

最近、横文字タイトルがマイブームです、@t32kです。要はReverse Port Forwardingしたいのです。

[前回の記事](/mol/log/charles-bandwidth-throttling/)で久しぶりに、[Remote Debugging on Androidの記事を読んでたらReverse Port Forwarding](https://developers.google.com/chrome-developer-tools/docs/remote-debugging?hl=ja#reverse-port-forwarding)って新しい項目ができてるのを見つけたじゃないですかー、気になるじゃないですかー、ためしてみるじゃないですかー。

> Commonly you have a web server running on your local development machine, and you want to connect to that site from your device. If the mobile device and the development machine are on the same network, this is straightforward.

Reverse Port Forwardingってのがなんなのかはよくわかってないですが、よくローカルに静的なサーバーたちあげてマークアップして、iOSシミュレータとかで確認してるんですけど、これ実機で確認できればなーと思ってたんですよね。Chromeだとできるってよ、これ。


- デスクトップにChrome Canary
- Android Debug Bridge (ADBPlugin or full Android SDK)
- 検証端末にChrome for Android beta

必要な物は上記です、Canaryとbetaが必要なんですね。ADBPluginって書いてあるけど、拡張機能からだとうまくいかなかったので、おとなしくコマンド叩いた。とりあえずADBを起動させておく。

![](/static/blog/2013/08/flag.png)

まず、Canaryで<strong> chrome://flags</strong> を開いて、『<strong>デベロッパー ツールのテストを有効にする</strong>』にします。<strong>#enable-devtools-experiments</strong> で検索すればいいよ。再起動もしておく。

![](/static/blog/2013/08/port.png)

`chrome://inspect` を開くと、USBで繋いだChrome for Android betaで開いているサイトが出てくるので、そこの上の『<strong>Enable port forwarding</strong>』にチェック！（記事にはDevToolsのSettings Panelって書いてあってフェイントくらった）Configure port forwardingで、`port:8080, IP adrress andport: 127.0.0.1:8080` をにする。

あとは、開発環境で`python -m SimpleHTTPServer 8080`とかでサーバー立てたりすればいいじゃん。

![](/static/blog/2013/08/xperia.jpg)
