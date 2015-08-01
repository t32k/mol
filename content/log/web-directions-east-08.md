---
date: 2008-11-30
title: Web Directions East 08 カンファレンス
categories: report
---

[Web Directions East 08](http://east.webdirections.org/)に行ってきた。当日の写真は[Flickr: "wde08"](https://www.flickr.com/photos/tags/wde08/)で共有されている。

## 『State of the web』ブラウザの多様化でみる最良のウェブ開発
[Eric Meyer](http://meyerweb.com/eric/thoughts/)（エリック・メイヤー）

![Eric Meyer](https://farm4.staticflickr.com/3285/3019345414_6e962eb72a_b.jpg)

<a href="http://www.flickr.com/photos/t32k/3019345414/"><img src="http://farm4.static.flickr.com/3285/3019345414_90d286ff10.jpg" alt="RIMG0007 1"/></a>

+ Google Chromeは新しくない
+ Safariのwebkit搭載してるから実質的にはSafari
+ GoogleはなぜGeckoを選ばなかったのか？
+ モバイルを見越して、モバイル版も対応しているwebkitにしたのではないか？
+ IE8はAcid2をようやく合格
+ Acid3でもSafariやOperaが高い評価を出してる
+ Googleの関係者ははHTML5は2022年頃に勧告になるのではと言ってる
+ しかし、使おうと思ったら今すぐHTML5は使えるよ
+ ベクトルデータのCanvasとか
<a href="http://typeface.neocracy.org/">typeface.js</a>
Canvasを使うとFlashのSIFRみたいなんができる。
フォントの可能性が広がる！
こうゆうのもできるようになりJSエンジンの性能が重要になってきた。
Squirrelfish Extreme高速、TraceMonkeyも高速
<a href="http://code.google.com/p/ie7-js/">IE7.js</a>
IE6やIE5で対応していないセレクタなどJSでカバーしようよ
デザイナー側からの希望
<a href="http://github.com/jeresig/sizzle/tree/master">Sizzle</a>：jQueryのセレクターエンジン
<a href="http://bluff.jcoglan.com/">Bluff</a>：グラフライブラリ
データとしてグラフを残せる
<a href="http://raphaeljs.com/">Raphaël</a>：グラフライブラリ
<a href="http://280slides.com/">280 Slides</a>
ブラウザ上のkeynoteみたいなサービス。
Objective-CをJavaScript で実現、Objective-Jを使用
<a href="http://ejohn.org/blog/processingjs/">processing.js</a>：ProcessingをJavaScriptに移植
silverlight,flashのようにインストールする必要はないが
JSに依存することになる。
ゆえにブラウザのJSエンジンの役割は重要
Google ChromeはWebアプリケーションために作られた
モバイルウェブはまだまだ発展途上
質の高いユーザーエクスペリエンスを提供できていない
iPhone,Andoroidどちらが勝かという問題ではない
要はどちらも試してみることが大事。
というわけで、JSの進化によってWeb標準がサポートされている2008年のWebの現状
Slide : <a href="http://www.slideshare.net/mantangs/wde-state-of-the-web">WDE08 State of the web</a>


<h2>『Bulletproof A-Z』　あらゆるデバイスに対応できるウェブデザインの考え方</h2>
<a href="http://www.simplebits.com/">Dan Cederholm</a>（ダン・セダーホルム)
<a href="http://www.flickr.com/photos/t32k/3018515571/"><img src="http://farm4.static.flickr.com/3150/3018515571_2f5656a2e9.jpg" alt="RIMG0009 1"/></a>

BulletProof A-Z
simplebitsでも有名なダンさん
craftsmanship：職人気質的なところがある
私の育ったところバーモント州は品質の高さで有名
ダンがコーヒー好きってコトで<a href="http://icedorhot.com/">Iced or Hot°</a>つくった
A：メタ情報付きのアンカーリンク
長いテキストだろうが、いかなる時も崩れない
B：border-radius
CSS3 -webkit-border-radius,-moz-border-radius
master.cssとenrich.css分けて管理
プロトタイピングのときにでも良いのでは？
C：color trancepency
opacityではなくRGBa使ったほうがよい
PNG画像ならもっと広く対応できる
D：Do you....(すべてのブラウザで同じ見た目じゃないとだめなのか？)
答えはノー！
readbility的に問題なければ良いのでは？
E：easy clearing hack
clearfixが常套手段だけど名前がイケて無くない？
groupって名前ののほうがセマンティクじゃない？
F：framework
フレームワークを賢く使って必要なものはリセットしておこう
G：Grid Layout
グリッドシステムのほうが記憶に残る by ヨーゼフミューラブロックマン
em指定でエラスティックレイアウト
究極のflexibilityじゃないか？
エラスティックレイアウトをする際、font-size 62.5%は計算しやすい
ブラウザ幅からはみ出してしまう時もを考えてmax-widthもちゃんと指定して
H：垂直グリッド
垂直グリッドも対応可能、モジュールで考える
I：Internet Exploer 8
J：jQuery
CSSライクなJSライブラリ
デザイナーでも比較的使いやすい
K：Kitty
うちのねこ
L：Last
:last-childに対応していないブラウザには.lastで対応
MからRまでは時間がないので飛ばす
S：Shift Background
<a href="http://silverbackapp.com/">Silverback</a>のサイトは背景画像がクールだ
T：text blennding RGBa
<a href="http://www.wilsonminer.com/">Wilson Miner</a>のサイトはaのhover時にrgbaでブレンドしてる
U：yoUR starts?
いつから使う？
When can we__?
ログ解析しなさい。
Slide : <a href="http://www.slideshare.net/mantangs/bulletproof-a-to-z">WDE08 BULLETPROOF A to Z</a>


<h2>Bulletproof 使い勝手と見やすさを両立するAjaxを使ったサイト設計</h2>
<a href="http://adactio.com/">Jeremy Keith</a>（ジェレミー・キース）
<a href="http://www.flickr.com/photos/t32k/3019353226/"><img src="http://farm4.static.flickr.com/3283/3019353226_1545e97964.jpg" alt="RIMG0020 1"/></a>

Designing Ajax
Ajaxの定義
バックグラウンドでサーバーと通信しページ全体をリフレッシュすることがない
体感的な問題、通信速度が速くなるわけではない。
ページを部分的に更新するならframe iframe flashがあるがこれはAjaxでしょうか？
XML HTTP Request
はじめはMicrosoftでIE5で初めて実装
そのあとMozilla, Safari, Operaがサポート
<ul>
	<li>CONTENT</li>
	<li>STRUCTURE(HTML)</li>
	<li>PREZENTATION(CSS)</li>
	<li>BEHAIBIOR(JavaScript)</li>
</ul>
Hijax = Ajax + Progressive Enhancement
JavaScriptが使えなくても普通に使える
モジュール化したデザイン
<ul>
	<li>Plan for Ajax from the start</li>
	<li>Implement Hijax at the end</li>
</ul>
パターン認識
<ul>
	<li>sign up</li>
	<li>add to cart</li>
	<li>rate this</li>
	<li>add a comennt</li>
</ul>ajaxで対応すべき
<ul>
	<li>search result?</li>
	<li>pagination?</li>
</ul>ajaxで対応すべきではない
feedback
What is happening?　何が起きたのか？
What just happend?　何が起きているのか？
<ul>
	<li>status indicators</li>
	<li>yello fade</li>
<li>drag'n'drop</li>
</ul>
結局、どこまでやるとやりすぎなのか？
ログ解析しなさい。
Slide : <a href="http://www.slideshare.net/mantangs/wde08-designing-for-interaction-with-ajax">WDE08 Designing for interaction with Ajax</a>
<a href="http://www.flickr.com/photos/t32k/3019354724/"><img src="http://farm4.static.flickr.com/3005/3019354724_001980f5b0.jpg" alt="RIMG0022 1" width="375" height="500"/></a>
お昼休み(<a href="http://www.nicovideo.jp/watch/sm5218852">niconico動画</a>)
John Allsoppのグローバルナビを画像を使わず、CSS3だけで実装してみせた
ファイル削減 30kBから1.7KB、文字サイズ拡大に対応


<h2>『Guerilla Userbility Testing』高効率・低コストで行うユーザビリティテストの仕組み</h2>
<a href="http://www.andybudd.com/">Andy Budd</a>（アンディ・バド）
<a href="http://www.flickr.com/photos/t32k/3018524443/"><img src="http://farm4.static.flickr.com/3195/3018524443_3e7221269f.jpg" alt="RIMG0025 1"/></a>

チケット購入システムUIがひどい
今のコンピュータはすごいよ
月へ行った頃の全部のパソコンを集めても、今のラップトップにかなわない
ユーザーはマニュアルを読まない
今までの経験に基づいた判断をする
video,DVD,Blue-rayのプレイヤーは基本的な操作は同じ
マルチタスクでユーザーはウェブを見ている
必ずしもデベロッパーとユーザの考えは一緒ではない
Test on Real Users
microsofの<a href="http://www.xbox.com/ja-JP/games/h/halo3/">Halo3</a>はHalo2の失敗を受け、600人、3000時間のユーザーテストを行った
結果、3億ドルの売り上げ
User test for web
時間とお金がかかる
従来どおりのミラーとビデオで観察
informal test
どこでもできる、簡単、すぐにフィードバック
客観性が必要
統計的というよりも何が問題なのか考えることが大切
<a href="http://silverbackapp.com/">Silverback</a>の簡単な説明
パソコンの前に座って、あとはテストするだけ
全部記録できる
Slide : <a href="http://www.slideshare.net/andybudd/guerilla-usability-testing">Guerilla Usability Testing
</a>

<h2>Web標準的ブラウザのグラフィックのススメ</h2>
Doug Schepers(ダグ・シェパーズ)
SVG and Canvas : Standards based open graphics
■SVG
<ul>
	<li>Google Mapsでも使われているよ</li>
	<li>XMLベースだよ</li>
	<li>wikipediaの画像</li>
	<li>パーツごとに独立している</li>
	<li><a href="http://research.sun.com/projects/lively/">Lively Kernel</a></li>
	<li><a href="http://dojotoolkit.org/">Dojo</a></li>
	<li><a href="http://svg-whiz.com/svg/StarMaker.svg">Star Maker</a></li>
</ul>
■Canvas
<ul>
	<li>WHATWG Appleとかが作った</li>
	<li>ベクトルを使ってラスターを作成</li>
	<li>全体で1つの画像</li>
	<li><a href="http://ejohn.org/blog/processingjs/">proceccing.js</a></li>
	<li><a href="http://www.azarask.in/projects/algorithm-ink/">Algorithm Ink</a></li>
</ul>JavaScriptが使えれば、いろんなことができる。
JIS化されれば日本でももっと広まっていくと思う


<h2>Visualization A Web Of Data─Web上における情報データの可視化</h2>
<a href="http://mike.teczno.com/">Mike Migurski</a>(マイク・ミジャースキー)
<a href="http://www.flickr.com/photos/t32k/3019356328/"><img src="http://farm4.static.flickr.com/3221/3019356328_1c93185280.jpg" alt="RIMG0026 1"/></a>

Visualization A Web Of Data
地図デザイン、情報のビジュアライゼーションの<a href="http://www.stamen.com/">stamen design</a>の人
データの可視化の三原則
<ul>
	<li>LIVE：常に最新であること</li>
	<li>VAST：広範囲でデータをカバー</li>
	<li>DEEP：どの程度まで情報を掘り下げれるか</li>
</ul>制作事例
<a href="http://www.fivethirtyeight.com/"><img src="http://ijok.ijok.googlepages.com/081130_01.png" alt=""/>
FiveThirtyEight.com</a>
<a href="http://www.nytimes.com/ref/us/20061228_3000FACES_TAB2.html"><img src="http://ijok.ijok.googlepages.com/081130_02.png" alt=""/>
Casualties of War - New York Times</a>
<a href="http://www.moveon.org/"><img src="http://ijok.ijok.googlepages.com/081130_03.png" alt=""/>
MoveOn.org</a>
<a href="http://labs.digg.com/"><img src="http://ijok.ijok.googlepages.com/081130_04.png" alt=""/>
digg labs</a>
<a href="http://hindsight.trulia.com/"><img src="http://ijok.ijok.googlepages.com/081130_05.png" alt=""/>
Trulia Hindsight</a>
<a href="http://snapshot.trulia.com/"><img src="http://ijok.ijok.googlepages.com/081130_06.png" alt=""/>
Trulia Snapshot</a>
<a href="http://www.sfmoma.org/projects/artscope/"><img src="http://ijok.ijok.googlepages.com/081130_07.png" alt=""/>
SFMOMA</a>
<a href="http://modestmaps.com/"><img src="http://ijok.ijok.googlepages.com/081130_08.png" alt=""/>
Modest Maps</a>
<a href="http://oakland.crimespotting.org/"><img src="http://ijok.ijok.googlepages.com/081130_09.png" alt=""/>
Oakland Crimespotting</a>
<a href="http://www.plasticbag.org/files/native/"><img src="http://ijok.ijok.googlepages.com/081130_10.png" alt=""/>
Native to a Web of Data</a>
Slide : <a href="http://www.slideshare.net/mantangs/wde08-visualizing-web-of-data-1488939">WDE08 Visualizing Web of Data
</a>
