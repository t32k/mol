---
layout: post
title: Titanium Mobile で Hello World!
categories:
- javascript
- Titanium Mobile
tags:
- Titanium
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '7667'
  _aioseop_description: 先月のkanajで大阪の@astronaughtsさんが、「Titanium Mobileえ〜よ。え〜わ〜。くるで！これくるで！！」と言ってたので、勉強してみるよの巻。彼もTitanium情報をまとめてくれてたりもします。
  _aioseop_keywords: titanium mobile, Appcelerator, iphone
---
先月の<a href="http://kanazawajs.tumblr.com/v1-0/">kanaj</a>で大阪の<a href="http://twitter.com/#!/astronaughts">@astronaughts</a>さんが、「Titanium Mobileえ〜よ。え〜わ〜。くるで！これくるで！！」と言ってたので、勉強してみるよの巻。彼もTitanium情報をまとめてくれてたりもします。
<ul>
	<li><a href="http://astronaughts.net/?p=204">Titanium mobile で開発を始める時に役立つ情報のまとめ | astronaughts.net</a></li>
</ul>
Titanium Mobileというのは、JavaScriptで書いたコードをうまいことして、iPhoneやAndroidでも動くようにしてくれるものです。つまり、JavaScriptさえできれば、iPhoneアプリ作れちゃうってことですよ！！（Android持ってないので、今後はiPhoneアプリ制作でがんばってきます）

Titaniumをインストール前にSDK(Software Development Kit)インスールしといてね。
<ul>
	<li><a href="https://developer.apple.com/xcode/index.php">Download Xcode + iOS SDK - Apple Developer</a> (iPhone)</li>
	<li><a href="http://developer.android.com/sdk/index.html">Android SDK | Android Developers</a> (Android)</li>
</ul>
iOS SDKのほうはインストールされていたらTitaniumが勝手に認識してくれるのですが、Androidのほうはそうもいかないみたいでちょっとめんどくさいです。でもここ見たらなんとかイケマシタ！
<ul>
	<li><a href="http://d.hatena.ne.jp/r_kurain/20110306/1299393778">Android SDK+Titaniumのインストール方法復習 - kurainの壺</a></li>
</ul>
<h3>Titanium Developer のインストール</h3>
てことで<a href="http://www.appcelerator.com/">公式サイト</a>より、<a href="http://www.appcelerator.com/products/download/">DOWNLOAD TITANIUM</a>！！

あ、そうそう、私の環境ですが、Mac OS X 10.6.7でiOS SDK 4.3でがんばってます。

で、dmgをダウンロードしたらだぼーくりっくでインストールだ！で、Titanium Developerを起動！

あ、そうそう、Titaniumって、タイタニウムって読むらしいですよ。で、タイタンの野郎が勝手にTitanium SDKなど最新バージョンにアップデートせいや！って要求してくるので最新のものにしておきましょう。
<h3>Titanium Mobile で Hello World!</h3>
<iframe src="http://player.vimeo.com/video/21389746?byline=0&amp;portrait=0&amp;color=ffffff" width="470" height="264" frameborder="0"></iframe>

で、ここから本番。初心者の基本「Hello World！」してみましょう。動画を見てくれれば分かると思うんだけど5分もかからずにできちゃう。ほんとかんたんにできちゃう！ほらできった！

とりあえず、Test&amp;Package &gt; Run Emulator &gt; iPhone からLaunch(ビルド)してみると、タブが2個あるアプリが生成されますんで、I am Window1ってとこをHello World!に置き換えて再度ビルドしてあげるだけですお。

最初のテンプレがあるからじゃん！って言われるかもしれないけど、全く見たことないobjective-cのコードからがんばるよりは、JavaScriptなら普段見慣れているので格段にとっつきやすいですよね。
<h4>New Project 記入項目</h4>
<ul>
	<li><strong>Project type:</strong> iPhone app作りたいのでMobileでおｋ</li>
	<li><strong>Name:</strong> アプリの名前（英数字にしときましょう）</li>
	<li><strong>App Id</strong>: 一意であればなんでもいいのですが、確実するためにはドメイン反対にした感じで。</li>
	<li><strong>Directory</strong>: プロジェクトを保存するところ。</li>
	<li><strong>Company /Personal URL</strong>: 自分のWebサイトとかそのまんまで</li>
	<li><strong>Titanium SDK version</strong>: デフォルトのいっちゃん新しいやつで</li>
	<li><strong>Installed Mobile Platformns</strong>: ちゃんとSDKがインスコされてば緑のチェックが表示されます。</li>
</ul>
正直、単にHello Worldして動きを確かめたいだけなら、全部の項目UNKOでも問題ないです！
<h3>プロジェクトのファイル構成</h3>
<img class="alignnone size-full wp-image-2592" title="proj" src="/static/blog/2011/03/proj.png" alt="" width="390" height="247" />

プロジェクトフォルダ直下が上記のような構成をしておりますんで、これをもとに開発していくのだ。

いっちゃん重要なのはResources以下のapp.jsです。「全てのJSファイルはapp.jsに帰結する」の言葉はもはや言うまでもありませんが、Titanium Mobile において、このapp.jsが最初に起動するファイルになってます。HTMLでゆうindex.htmlみたいな感じでしょうか。
<h3>コード</h3>
今回変えた部分はここです。createLabelしてるtextの値を書き換えたわけです。
<pre><code>var win1 = Titanium.UI.createWindow({
 title:'Tab 1',
 backgroundColor:'#fff'
});
var label1 = Titanium.UI.createLabel({
 color:'#999',
 text:'Hello World!',
 font:{fontSize:20,fontFamily:'Helvetica Neue'},
 textAlign:'center',
 width:'auto'
});
win1.add(label1);</code></pre>
これって、言ってることはWebサイトで言えば以下のコードみたいなことですよね。要素を作ってそれ挿入してるわけですよ。メソッドなどがTitaniumから始まってるだけでほんとJavaScriptです。ありがとうございますってかんじです。うん。これなら僕でもできそうだ！
<pre><code>var element = document.createElement('p');
var text = document.createTextNode('hello unko');
element.appendChild('text');
document.body.appendChild(element);</code></pre>
iOSシュミレータでの確認ですが、1回目のビルドは2,3分かかることもあるんですけど、2回目以降は普通にブラウザ立ち上げるのと変わらないほどのスピードで起動してくれますので、開発スピードもかなり早めることができて嬉しいかぎりです。
<h3>参考リソース</h3>
基本的に<a href="http://twitter.com/#!/donayama">@donayama</a>さんが作ってくれている、ti-mo-jaとPDFが最強っす。ここから始めれば問題ねっす！ちょっとできるようになってきたら、gihyoさんでやってる連載記事を見れば、Twitterとの連携とか高度なことが出来る感じです。
<ul>
	<li><a href="http://code.google.com/p/titanium-mobile-doc-ja/">titanium-mobile-doc-ja</a></li>
	<li><a href="http://code.google.com/p/titanium-mobile-doc-ja/downloads/detail?name=20100314.pdf&amp;can=2&amp;q=">Appcelerator Titanium MobileではじめるiPhoneアプリケーション開発</a></li>
	<li><a href="http://gihyo.jp/dev/serial/01/titanium">Titanium Mobileで作る！ iPhone／Androidアプリ｜gihyo.jp … 技術評論社</a></li>
</ul>
んなわけでみんなも、れっつ、たいたん！
