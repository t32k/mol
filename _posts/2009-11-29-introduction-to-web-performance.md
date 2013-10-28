---
layout: post
title: ウェブサイトパフォーマンス入門 - ニコール・サリバン
categories:
- performance
- report
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/11/introduction-to-website-performance.html
  _edit_last: '1'
  pvc_views: '7593'
  _comment_timeout: '365,60'
---
<img src="http://lh5.ggpht.com/_1drnogi3vdg/SxEtcjQFk1I/AAAAAAAAAt4/aoCs08yfz4E/head.jpg" alt="'''" />

<a href="http://east.webdirections.org/wde/2009/workshop/#nicole-sullivan">Web Directions East 2009 ワークショップ</a> 11月12日
ウェブサイトパフォーマンス入門 ニコール・サリバン

通訳は<a href="http://www.yasuhisa.com/could/">could</a>の<a href="http://twitter.com/yhassy">長谷川さん</a>だよ。
<h3>Nicole Sullivan （ニコール・サリバン）</h3>
3000以上にも昇る大規模サイトの最適化に携わって来た Nicole Sullivan は、現在 Yahoo! のパフォーマンスエンジニアと最適化のエバンジェリストとして国内外のセミナーで講演。Webサイトに関する研究だけでなく、プロジェクト管理もこなすマルチタスクなリーダーシップを発揮。フロントエンドエンジニアとしての高いスキルを持つ。

<span style="font-weight: bold;">Contacts</span>
<ul>
	<li> <a href="http://www.stubbornella.org/content/">Stubbornella - Blog</a></li>
	<li><a href="http://twitter.com/stubbornella">Nicole Sullivan (stubbornella) on Twitter</a></li>
	<li><a href="http://www.slideshare.net/stubbornella">Nicole Sullivan | SlideShare</a></li>
</ul>
<h3>なぜパフォーマンスについて話すのか？</h3>
<h4>1. 速い方が良い！</h4>
速くて困ることは特にない
<h4>2. サイトは年々巨大化している</h4>
現在のサイトはWebページというよりもアプリケーション化していて複雑になってきている2003年頃に比べ、ページサイズは3倍になっている
<span style="font-size: 85%;"><a href="http://www.websiteoptimization.com/speed/tweak/average-web-page/">Average Web Page Size Triples Since 2003 - web page statistics and survey trends for page size and web objects</a></span>

ユーザーにとってはWebアプリケーションもDesktopアプリケーションも同じ。
どちらも同じ性能を求められる
<h4>3. 時は金なり</h4>
<ul>
	<li><span style="font-weight: bold;">Amazon</span> : +100ms 売上が1%落ちる
<span style="font-weight: bold;"> </span></li>
	<li><span style="font-weight: bold;">Yahoo! </span>: +400ms 完全にページをローディング（full-page traffic）するユーザーが5-9%減る
<span style="font-weight: bold;"> </span></li>
	<li><span style="font-weight: bold;">Google</span> : +500ms 検索数が20%落ちる</li>
</ul>
<img src="http://lh5.ggpht.com/_1drnogi3vdg/SxEtWcsKK8I/AAAAAAAAAtg/GaFlZ8tBOgE/1.png" alt="shopzilla performance summary" />

<span style="font-weight: bold;">Shopzilla</span> : -3.5sec CVは7-12%, PVは25%アップした
<span style="font-size: 85%;"><a href="http://en.oreilly.com/velocity2009/public/schedule/detail/7709">Shopzilla's Site Redo - You Get What You Measure: Velocity 2009</a></span>

<span style="font-size: 85%;">
</span>

<img src="http://lh6.ggpht.com/_1drnogi3vdg/SxEtWopKSJI/AAAAAAAAAtk/u1i8Iinfxt8/2.png" alt="average page views per visit" />

<span style="font-weight: bold;">AOL Money &amp; Finance</span>（テスト数は10万人規模）

パフォーマンスが良いと思うユーザーほどページを多く見る(つまり広告収入への影響が大きい)
<span style="font-size: 85%;">(最も遅く感じているユーザーでPVが多いのはなぜ？　Nicole見解：ダイアルアップ接続ユーザーでもともと遅いのに慣れているのかも)</span>
<span style="font-size: 85%;"><a href="http://en.oreilly.com/velocity2009/public/schedule/detail/7579">The Secret Weapons of the AOL Optimization Team Presentation</a></span>

<span style="font-weight: bold;">Bing and Google Test</span>

