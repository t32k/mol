---
layout: post
title: Version Number (iTunes Connect) と Bundle version (CFBundleVersion)
categories:
- Titanium Mobile
tags:
- iphone
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '10776'
  _aioseop_description: 言葉の定義はしっかりしましょう。
  _wp_old_slug: vesion-bundle-cfbundle-build
---
ちょっとハマったので、メモ。

こないだNyarsのバージョンを1.2から1.2.1にアップデートしました。アップデート理由は文言修正など細かな修正だったので1.0, 1.1, 1.2 ときたバージョンアップですが、今回はマイナーアップデートてことで、1.2.1にし申請を出してみました。

んが、しかし、拒否られたくさい。（こんなん言われた＞＜）
<blockquote>The binary you uploaded was invalid. The key CFBundleVersion in the Info.plist file must contain a higher version than that of the previously uploaded version.</blockquote>
前出したバージョンより、CFBundleVersionが低いからダメってことよね？1.2から1.2.1ってどーみても上がってんじゃん！てめぇ数字数えられねーのかよ!?てことで調べてみた。

<!--more-->
<h2>Version (tiapp.xml)</h2>
バージョンに関して記入するところと言えば、

<img class="fig" title="Titanium Developer 1.2.2" src="/static/blog/2011/06/tidev.png" alt="Titanium Developer 1.2.2" width="470" height="340" />

Titanium Developer 1.2.2では↑ここ。

<img class="fig" title="Titanium Studio" src="/static/blog/2011/06/tistudio.png" alt="Titanium Studio" width="470" height="340" />

Titanium Studioでは↑ここですね。

この部分がtiapp.xmlに反映されるわけですね。

[html]
&lt;version&gt;1.0&lt;/version&gt;
[/html]
<h2>Bundle version (CFBundleVersion)</h2>
で、このtiapp.xmlの内容が、/<em>APPLICATION_PROJECT</em>/build/iphone/Info.plist のBundle version (CFBundleVersion)に反映されます。

<img class="fig" title="Bundle version (CFBundleVersion)" src="/static/blog/2011/06/info.png" alt="Bundle version (CFBundleVersion)" width="470" height="340" />

上記はXcodeで確認した場合になります。通常のテキストエディタでInfo.plistを開いてみると

[html]
&lt;key&gt;CFBundleVersion&lt;/key&gt;
&lt;string&gt;1.0&lt;/string&gt;
[/html]

こんな感じになってるかと思います。試しにテストアプリを作ってバージョンはどの段階においても1.0です。問題有りません。
<h2>Build Number</h2>
はい、でこのアプリを実機にインストールもしくはパッケージ化し、Info.plistのBundle Versionを確認してみましょう。なんということでしょう。こんなんになってた！
<pre>1.0.1308740503</pre>
1.0以降に変な数字でてるやないですか！たぶんこれBuild Numberってゆうやつだと思われます（なんかググってみてそんな感じのようなことが書かれてた）。これなんか勝手に生成されるようです。

ってことで、今回のNyarsマイナーアップデート申請がなぜ却下されたのか考えてみますと、前回のバージョンが1.2で今回出したバージョンが1.2.1てことで、それらにBuild Numberをくっつけたのを比較してみますと
<pre>1.2.BUILD_NUMBER
1.2.1.BUILD_NUMBER</pre>
ってことなので、3番目の値で比較（Build Numberと1）され却下されたのではないかと結論づけました。
<h2>Version Number (iTunes Connect)</h2>
ということで今回は、1.2.0って最初から出しとけば問題なかったわけですな。けどもVersion1.2.0でたぜ！ってゆうのもアレだと思った方、心配ご無用です。CFBundleVersionはいわゆる内部バージョン番号みたいなものなので、iTunes Connect（お店に並ぶときのバージョン）に出すのは別でよいのでそこは1.2って提出しときましょう。

<a href="/static/blog/2011/06/itunes.png"><img class="fig" title="iTunes Connect" src="/static/blog/2011/06/itunes.png" alt="iTunes Connect" width="470" /></a>

<a href="http://ja.wikipedia.org/wiki/Microsoft_Windows_7">Windows7の内部的なバージョン番号が 6.1</a>のようなものです。てことで今回僕は、1.2.1では通らなかったのでCFBundleVersionは1.3.0で提出してiTunes Conectには1.2.1を提出して無事アップデートできました。

めでたしめでたし。

めんどくさかったらこの人みたいに最初から整数値でアップデートしていくのも手かと。
<ul>
	<li><a href="http://vivacocoa.jp/cocoaApp/cocoaApp10.cgi">viva Cocoa / Cocoa GUI App no.10 </a></li>
</ul>
<h2>参考</h2>
<ul>
	<li><a href="http://basuke.blogspot.com/2010/02/appstore.html">Basuke's Blog: AppStoreのバージョン番号ではまる</a></li>
	<li><a href="http://www.dribin.org/dave/blog/archives/2006/08/02/versioning_os_x_apps/">Versioning Mac OS X Applications Best Practicies - Dave Dribin's Blog </a></li>
</ul>
&nbsp;
