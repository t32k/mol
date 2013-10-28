---
layout: post
title: お願いだから輝かないでくれ!!!
categories:
- memo
- Titanium Mobile
tags:
- Titanium
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '11180'
  _aioseop_keywords: glossy, appicon, pre
  _aioseop_description: "月灯りの下 やさしく眠る 思い出は夏の星空となる\r\nもう帰らない 帰れない\r\nあなたのそば以外で私輝かないの\r\n輝けないの
    輝かないの"
---
<img class="alignnone size-full wp-image-2673" title="ipon" src="http://t32k.me/mol/file/2011/03/ipon.png" alt="" width="470" height="250" />

アイコン的な意味でってことです。

iPhoneのアイコンってどれも個性的で素敵ですね。でもよーく見てみると、全部ってこともないけど、同じような光沢・輝き・テカリがついてますよね。あれを消したいというのが今回のエントリの主旨です。輝きも皆が同じように輝いていたらそれは没個性です。ではやっていきましょう。

<!--more-->
<h3>-precomposed.png</h3>
とりあえず、iPhoneアイコン設定とかでググってみるとこの記事が出てきました。
<ul>
	<li><a href="http://web-tan.forum.impressrd.jp/e/2010/06/15/8178">iPhone/iPadのホーム画面用アイコンapple-touch-icon.pngをサイトに設定しよう | Web担当者Forum</a></li>
</ul>
これはどうやらアプリアイコンではなく、Webサイトをホーム画面にブックマークしたときのアイコン設定ですね。Webサイトのルートにapple-touch-icon.pngを置いておけば認識してくれるのは知ってたのですが、apple-touch-icon<strong>-precomposed</strong>.pngで、このブックマークアイコンの光沢をなくせるとは、知りませんでした。機会あれば作成したいものです。
<h3>&lt;UIPrerenderedIcon&gt;</h3>
いや、ちゃうねんちゃうねん。僕はiPhone Appアイコンの輝きをなくしたいのです。僕の頭の方も輝かないで欲しいです。で、もうちょっとググッてみるとこうゆうのが出てきました。
<ul>
	<li><a href="http://blog.syuhari.jp/archives/966">[iPhone 開発メモ] アイコンの透明感を付けない方法 | Sun Limited Mt.</a></li>
</ul>
Info.plist（プロパティリスト）というのは、設定ファイルみたいですね。ここを書き換えればいいのですね。おｋ、余裕。ってことで、前回作成しましたTitanium Mobileのプロジェクトファイル内にInfo.plistがないか探してみました。ありました。
<pre>/[YOUR_PROJECT_NAME]/build/iphone/info.plist</pre>
開くエディタによってはこうゆう感じで表示されます。

<img class="fig" title="property_list_editor" src="http://t32k.me/mol/file/2011/03/property_list_editor.png" alt="UIPrerenderedIcon" width="320" height="60" />

<em><span style="color: #888888;">Property List Editor
</span></em>
<img class="fig" title="xcode" src="http://t32k.me/mol/file/2011/03/xcode.png" alt="Icon already includes gloss effects" width="320" height="60" />

<em><span style="color: #888888;">Xcode
</span></em>
ぼくはよく分からなかったので、普通のテキストエディタで
<pre>&lt;key&gt;UIPrerenderedIcon&lt;/key&gt;
&lt;true/&gt;</pre>
と追加しました。

よし、これでイケル！ってことで、Titanium Developerでビルドしてみましょう。
ほーらできた....できてない.........
<h3>&lt;prerendered-icon&gt;</h3>
ミスタイプしてるわけでもなく、Titanium Developer再起動しても、いつまでたってもアイコンの輝きは失ってくれません。そう、ダイヤモンドは永遠の輝きです。

試しに、Titanium Developerじゃなくて、Xcodeでビルドしてみるとうまくいった(・∀・)！試しに、Titanium Developerでビルドした後に、Info.plistを見てみると、UIPrerenderedIconが消えてる(・∀・;)！

ってことで、さらにググッてたら、どうやらTitanium側での設定が必要っぽいです。
<ul>
	<li><a href="http://code.google.com/p/titanium-mobile-doc-ja/wiki/tiapp_xml">tiapp_xml - titanium-mobile-doc-ja</a></li>
</ul>
いわゆる、Titanium側でのinfo.plistにあたるのがtiapp.xmlなのですね。

ここのprerendered-iconがfalseになっているからノー光沢ノーサンキューなわけなんですね、なるほどー。
<pre>&lt;prerendered-icon&gt;true&lt;/prerendered-icon&gt;</pre>
ってことでここをtrueにしてTitanium Developerでビルド！！！！！

ほーらできた....できてない.........もういややーーー！
<h3>Full Rebuild</h3>
またつまづいてしまいました。でもまた立ち上がればいいじゃない！再度ググるとこんなものがでてきました。
<blockquote><strong>なぜかエラーが起こる。</strong>
何の問題もないはずなのに、エラーが起こる場合があります。信じられないかもしれません。私も信じられません。でも本当です。しかも、エラー内容が表示されずに、スタックトレースが表示されます。どうしようもありません。試されてます。この場合は、Project/build/iphoneフォルダ以下をのファイルをすべて削除して、再度実行するとOKです。ちなみに、iphoneフォルダを消すと、デバッグできなくなりますので注意してください。
<span style="font-size: x-small;"><a href="http://d.hatena.ne.jp/shunsuk/20110304/1299229674"> Titanium Mobileの暗黒ノウハウを公開します。 - このブログは証明できない。</a></span></blockquote>
信じられませんキタ━━━(゜∀゜)━━━━ッ!!

ちなみに本当にデバッグできないのか確かめたかったのか、単に間違えちゃったのか今ではわかりませんがiphoneフォルダごと消しちゃったら、本当にRun Emulatorの部分にiPhoneの項目がでてきませんでした！

そう、私の心は常にATフィールド全開です。

てことで、まるっと削除して再度ビルドしたらいけました。やた！！！ここまで来るのに丸２日かかったので、誰かのためになればと思います。まとめると、Titanium Mobileで光沢の無いアイコンにしたければビルドするまえに、tiapp.xmlの修正すればOK！既にビルドしちゃってたら、プロジェクトの/build/iphone/以下をまるっと削除でFull Rebuildでおｋ！

それではみんなもれっつたいたん！