<img src="http://lh6.ggpht.com/_1drnogi3vdg/SxEtWoKer2I/AAAAAAAAAto/16mFXkk_s38/3.png" alt="" />

50ms, 200ms, 500ms, 1000ms で遅くする実験
左からユーザー当たりのクエリ数、クエリを変えて検索した数、ユーザー当たりの収益、ページをクリックしたかどうか、満足度、クリックするまでの時間
50msでは統計的な違いは出なかった
遅延時間が長いほど満足などの指標は減少する
遅くなれば遅くなるほど思考が止まる（自分が何をしたかったのか、いちいち思い起こす必要がある）

<img src="http://lh5.ggpht.com/_1drnogi3vdg/SxEtWs2dxCI/AAAAAAAAAts/w2m3Rv71YbU/4.png" alt="" />

レンダリングの見せ方による影響について
ヘッダーだけでもいいから何か見せておくことでユーザーに安心感を与える
（検索を多くするユーザーほど効果的）

<img src="http://lh4.ggpht.com/_1drnogi3vdg/SxEyI3CrcAI/AAAAAAAAAuA/OffhhGN_Nes/5.png" alt="" />

パフォーマンスの悪さが続けば、UX低下に深刻なダメージを与える。
（7週間目に元に戻すが4週間立っても元のレベルに回復していない）
<span style="font-size: 85%;"><a href="http://radar.oreilly.com/2009/06/bing-and-google-agree-slow-pag.html">Bing and Google Agree: Slow Pages Lose Users - O'Reilly Radar</a></span>
<div style="text-align: left;"><span style="font-weight: bold;">パフォーマンスについてユーザケアする必要がある</span></div>
<div style="text-align: left;"><span style="font-weight: bold;">
</span></div>
<h3>開発理念　Web Dev Philosophy</h3>
フロントエンドエンジニアとデザイナーのコミュニケーションをいかに円滑にするか重要
（エンジニア、デザイナー双方が歩み寄って理解する必要がある）
<h3>9つのベストプラクティス</h3>
<h4>1. コンポーネント化する</h4>
PSDファイルのコンポーネント化、ライブラリ化する(デザイナーが辞めても他のデザイナー対応できる)

コンポーネントはレゴに似てる
コンポーネントの利点：再利用でき、ブラウザキャッシュを利用できる
ページ全体からデザインするのではなく、コンポーネントからデザインしてそれを組み立てるのが良いのではないか
（この考え方は海外でも新しい）

Facebookコンサルの話：
Facebookは既存サイトで、最初からコンポーネントを意識して開発したわけではない
要素をカタログ化することから始めた

細かいデザインの違いによるパフォーマンス低下は極力避ける
レゴ化して見比べる
もし、同じページに2つの似たようなモジュールがあるのならば、ひとつにまとめる
<h4>2. サイト全体で一貫性を保つ</h4>
<span style="font-weight: bold;">Consistency（一貫性）</span>
ルールが多ければ多いほどデザインは崩れていく
長期スパンでパフォーマンスはゆるやかに落ちていく（危険性を感じないので厄介）
<h4>3. 透過デザインモジュールを使う</h4>
<img src="http://lh6.ggpht.com/_1drnogi3vdg/SxEtWwyxh7I/AAAAAAAAAtw/IXDBkJqmwtE/6.png" alt="" />

利点：拡張性に対応できる、コンポーネントを組み合わせることができる
弱点：複数の背景だと使えない、それ専用のモジュールを別途作らなければならない
<h4>4. 画像とCSSスプライトの最適化</h4>
Yahoo!の例：<a href="http://a.l.yimg.com/a/i/us/sch/gr4/srp_metro_20090910.png">http://a.l.yimg.com/a/i/us/sch/gr4/srp_metro_20090910.png</a>
ページ内の全ての画像をスプライト化
デザインパターンが１つだけだから可能（検索画面だけ）

スプライトするためには以下の3つから2つしかとれない

<img src="http://lh6.ggpht.com/_1drnogi3vdg/SxEtckIao6I/AAAAAAAAAt0/cQcfpjtcXJ0/7.png" alt="" />

<span style="font-weight: bold;">ページ数</span>、<span style="font-weight: bold;">メンテナンス性</span>、<span style="font-weight: bold;">最適化</span>
（ex：より多くのページ数を最適化したければメンテナンス性はあきらめるしかない）

拡張性を考えてスプライトする
ボタンは背景画像にして中身をテキストで変更
（日本語は汚くなるから考えもの）

