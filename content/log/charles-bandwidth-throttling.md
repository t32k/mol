---
date: 2013-08-06
title: CharlesでBandwidth Throttlingを設定しChrome for AndroidでRemote Debugする
subtitle:
categories: development
excerpt:
ogimage:
---

とりあえず表題のようなことがしたい。

<a href="http://t32k.me/mol/log/remote-debugging-with-chrome-for-android/">Chrome for AndroidでRemote Debuggingは以前の記事</a>でも紹介したとおりだ。

僕のAndroid端末は3G回線契約していない、いわゆる白ロムなので、WiFiしか使えない。これだと、3G回線の低速さが体感できない、低帯域でどうアプリケーションが振る舞うのかわからないので不便だ。ということで、CharlesでBandwidth Throttlingできたよねと思い、組み合わせて使ってみる。
<h2>ADBPlugin</h2>
まず、おさらい的なことで、Chrome for AndroidでRemote DebugをするためにはADB（Android Debug Bridge ）が必要だ。これは通常、Android SDKの中に入っていて、SDKまるごと落としてこなきゃいけなかったけど、最近じゃ、ADBを内包したChrome Extensionで提供されているらしく、これをインストールするだけだお。面倒なpathも通さなくても簡単に使えるようになってる。
<ul>
	<li><a href="https://github.com/GoogleChrome/ADBPlugin/">GoogleChrome/ADBPlugin </a></li>
	<li><a href="https://chrome.google.com/webstore/detail/adb/dpngiggdglpdnjdoaefidgiigpemgage">Chrome ウェブストア - ADB </a></li>
</ul>
あとは前回紹介したようにChromeで調べるだけ。便利な世の中になったもんだ。

詳細は下記リンク参照。
<ul>
	<li><a href="https://developers.google.com/chrome-developer-tools/docs/remote-debugging?hl=ja#remote-debugging-beta">Remote Debugging on Android - Chrome DevTools — Google Developers</a></li>
</ul>
<h2>Bandwidth Throttling - Charles <span style="font-size: 13px;"> </span></h2>
<div></div>
<div><img class="alignnone size-full wp-image-5086" title="Bandwidth Throttling - Charles  " src="/static/blog/2013/08/bs1.png" alt="" width="550" height="570" /></div>
<div></div>
<div>Charlesはよく使うツール。といっても、デスクトップでこの機能使うくらいなんだけど。</div>
<div>詳しい使い方はこもりさんの記事がわかりやすい。</div>
<div>
<ul>
	<li><a href="http://blog.gaspanik.com/how-to-setup-charles-web-debugging-proxy">Charles Web Debugging Proxy の使い方 | gaspanik weblog </a></li>
</ul>
<div>とりあえず、実機の端末はこのCharlesを通してインターネッツに羽ばたけば良いわけです。重要なのはCharelsが入ってるMacのIPアドレスと、ポート番号（ここではとりあえず8888にしときましょう）です。</div>
</div>
<div></div>
<div></div>
<div> <img class="alignnone size-full wp-image-5090" title="network" src="/static/blog/2013/08/network.png" alt="" width="660" height="570" /></div>
<div>ちなみに、MacでIPアドレスを確認したい場合は、<strong>システム環境設定 ＞ ネットワーク ＞ 詳細 ＞ TCP/IP</strong>でみれます。</div>
<div></div>
<div>で、このIPをAndroidの端末に設定してあげれば行けるわけですね。けど、記事にはiOSの設定しか書いてない！ということでググったらネットワークの部分長押しでプロキシ設定項目がでてくるらしい。。。</div>
<div>
<ul>
	<li><a href="http://ameblo.jp/yongmars/entry-11339671898.html">忘れないように 『プロキシ設定』｜スイーツ＠インデックス リバース </a></li>
</ul>
<div><a href="/static/blog/2013/08/ss.png"><img class="alignnone size-full wp-image-5087" title="" src="/static/blog/2013/08/ss.png" alt="" width="338" height="600" /></a></div>
</div>
どうでもいいけど、<a href="http://juggly.cn/archives/75086.html">Android 4.2で「開発者向けオプション」を表示する方法</a> とかも分かりにくいよね。。

とりあえず、できました。ありがとうございました。
