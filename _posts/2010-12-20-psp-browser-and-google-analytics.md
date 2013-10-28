---
layout: post
title: PSPインターネットブラウザとGoolge Analytics
categories:
- analytics
tags:
- PSP
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '7598'
  _aioseop_description: 先日、Google Analyticsの非同期スニペットに移行作業中、PSP専用サイトでのデータ取得ができなくなった報告を受けました。非同期スニペットに変更した途端、データが取得できなくなったので、これが問題なのは確かなようです。
---
先日、Google Analyticsの非同期スニペットに移行作業中、PSP専用サイトでのデータ取得ができなくなった報告を受けました。非同期スニペットに変更した途端、データが取得できなくなったので、これが問題なのは確かなようです。

実装したスニペットにセミコロン抜けなどのコードミスは見受けられず、非同期スニペット自体が問題なのかなと思いましたが、他のサイトでは問題なくデータが取得できているのでこれも原因ではなさそうです。

<!--more-->

やれやれ困ったなと考えあぐねてたのですが、優秀な同僚さんがこんなものを見つけて来てくれました。
<blockquote>
<div id="_mcePaste">
<ul>
	<li><a href="http://www.jp.playstation.com/psp/dl/pdf/InternetBrowser_ContentGuideline-J_500.pdf">PSP™ (PlayStation® Portable)インターネットブラウザ向けコンテンツ作成ガイドライン　Version 5.00</a> [ PDF 約492KB ]</li>
</ul>
</div>
<div id="_mcePaste"><a href="http://www.jp.playstation.com/psp/update/ud_01.html"><span style="font-size: x-small;">PlayStation.com(Japan)｜PSP®「プレイステーション・ポータブル」情報｜システムソフトウェア アップデート</span></a></div></blockquote>
PSP専用サイトなので、当然アクセスしてくるユーザーエージェントはPSP専用ブラウザです。簡単にゆうと、そのPSP専用ブラウザがDOMに対応してないんじゃないの？ってことっぽいです。

ということで、今一度、非同期スニペットがどのようなものか、見てみましょう。
<pre><span style="color: #888888;">&lt;script type="text/javascript"&gt;</span>
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
<span style="color: #888888;">&lt;/script&gt;</span></pre>
上記スニペットとPSPインターネットブラウザガイドラインの<em>8 Appendix 詳細仕様DOM</em>の部分を見比べてみると、どうやらSCRIPT要素を書き出している部分のcreateElement、insertBeforeメソッドが対応していない模様です。

なるほど、どうりでデータが取得されていなわいけですね。ga.jsを読み込めてないわけですから。
<pre><span style="color: #888888;">&lt;script type="text/javascript"&gt;</span>
var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");
document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
<span style="color: #888888;">&lt;/script&gt;</span></pre>
そこで、ga.jsの読み込みの部分だけ、旧スニペットのdocument.writeによる書き出しに修正してみたのですが、なぜか動かない。なせ動かない、よく分からない＞＜

そこで、仕方なく非同期スニペット導入以前の旧スニペット（アカウント設定の部分も旧メソッド）に変更して対応しました。

結局分からないままなので、非同期スニペットだとPSPブラウザトラッキングできないの？とGoogleさんに問い合せてみたところ、以下のような返答がきました。
<blockquote><span style="font-family: 'MS ゴシック'; line-height: normal; border-collapse: collapse;">Analytics を使用するためには javaEnabled 等のメソッドが使える必要がございます。 PSP ブラウザの仕様書によりますとこれらのメソッドが PSP ブラウザにサポートされていないため、Analytics によるトラッキングがご利用頂けません。<br style="font-family: 'MS ゴシック' !important;" /><br style="font-family: 'MS ゴシック' !important;" />なお、本件につきましては弊社米国エンジニアにリクエストとしてご連絡させていただきましたので、将来的に PSP におきましても Analytics が使用できるようになる可能性がございますが、正確な時期に関しましては現在のところご案内致しかねますので、ご了承下さい。</span></blockquote>
<span style="font-family: 'MS ゴシック';"><span style="border-collapse: collapse; line-height: normal;">javaEnableメソッドはJAVAをサポートしてるかどうか調べるもんだから、そこ対応していなくてもJAVAサポートのデータが取れないだけで問題なさげのような気もしますが、いろいろ対応していないのでしょう。てかそもそも非同期スニペットだからだめなのか、それとも旧スニペットでもだめなのかというところを再度質問すると、</span></span>
<blockquote><span style="font-family: 'MS ゴシック';"><span style="border-collapse: collapse; line-height: normal;">確認しましたところ、旧スニペットにおきましても Analytics の動作環境を PSP ブラウザが満たしておりません。<br style="font-family: 'MS ゴシック' !important;" /><br style="font-family: 'MS ゴシック' !important;" />そのため、旧スニペットで測定できていたとしても、Analytics の動作環境を PSP ブラウザが満たしていないため、正確な値が取れているという保証はできません。</span></span></blockquote>
なんと！今まで取れていた情報って不正確なの！？てか、そもそもPSPブラウザなんなの？って根本的なことが疑問になってきたので、今度はPSPブラウザに調べてみた。
<h3>NetFront</h3>
さっきのPSPインターネットブラウザガイドラインにはこのように書かれています。
<blockquote>PSPのインターネット機能は株式会社ACCESS のNetFrontを搭載しています。</blockquote>
おー！Net Frontってなに？
<blockquote>携帯電話（NTTドコモ・ソフトバンク）、PDA、ゲーム機、セットトップボックスに搭載されている。 モジュール化されていて、必要な機能を取捨選択して実装できる。Adobe社と共同開発により、Adobe Reader LE、Adobe Flash Playerも移植されている。主要なHTMLレンダリングエンジンの中では、唯一、PC版を提供していない。Net Applicationsの調査によると、2010年10月現在、世界シェアは0.05%。