<span style="font-weight: bold;">パフォーマンスで重要な3つのこと</span>
<ul>
	<li>HTTP requests</li>
	<li>Size of image</li>
	<li>Size of the CSS</li>
</ul>
角丸を表現するためにはHTTPリクエストが4つ必要
リクエストが2倍になれば、CSSコードも2倍に

<strong>9 画像の最適化</strong>
<ol>
	<li><span style="font-size: 85%;">似たような色でまとめる（スプライトの話）</span></li>
	<li><span style="font-size: 85%;">スキマを詰める（モバイル環境を見越すと、ちょっとでもダメ）</span></li>
	<li><span style="font-size: 85%;">CSSスプライトの画像は縦より横に並べるの方がほんのちょっとだけいい(横に読み込んでいくらしい)</span></li>
	<li><span style="font-size: 85%;">等倍で見たときの色を減色</span></li>
	<li><span style="font-size: 85%;">個々の画像を最適化してからスプライトする</span></li>
	<li><span style="font-size: 85%;">アンチエイリアスは避ける（平行四辺形はきつい）</span></li>
	<li><span style="font-size: 85%;">斜めのグラデーション画像は避ける（パフォーマンス的というよりモジュールの拡張性がない）</span></li>
	<li><span style="font-size: 85%;">アルファフィルターは避ける</span></li>
	<li><span style="font-size: 85%;">グラデーションの色は2-3px毎に変更していく</span></li>
</ol>
ロゴ画像のサイズ縮小だけは慎重に（無意識下で刷り込まれているので）
マクドナルドのロゴは大統領よりも有名

フィルタはやめてよ！
ブラウザがフリーズする、メモリを大量消費する
どうしても使いたければアンダースコアハックでIE6分岐

Alpha Image Loaderやめただけで100ms速くなったよ  by Yahoo! Search

Progressively enhanced PNG8
より良いPNG画像を作るにはPhotoshopよりもFireworksが良い

<span style="font-weight: bold;">画像圧縮の流れ</span>
Step1: デザイナーが『Web用に保存』などで減色する
Step2: 画像のメタ情報を取り除く（画像のクオリティはそのまま）
<ul>
	<li><a href="http://developer.yahoo.com/yslow/smushit/">Smush.it | Yahoo! Developer NetWork</a></li>
	<li><a href="http://www.gracepointafterfive.com/punypng">punypng - PNG Compression and Image Optimization</a></li>
</ul>
<h4>5. ブラウザに搭載されないフォントの使用は避ける</h4>
sIFR（Scalable Inman Flash Replacement）やJSで無理やり表現すればその分HTTPリクエストが増える
<h4>6. 縦で考える</h4>
コンテンツは増えていくものなので仕方がない
横に合わせるのは難しい（jQueryなどJSで制御する必要があるため）
<h4>7. ギラギラなデザインは慎重に</h4>
画像などを使って目立せることでコスト（パフォーマンス低下）がかかっていることを理解する
<h4>8. フレキシブルに</h4>
拡張性を考えてデザインする
コンテンツは横にも縦にも伸びる
横はグリッドでコントロール（縦は仕方ない）
<h4>９。グリッドは重要です</h4>
上記に同じ
<h3>アクティビティ</h3>
各自が選んだサイトがどのように改善できるか考えるワークショップ
<h4>パフォーマンスツールの紹介</h4>
<ul>
	<li><a href="http://www.alphaworks.ibm.com/tech/pagedetailer">IBM Page Detailer : Overview</a></li>
	<li><a href="http://www.webpagetest.org/">Pagetest - where web sites go to get FAST!</a></li>
	<li><a href="http://www.gomez.co.jp/business/gpn/index.html">Webサイトパフォーマンス測定：ゴメス・コンサルティング株式会社</a></li>
	<li><a href="https://addons.mozilla.org/ja/firefox/addon/1843">Firebug :: Add-ons for Firefox</a></li>
</ul>
今回はFirebugを使う

Firebugの弱点
キャッシュしたのは計測しない（キャッシュクリアして使う）
ブラウザのイベントモデルが表示される（実際のネットワークの流れではない）

<span style="font-weight: bold;">最初からツールを使うのではなく、まずぺージ全体を見て考える</span>

Flashの良い点：ユーザーの注意を引かせる
Flashの悪い点：ロードには時間がかかる
ユーザーの視点から考える

ページ下部のリクエストは遅延ロードで

<span style="font-weight: bold;">パフォーマンス改善に当たっての考え方</span>
<ul>
	<li>どれくらい改善されるのか？</li>
	<li>コストはどれくらいなのか？</li>
