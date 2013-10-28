---
layout: post
title: Chrome for Androidでリモートデバッグ
categories:
- development
- mobile
tags: []
status: publish
type: post
published: true
meta:
  pvc_views: '5580'
  _edit_last: '1'
---
さて、<a href="http://html.adobe.com/jp/edge/">Adobe Edgeツール&amp;サービス</a>が発表されましたね。リモートデバッグではAdobe Shadowが<a href="http://html.adobe.com/jp/edge/inspect/">Edge Inspect</a>に名をかえて正式にリリースされたようです。まぁ特に変わったことはないんですけど、ダウンロードするのに、Adobeのアカウントが必要になったとかでちょいめんどくさくなりました。Shadowの使い方は<a href="http://havelog.ayumusato.com/develop/others/e476-try_adobe_shadow.html">こことか参照</a>するとよい。

ここではあえて、時代の流れを読まずに<a href="https://play.google.com/store/apps/details?id=com.android.chrome&amp;hl=ja">Chrome for Android</a>でリモートデバッグに挑戦したいと思います。ChromeはAndroid4.0以降対応なんですね、必死こいて2.3の端末機にインスコしようとググってました。あと、4.1からデフォルトのブラウザーになるとかで今後のメインストリーム確実な感じです。
<ul>
	<li><strong><a href="https://developers.google.com/chrome/mobile/docs/debugging">Remote Debugging - Google Chrome Mobile — Google Developers</a></strong></li>
</ul>
<div><!--more--></div>
<h2>各種インストール</h2>
まぁ、インストールの仕方などは上記リンクに、ほぼ書いてあるんですけどメモ代わりに残しておきます。あ、自分Macっす！
<ul>
	<li><a href="http://developer.android.com/sdk/">Android SDK</a></li>
	<li><a href="https://www.google.com/intl/ja/chrome/browser/">Chrome </a></li>
</ul>
SDKとChromeをインストール。SDKはどっか任意の場所に保存して、/Applications/android-sdk/tools/android（僕の場合はアプリケーションディレクトリにandroid-sdkという名前で置いた）を実行すると、Android SDK Managerが起動するので、Android SDK Platform-toolsをインストール。

<img class="aligncenter wp-image-4297" title="Android SDK Platform-tools" src="http://t32k.me/mol/file/2012/09/Android-SDK-Platform-tools.png" alt="" width="520" />

/Applications/android-sdk/platform-toolsのAndroid Debug Bridge (adb)コマンドが必要になってくるので、PATHを通しておく。.bash_profileとかに下記のように記述する。
<pre><code>#.bash_profile
PATH=$PATH:/Applications/android-sdk/platform-tools</code></pre>
んで、読み込ませておく。
<pre><code>$ source .bash_profile</code></pre>
PATHが通ったので、次回からは下記コマンドだけOK。
<pre><code>$ adb forward tcp:9222 localabstract:chrome_devtools_remote</code></pre>
<h2>各種設定</h2>
んで、Androidの方の設定で、【本体設定】&gt;【開発者向けオプション】&gt;【USBデバッグ】にチェキラーぁぁぁっｌ！！

<img class="aligncenter wp-image-4300" title="Setting-for-Android" src="http://t32k.me/mol/file/2012/09/Setting-for-Android.png" alt="" width="380" />

んで、Chrome for Androidの方の設定で、【設定】&gt;【デベロッパーツール】&gt;【USBウェブデバッグを有効化】にチェキラーぁぁぁっｌ！！

<img class="aligncenter wp-image-4301" title="Setting-for-Chrome" src="http://t32k.me/mol/file/2012/09/Setting-for-Chrome.png" alt="" width="380" />

これらも一回設定しておけばOK.
<h2>使ってみる</h2>
前述のadb forwardなんちゃらってコマンド打ち込んで。localhost:9222をPC Chromeで開いてみましょう。
<pre><code>http://localhost:9222/</code></pre>
このとき、USBでAndroid実機をつなげて、Chrome for Androidでデバッグしたいページを開いておきましょう。そうするとAndroidで開いてるページがPCから確認できます。

<img class="aligncenter wp-image-4304" title="Inspectable Pages" src="http://t32k.me/mol/file/2012/09/Inspectable-Pages.png" alt="" width="520" />

デバッグしたいページをクリックするとデベロッパーツールが立ち上がります。
<p style="text-align: center;"><img class="aligncenter" title="DevTools" src="http://t32k.me/mol/file/2012/09/DevTools.png" alt="" width="520" height="326" /></p>
見てもらえるとわかるように、PCのデベロッパーツールとほぼ同等の機能が使えます。比較検討のためにEdge Inspect（weinre）で開いたデベロッパーツールのキャプチャを置いときますね ↓

<img class="aligncenter wp-image-4306" title="weinre" src="http://t32k.me/mol/file/2012/09/weinre.png" alt="" width="520" />

weinreでもNetworkとかTimeline使えるけど、Chrome for Androidでのリモートデバッグのほうがより細かいとこまで見れたり全体的に高機能かつサクサク動きますです、はい。個人的に一番バビったのが拡張機能のPageSpeedが普通に動いてて、なおかつ評価設定がちゃんと<strong>【モバイル】</strong>として評価されていたの感動しました。

これまでも、デベロッパーツールの設定でUAをスマホにしたりしてスマホサイトをPageSpeedで評価できたのですが、これはあくまでデスクトップ基準での評価でして、例えばオンラインのPageSpeedで<a href="http://t32k.me/">t32k.me</a>を評価してみると、<a href="https://developers.google.com/speed/pagespeed/insights#url=http_3A_2F_2Ft32k.me_2F&amp;mobile=false">デスクトップ版92点</a>なのに対して、<a href="https://developers.google.com/speed/pagespeed/insights#url=http_3A_2F_2Ft32k.me_2F&amp;mobile=true">モバイル版は88点</a>と厳しめの評価です。改善策のサジェスチョンも微妙に違ったり（違いに関しては<a href="https://developers.google.com/speed/docs/insights/faq#howonlinemobilediff">ここ参照</a>）しますので、Chrome for Androidのリモートデバッグ調べてたら思わぬ収穫を得たなという感じですね。

そんな感じで、こんな機能もあるぜってのあったら教えて下さい。