<a href="http://ja.wikipedia.org/wiki/NetFront_Browser"><span style="font-size: x-small;">NetFront Browser - Wikipedia</span> </a></blockquote>
ほー！これってPS2のブラウザもそうなんだけど、PS3にも実装されてるのかなと疑問に思ったので、pS3のコンテンツ作成ガイドライン見つけた。しかしね、特に情報となるものは書いていない。。
<ul>
<blockquote>
	<li><a href="http://www.jp.playstation.com/ps3/pdf/Web_Content-Guidelines_j250.pdf">PlayStation®3 インターネットブラウザ向け Webコンテンツ ガイドライン Version 2.50</a> [ PDF 約430KB ]</li>
<a href=" http://www.jp.playstation.com/ps3/update/"><span style="font-size: x-small;">PlayStation.com(Japan)｜PlayStation®3 情報｜システムソフトウェア アップデート</span></a></blockquote>
</ul>
JavaScriptの対応もざっくりとしか書いてないので、ゲンナリですが、<a href="http://q.hatena.ne.jp/1163249228">ここに</a>書いてあるぶんは、NetFrontベースで独自カスタマイズされた感じでしょうか？
<blockquote>【携帯端末向けNetFront Browser】
NetFront Browserは、世界中で最も利用されている携帯端末向けブラウザです。柔軟な機能拡張性を活かし、各通信事業者の独自サービスの提供をサポートします。CPU速度やメモリの限られた携帯端末においても、最新のＰＣ向けコンテンツの閲覧を可能とする、先進のブラウジングエンジンを提供。画面が小さく、入力キーの限られた環境においても高速かつ快適なブラウジングを実現するさまざまな独自機能を取り揃えています。</blockquote>
公式サイトにはNetFrontも携帯端末向けと情報家電向けがあるそうです。たぶん携帯端末向けがPSPに実装されているブラウザなのかも。
<blockquote>【情報家電向けNetFront Browser】
NetFront Browserは、ＴＶ、ゲーム機、セットトップボックス、カーナビゲーションシステムなどの情報家電向けにも広く採用されています。
NetFront® Browser SDK（移植開発キット）を利用することで、ＴＶ画面向けのリモコン操作を前提としたユーザインターフェースの開発も容易に行えます。
また、機器のコントロールを可能とするDirectConnectと組み合わせることで、Webコンテンツで機器のユーザインターフェースを実現するためのプラットフォームとしても数多く採用されています。</blockquote>
で、情報家電向けがNetFrontを改造したのがPS3のブラウザなのかな。。。

まぁ、特に答えもない感じです。。そんなわけで、僕のググる力なんざこんなもんよ。

Google Analyticsのレポートで確認したところPS3のブラウザのアクセス数は非同期スニペット導入以前、以後も対して変わっていないので問題なさそうです。たぶん。

話は戻ってまとめると、PSPインターネットブラウザはGoogle Analyticsに対応していない。PSPインターネットブラウザをトラッキングしたい場合は、JavaScriptビーコン型では無理だと思うので、パケットスニファ型かアクセスログ型で解析する必要性がある。あと、PSPインターネットブラウザを携帯電話端末と同じレベルと考えれば、携帯版トGAラッキングコードを使用すれば良いのかもと思ったけど、試していない（てか、モバイル製品なんだからモバイル向けトラッキングコードを使うのは当たり前か）。なにせ、検証機とかテスト環境を用意できないのであきらめている。

そんなわけで、サポートさん的には米国のGAエンジニアに報告したと言っておりますが、世界的なシェアを見れば優先度低そうなので、気長に待ちましょう。