</ul>
<h3>ワークショップを通して</h3>
パフォーマンスについての小手先の技術を覚えたというよりも、パフォーマンスに対しての考え方が身につけられた一日ではないかと思う。Nicoleはエンジニア畑の人だけれども、デザインについて物を言うエンジニアだ。そのグラフィックは本当に必要なのか？そのデザインはほかのモジュールと似ているけれども１つにまとめられないのかなど問い正してくる。

実際、アクティビティの時間では自分が制作したサイトを元にどのように改善できるのか指摘してもらった。Nicoleから見ればJSファイル容量の割にはJSの効果が見えないとのこと。（ページ内リンクにスムーススクロールとか使ってた）

Nicoleが考えるに、大半のユーザーはその機能を使わないだろう（使えなくても問題ない）し、目に見えない面でコストをかける必要性があるのかと聞かれた。確かに、そのサイトの大半のページがそれほど長くないのでマウススクロールで事足りるし、ページ内リンクを押す必要性もあまり感じられない。もし、気になるのならアクセス解析ツールなど使って実際に使われているのか調査してみれば良いと言われたので調査中。（たぶん外すと思う）

結局は重要なのは自分が行ったデザインの費用対効果がどうなのかという問題だ。Webページは気軽に修正・追加されがちだけど、その１枚のバナー画像を追加することでHTTPリクエストは増えるのだから確実にパフォーマンスコストがかかっていることを理解する必要性がある。そういったコストを超えるメリットが得られるのなら追加すれば良いが、何の考えもなしにあれやこれやとページの要素を追加していくことは非常に危険だと思う。

開発方法においても、最初から細かいチューニングをするよりも、まずページ全体を見て不必要なものがないか確認する方が効果的だということも覚えておかなければならない。フロントエンドのパフォーマンスについては昨年あたりから注目され始めてきてまだ成熟していない分野だと思うので、あまり瑣末なことにリソースを割かれるのも賢明ではない。
<div id="__ss_658403" style="width: 425px; text-align: left;"><a style="margin: 12px 0pt 3px; font-family: Helvetica,Arial,Sans-serif; font-style: normal; font-variant: normal; font-weight: normal; font-size: 14px; line-height: normal; font-size-adjust: none; font-stretch: normal; display: block; text-decoration: underline;" title="Design Fast Websites" href="http://www.slideshare.net/stubbornella/designing-fast-websites-presentation">Design Fast Websites</a><object style="margin: 0px;" classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="425" height="355" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="src" value="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=designingfastwebsites-1224025689783608-8&amp;stripped_title=designing-fast-websites-presentation" /><param name="allowfullscreen" value="true" /><embed style="margin: 0px;" type="application/x-shockwave-flash" width="425" height="355" src="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=designingfastwebsites-1224025689783608-8&amp;stripped_title=designing-fast-websites-presentation" allowscriptaccess="always" allowfullscreen="true"></embed></object>

</div>
スライドはほぼこれと一緒で、収益に関するデータが新たに追加されてた感じだった。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51apDotzVxL._SL160_.jpg" border="0" alt="続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス" width="125" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462" target="_blank">続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
Steve Souders 武舎 広幸 </span>

<span>オライリージャパン  2010-04-10
売り上げランキング : 24938
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-3-0.gif" alt="" /></span>

<span><a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
NicoleはChapter10のOptimizing Imagesを<a href="http://www.phpied.com/">Stoyan Stefanov</a>と担当しています。

<img src="http://lh4.ggpht.com/_1drnogi3vdg/SxEtcgToPTI/AAAAAAAAAt8/lycFxE15vtM/room.jpg" alt="" />

こんな感じのところでワークワークしました。当日は<a href="http://search.twitter.com/search?q=%23wde09">#wde09</a>のハッシュタグで<a href="http://twitter.com/boblet">@boblet</a>と<a href="http://twitter.com/Zazie">@Zazie</a>と<a href="http://twitter.com/t32k">@t32k</a>がNicoleのワークショップを実況してました。にしても最後まで<a href="http://twitter.com/Zazie">@Zazie</a>さんがどなたか分かりませんでした。たぶん横にいた方だと思うのですがもっと喋りかけていけば良かったと後悔。
あと、Nicoleに話しかけられてよく分からんからOK,OK連発する典型的な日本人になりましたw あとからGoogle先生で翻訳した文をTwitterで返信するなど時間差コミュニケーションとなりました。
日本語、英語ともにコミュニケーション能力を鍛えたいなと思いました。
