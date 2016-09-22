---
date: 2013-08-06
title: CharlesでBandwidth Throttlingを設定しChrome for AndroidでRemote Debugする
subtitle:
categories: 
    - development
excerpt: 僕のAndroid端末は3G回線契約していない、いわゆる白ロムなので、WiFiしか使えない。これだと、3G回線の低速さが体感できない、低帯域でどうアプリケーションが振る舞うのかわからないので不便だ。ということで、CharlesでBandwidth Throttlingできたよねと思い、組み合わせて使ってみる。
ogimage: /static/blog/2013/08/bs1.png
---

とりあえず表題のようなことがしたい。[Chrome for AndroidでRemote Debuggingは以前の記事](https://t32k.me/mol/log/remote-debugging-with-chrome-for-android/)でも紹介したとおりだ。

僕のAndroid端末は3G回線契約していない、いわゆる白ロムなので、WiFiしか使えない。これだと、3G回線の低速さが体感できない、低帯域でどうアプリケーションが振る舞うのかわからないので不便だ。ということで、CharlesでBandwidth Throttlingできたよねと思い、組み合わせて使ってみる。

## ADBPlugin

まず、おさらい的なことで、Chrome for AndroidでRemote DebugをするためにはADB（Android Debug Bridge ）が必要だ。これは通常、Android SDKの中に入っていて、SDKまるごと落としてこなきゃいけなかったけど、最近じゃ、ADBを内包したChrome Extensionで提供されているらしく、これをインストールするだけだお。面倒なpathも通さなくても簡単に使えるようになってる。

+ [GoogleChrome/ADBPlugin](https://github.com/GoogleChrome/ADBPlugin/)
+ [ADB - Chrome ウェブストア](https://chrome.google.com/webstore/detail/adb/dpngiggdglpdnjdoaefidgiigpemgage)

あとは前回紹介したようにChromeで調べるだけ。便利な世の中になったもんだ。詳細は下記リンク参照。

+ [Remote Debugging on Android with Chrome - Google Chrome](https://developer.chrome.com/devtools/docs/remote-debugging?hl=ja#remote-debugging-beta)

## Bandwidth Throttling - Charles

![](/static/blog/2013/08/bs1.png)

Charlesはよく使うツール。といっても、デスクトップでこの機能使うくらいなんだけど。詳しい使い方はこもりさんの記事がわかりやすい。

+ [Charles Web Debugging Proxy の使い方 | gaspanik weblog](http://blog.gaspanik.com/how-to-setup-charles-web-debugging-proxy)

とりあえず、実機の端末はこのCharlesを通してインターネッツに羽ばたけば良いわけです。重要なのはCharelsが入ってるMacのIPアドレスと、ポート番号（ここではとりあえず8888にしときましょう）です。

![](/static/blog/2013/08/network.png)

ちなみに、MacでIPアドレスを確認したい場合は、システム環境設定 ＞ ネットワーク ＞ 詳細 ＞ TCP/IPでみれます。で、このIPをAndroidの端末に設定してあげれば行けるわけですね。けど、記事にはiOSの設定しか書いてない！ということでググったらネットワークの部分長押しでプロキシ設定項目がでてくるらしい...

+ [忘れないように 『プロキシ設定』｜スイーツ＠インデックス リバース](http://ameblo.jp/yongmars/entry-11339671898.html)

![](/static/blog/2013/08/ss.png)

どうでもいいけど、[Android 4.2で「開発者向けオプション」を表示する方法](http://juggly.cn/archives/75086.html)とかも分かりにくいよね... とりあえず、できました。ありがとうございました。











