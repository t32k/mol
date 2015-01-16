---
date: 2009-11-24
title: High Performance Web Design ~デザインから考えるハイパフォーマンスWebサイト~
categories: performance
---

<a href="http://www.cssnite-ishikawa.jp/">CSS Nite in ISHIKAWA</a>で話をしてから1ヶ月経ったので、薄れゆく記憶の復習も兼ねて思いの丈を綴ってみたｗ
<div id="__ss_2352987" style="width: 425px; text-align: left;"><a style="margin: 12px 0pt 3px; font-family: Helvetica,Arial,Sans-serif; font-style: normal; font-variant: normal; font-weight: normal; font-size: 14px; line-height: normal; font-size-adjust: none; font-stretch: normal; display: block; text-decoration: underline;" title="High Performance Web Design" href="http://www.slideshare.net/t32k/high-performance-web-design">High Performance Web Design</a><object style="margin: 0px;" classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="425" height="355" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true" /><param name="allowScriptAccess" value="always" /><param name="src" value="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=wpo-091026191440-phpapp02&amp;rel=0&amp;stripped_title=high-performance-web-design" /><param name="allowfullscreen" value="true" /><embed style="margin: 0px;" type="application/x-shockwave-flash" width="425" height="355" src="http://static.slidesharecdn.com/swf/ssplayer2.swf?doc=wpo-091026191440-phpapp02&amp;rel=0&amp;stripped_title=high-performance-web-design" allowscriptaccess="always" allowfullscreen="true"></embed></object></div>
<h3>1. What's High Performance?</h3>
ここでいうパフォーマンスというのはWebサイトの表示高速化についてです。つまり、ページをいかに早く表示させるかという課題です。でも、そうゆうのってサーバー側の問題でしょ？システムエンジニアの管轄じゃないの？と思われがちですが「<a href="http://warikiru.blogspot.com/2008/05/high-performance-web-sites.html">ハイパフォーマンスWebサイト</a>」の著者であるSteve Soudersの調査によると、<span style="font-weight: bold;">80:20</span>。一般的にユーザーの待ち時間の実に80%がブラウザ側、フロントエンドで費やされていて、サーバー側、バックエンドでの時間は全体の20%でしかないという結果が出ています。つまり、サーバー側でデータベースのチューニングやメモリ管理、アルゴリズムの見直しなどして処理時間を半分にできたとしても全体として見れば10%でしかないということです。要するにフロントエンドを預かるWebデザイナーの責任が重大と言うことです。
<h3>2. Why High Performance?</h3>
では、なぜパフォーマンスが重要なのでしょうか？パフォーマンスが悪いと何か都合が悪いのでしょうか？パフォーマンスをないがしろにしていると怖いよっていうデータを見せたいと思います。

<a href="http://news.cnet.com/8301-10784_3-9954972-7.html"><span style="font-weight: bold;">Google</span></a><span style="font-weight: bold;">：</span>0.5秒遅くなると、検索数が20%減少する
うん、怖いですね、メインの事業ですからね。

<span style="font-weight: bold;"><a href="http://www.scribd.com/doc/4970486/Make-Data-Useful-by-Greg-Linden-Amazoncom">Amazon</a>：</span>0.1秒遅くなると、売り上げが1%減少する
怖いですね、たった0.1秒遅くなることで数十億、数百億ぐらいの影響になってくるということです。このようにパフォーマンスが低下すれば収益に直に影響してくるといったケースが考えられます。だけども、うちはAmazonみたいに大きくないから考えすぎだよとおっしゃりたいかもしれません。

<a href="http://www.gomez.com/download/aberdeen-gomez-best-in-class.pdf"><span style="font-weight: bold;">Aberdeen Group</span></a>というリサーチ会社が出したレポートによると、一般的に表示スピードが1秒遅くなると、PVは11%、CVは7%、顧客満足度は16%ダウンするといったことが報告されています。こういった数値を知っていればパフォーマンス対策をするための目標を決めやすいのではないでしょうか。

またユーザービリティ的に見てもパフォーマンス低下は避けた方良いということが分かります。

<a href="http://www.useit.com/papers/responsetime.html"><span style="font-weight: bold;">反応時間の3つの重要限界</span></a>
<ul>
	<li>心理的・感情的な違和感を感じないのは0.1秒まで</li>
	<li>思考の流れが妨げられないのは1秒まで</li>
	<li>注意力を維持できる限界の時間は10秒まで</li>
</ul>
結局のところ、Time is Money！と言えるのではないでしょうか。つまり、ページをハイパフォーマンス化することでユーザーのストレスをなくし、ユーザーエクスペリエンス（体験）の質を向上させることで、結果収益にもつながってくるこということです。
<h3>3. How do you measure it?</h3>
次はどうやってページを計測・評価するのかといった面を考えてみましょう。

計測するためにはパフォーマンスツールが必要です。いろいろあるのですが、大きくは2つに分けられると思います。Packet SniffersはWebページのコンポーネントつまり画像などの部品がどのようにダウンロードされているのか教えてくれます。Performance Analyzersはあらかじめ決められた項目を評価してくれるツールです。まぁ、見てみましょう。
<h4>Packet Sniffers</h4>
<a href="http://www.fiddler2.com/fiddler2/">Fiddler</a>, <a href="https://addons.mozilla.org/ja/firefox/addon/1843">Firebug Net Panel</a>, <a href="http://www.apple.com/jp/safari/">Web Inspector Resources Panel</a>
ひとつひとつがバーチャートがコンポーネントを表しています。チャートの長さがダウンロードにかかった時間ですね。このようにグラフィカルに表示してくれるので、どのバーチャートが一番長いのか着目すれば、ボトルネックがすぐ見つかります。これを取り去るか縮小させれば表示速度改善につながりますね。とはいっても、このように差がはっきりしていないときもありますので、パフォーマンス初心者にとってはちょっと敷居高いかもしれません。
<h4>Performance Analyzers</h4>
Googleつくった<a href="http://code.google.com/intl/ja/speed/page-speed/">Page Speed</a>というのものありますが、これ見た感じ文字ばっかて嫌になっちゃいますよね評価項目も細かいことばかりです。これはGoogleだからやっていることなので普通のサイトに当てはめるのはちょっと酷です。ということで、僕はこちらをお薦めします。Yahooがつくった<a href="https://addons.mozilla.org/ja/firefox/addon/5369">YSlow</a>です。

13項目の視点からWebページをABCDEFの6段階でランク付けてくれます。これは良いですね。先程のPacket Sniffersは見たいに読み取る必要がないためです。総合評価がDと言われば次はCを目指そうと思うじゃないですか。各項目毎に評価してくれるのでちょっと見てみるとHTTPリクエストを減らしなさいよなどと注意されています。<span style="font-weight: bold;">Components</span>はページの部品・パーツがどのくらいの数ダウンロードされているのか教えてくれます。<span style="font-weight: bold;">Statistics</span>はコンポーネントの種類毎の容量が全体でのどのくらいの割合を占めているのか円グラフで表示してくれます。どうでしょうか、分かりやすい機能でやる気になってきませんか？僕は勝手にやる気になってきたので日本の主要なサイトをYSlowで評価してみました。

<img src="http://lh4.ggpht.com/_1drnogi3vdg/SwvxbuZSrdI/AAAAAAAAAtA/Iwqu_HduDg8/yslow.png" alt="YSlow評価結果" />
<span style="font-size: 85%;">2009/10/14  YSlow Ruleset applied: <span style="font-weight: bold;">Classic(V1)での評価</span></span>

D, E, Cとか低い評価が目立ちますよね、これは仕方ないのかもしれません。というのも大抵のパフォーマンスを意識していないサイトはDかEといった評価になります（Ruleset:Classic(V1)で）。Cぐらいになって初めてここはちょっとパフォーマンスを意識しているなと感じるくらいです。Aにいたっては僕は2サイトしか知らないですね。GoogleとYSlowを作った米Yahoo!です。

その<a href="http://www.google.co.jp/">Google</a>なんですが、シンプルなページだからA評価当たり前だよねと思っちゃいそうですが、実は裏側を見てみますと。10個以上あったアイコンはCSSスプライトで1つの画像にまとまっていたり、シンプルなページであるのにも関わらず、さらに改行など取り除いてHTMLを圧縮しているなどの努力が見られます。こういった面もYSlowなら見逃さず評価してくれます。

YSlowの使い方ですが、最初のインストールをしてしまえば、ほんの2,3ステップでチェックできるので、是非皆さんも、自分のサイト、競合他社、大手のサイトなどチェックしてみて自分がどういう位置にいるのか確認してみてください。

というわけで、計測できないものは改善のしようがないということです。つまり、何か対策を行って評価しなければ次につながりません。対策→評価→対策→評価、このサイクルを回していくことで自ずとパフォーマンスは向上していくでしょう。
<h3>4. What should I do to improve?</h3>
では、パフォーマンスを改善するために私たちは何をすべきなんでしょうか？
Yahoo!が出している高速サイトを実現するための14のルールは先程紹介したYSlowの評価項目に対応しているので、ハイパフォーマンスWebサイトの本と共に対策していけば良いでしょう。
<ol>
	<li><span style="font-size: 85%;">HTTPリクエストを減らす</span></li>
	<li><span style="font-size: 85%;">CDNを使う</span></li>
	<li><span style="font-size: 85%;">Expiresヘッダを設定する</span></li>
	<li><span style="font-size: 85%;">コンポーネントをgzipする</span></li>
	<li><span style="font-size: 85%;">スタイルシートは先頭に置く</span></li>
	<li><span style="font-size: 85%;">スクリプトは最後に置く</span></li>
	<li><span style="font-size: 85%;">CSS expressionの使用を控える</span></li>
	<li><span style="font-size: 85%;">JavaScriptとCSSは外部ファイル化する</span></li>
	<li><span style="font-size: 85%;">DNSルックアップを減らす</span></li>
	<li><span style="font-size: 85%;">JavaScriptを縮小化する</span></li>
	<li><span style="font-size: 85%;">リダイレクトを避ける</span></li>
	<li><span style="font-size: 85%;">スクリプトを重複させない</span></li>
	<li><span style="font-size: 85%;">ETagの設定を変更する</span></li>
	<li><span style="font-size: 85%;">AJAXをキャッシュ可能にする</span></li>
</ol>
<a href="http://journal.mycom.co.jp/news/2008/03/27/016/index.html"><img src="http://lh6.ggpht.com/_1drnogi3vdg/SwvxbrbUZxI/AAAAAAAAAtE/m3Eu7b2WxKA/yahoo.png" alt="After A Grade 20 More Best Practices" /></a>

さらにYSlowでA評価とった人のためにもっと細かい20のルールとしてこんなことも提示されています。

<a href="http://coliss.com/articles/build-websites/operations/web-performance-best-practices-from-google.html"><img src="http://lh3.ggpht.com/_1drnogi3vdg/SwvxcGf74gI/AAAAAAAAAtM/K65OfQKOCVE/google.png" alt="Google Performance Best Practice" /></a>

はたまた、Yahoo!に重複するところもありますが、GoogleのPerformance Best Practicesというのもあります。

てか、多いですよねｗ　Too Many!

これら全て対策しようと思ったらWebページのパフォーマンスがあがる前に、制作者のパフォーマンスがダウンしてしまいます。しかも、ほとんどの会社にはWebパフォーマンスを専門で担当する人なんていないと思います。僕もパフォーマンスばかりやってるわけではないですから。ここで重要なのは対策を闇雲にこなすのではなく、効果的なものから優先度をつけて順にやれるところから行っていくことです。つまり、使えるリソースは有限だということです。
<div style="text-align: center;"><span style="font-weight: bold;">Make Fewer HTTP Requests</span>
<span>HTTPリクエストを減らす</span></div>
ということで、今回最も有効な対策、一番始めに考えるべき対策としてこれを挙げます。今日はこれだけです。本当にこれだけです。先程の14の対策を紹介したのですが、14全てやれば100%パフォーマンスが改善されるのかというと、そうでもありません。先のルールは有効的な対策として考えられるものから列挙してあるので、一番最初に紹介されているHTTPリクエストを減らすに対応するだけサイトが50%も速く表示されるようになったと言うケースも報告されています。
<h4>What’s HTTP Requests?</h4>
HTTPリクエストとはなんぞ？ってことですが、画像、スクリプト、スタイルシート、FlashなどのサーバーにHTTPプロトコルでサーバーにリクエストしているものですね。
<h4>Make Fewer HTTP Requests</h4>
HTTPリクエストを減らす方法としてハイパフォーマンスWebサイトの本では以下のようなことを挙げています。

<span style="font-weight: bold;">Image Maps</span>
うん、Webをまったく知らなかった大学生の頃に多用した。ボタンなどの画像を1個1個切り出すよりもまとめて1枚画像としたほうがリクエスト減らせますよと言うことです。
<span style="font-weight: bold;">CSS Sprites</span>
先程のGoogleのように、CSSを用いて一枚の画像を複数の画像のように見せることでリクエスト数を減らしています。
<span style="font-weight: bold;">Inline Images</span>
URLに画像データを長っい文字列として表現してそこから画像を生成するのでリクエストをしない。が多用するとコード量が増えるのが難点。
<span style="font-weight: bold;">Combined Scripts and Stylesheets</span>
JSとかCSSファイルをモジュール毎に管理するのは良いのだけれど、パフォーマンス的にはそれら１個にまとめた方が良いよとのこと。（開発時はモジュールで管理してページ生成時に動的にファイルを結合するやり方もあるのでシステムさんに相談してみよう。<a href="http://code.google.com/p/modconcat/">modconcat</a>とか）

というか、めんどくさいっすよねｗｗ
なんでこんなめんどくさいことをやらなければいけないのか。
そうは思いませんか。僕は思います。

似たような話で<a href="http://d.hatena.ne.jp/keyword/%A5%ED%A5%B7%A5%A2%A4%CF%B1%F4%C9%AE%A4%F2%BB%C8%A4%C3%A4%BF">Space Pen</a>という話がありますのでちょっと紹介。
ここで重要なのはボールペンという枠組みに固執することなく鉛筆という解を導き出したということです。今回のケースにおいてこの鉛筆にあたるのは何でしょうか？僕はデザインだと考えます。

つまり、デザイン・設計の段階からパフォーマンス意識すれば難しいことはしなくてもいいんです。最初からHTTPリクエストを増やすようなデザインにしなければいいんです。

じゃなぜ、HTTPリクエスト一杯のデザインになってしまうのでしょうか？そう考えたときに、僕の短いWebデザイナー人生とネットサーフィンをしてて思うサイト制作者が陥りやすい3つの欲求としてこんなことが挙げられるんではないかと思います。自分も含めて。

<span style="font-weight: bold;">目立たせたい！</span>
あれやこれやと目立たせることで画像だらけになってリクエストが増えてしまう。
<span style="font-weight: bold;">多機能にしたい！</span>
あれやこれやと機能を付加することでJSファイルの読み込みすぎといったことが考えられます。
<span style="font-weight: bold;">とりあえず、全部載せたい</span>
あれやこれやと自サイトのセールスポイントを挙げてしまい長大なページになってリクエストも増える。

<img src="http://lh5.ggpht.com/_1drnogi3vdg/Swvxi01iTEI/AAAAAAAAAtY/VmTsVCBGhhE/5plan.png" alt="5 Planes Model" />

これらを考える上で、<a href="http://www.jjg.net/elements/">Jesse James Garrettの5 Planes Model</a>をフレームワークとして使うと、第1の目立たせたい！は<span style="font-weight: bold;">表層</span>、<span style="font-weight: bold;">骨格</span>に当たる問題だと考えます。
<h4>1. 目立たせたい！</h4>
そもそも目立つとは何なのでしょうか。目立つ目立たないは周りとのオブジェクトの対比であって、必ずしも画像にすれば良いというわけでありません。

<img src="http://lh6.ggpht.com/_1drnogi3vdg/Swvxi4yj4nI/AAAAAAAAAtU/8oI6UcmOH9M/case.png" alt="Case" />

このCaseのようにさまざまなステークホルダーが主張を通した結果、1ページに沢山の画像が溢れています。このようなページが本当に制作側の思い通り、見られるのか検証してみる必要あります。<a href="http://www.feng-gui.com/">Feng-GUI</a>という人間の視覚の動きをシミュレートしてくれるサービスがあるので、先程のページデザインをシミュレートしてみると、全ての画像が目立っていないことが分かります。

<img src="http://lh5.ggpht.com/_1drnogi3vdg/SwvxcJCVPFI/AAAAAAAAAtQ/MBlGyCGOYdg/cssnite.png" alt="CSS Nite Banner Test" />

また、本当に画像にすれば目立つのかという疑問が僕の中で大きかったので実験してみました。自分のブログにて、右上部に「CSS Nite 石川に出ることになりました」というバナーを置いて、テキストリンク・画像ボタンで「詳細はこちら」表現したものを比較してみました。結果、テキストリンクで表示したほうが画像ボタンに比べて、90%以上多くクリックされました。<span style="font-size: 85%;">（参考：<a href="http://cssnite.jp/archives/post_1575.html">CSS Nite in Ginza, Vol.37：フォローアップ</a>）</span>

また、クックパッドのプレミアム会員への入会導線比較においても、バナー画像よりも、テキストリンクの方が3倍の効果を挙げたというデータが出ています。文脈（このケースの場合、プレミアムサービスに検索結果の並べ替えが含まれていたので、検索結果ページでの誘導が効果を発揮したということが分かる）を理解すれば必ずしも画像にする必要はないということが分かります。<span style="font-size: 85%;">（出典：<a href="http://cssnite.jp/archives/post_1460.html">CSS Nite in Ginza, Vol.32：フォローアップ</a>）</span>

つまり、デザインというのはデコレーションではありません。大事なのはコンテンツです。厚化粧することコンテンツを見えにくくしてはいけません。デザインというのはコンテンツをうまく伝えるための最適な手段を考えることです。
<h4>2. 多機能にしたい！</h4>
骨格、構造、要件、多岐にわたる要素を含んでいます。この背景にはjQueryやPrototypeなどのAJAXライブラリが普及してきたことによって、Webデザイナーでも比較的簡単にインタラクティブなサイトを制作できるようになってきたことが考えられます。

また、個人レベルにおいてもブログパーツの浸透などで、安易にブログパーツは貼り付けていけば、それに伴いJSファイルなどの増加の危険性が考えられます。自分のブログが何位だとかそういった自己顕示欲を主張するパーツなどはどんどん取り去っていけば良いのですが、リッチインタラクションと呼ばれる部分は難しいものがあります。

カルーセル、アコーディオン、ドラッグ&amp;ドロップなどのリッチインタラクションはある人にとっては便利と感じるかもしれません、しかしある人にとってはよく分からないと映るかもしれません。何を採用して何を採用しないか判断するためにはウェブ解析をする必要あります。

<a href="https://www.google.com/analytics/home/?hl=ja">Google Analytics</a>であなたのサイトのユーザーが使っているブラウザが何なのか分かります。もし、IE6などの古いブラウザのユーザーが大半ならば、リッチインタラクションを実現するためのJSファイルでブラウザがもたつくかもしれません。そうゆう場合はやめておいたほうが無難でしょう。

<a href="http://www.google.com/analytics/siteopt/?et=reset">Google Website Optimizer</a>では先程のバナーテストのように多変量テスト、A/Bテストが可能です。テストした結果、リッチインタラクションがあったほうが、コンバージョン率がいいというのなら採用しても良いかもしれません。

<a href="http://userheat.com/">User Heat</a>はFeng-GUIのように大まかなヒートマップを作成してくれます。もし、該当の機能部分がまったく見向きもされていなければ、素直に外しておきましょう。

何かを追加すれば、誰からしらの役に立つから良いのではないかと考えがちですが、<a href="http://www.ideaxidea.com/archives/2008/03/37_signals.html">37Signalsも自問している</a>ことに、”価値とは加えることと取り去ることのバランスなのです”とあるように、時としては引き算をすることで価値を増やせることも可能なのです。

結局はユーザーが何を欲しているのか、聞かなければなりません。Webデザイナーであろうとも、ウェブ解析ツールなど使うことで（今回紹介したツールはすべて無料）ユーザーのフィードバックを得ることできます。そして、無用な機能を実現するためのリクエストを削減することができます。
<h4>3. とりあえず、全部載せたい！</h4>
これは要件、戦略にあたる内容でしょうか。長すぎるページというのが存在します。果たして、このようなページは本当に読まれているのでしょうか？<a href="http://warikiru.blogspot.com/2008/09/visitor-attention-and-web-page-exposure.html">Click Tale社の調査</a>によると、ページの露出は上部から540pxを境に急激に下降しており、ユーザーが流し読みしていることが考えられます。<a href="http://www.usability.gr.jp/alertbox/whyscanning.html">なぜユーザーは流し読みする</a>のでしょうか。Jakob Nielsenは以下のことを挙げています。
<ul>
	<li><span style="font-size: 85%;">コンピュータ画面で読むのは目が疲れる。</span></li>
	<li><span style="font-size: 85%;">ウェブはユーザ主導型のメディアである。</span></li>
	<li><span style="font-size: 85%;">他の何億ものページと競争しなくてはならない。</span></li>
	<li><span style="font-size: 85%;">現代生活はあわただしい。</span></li>
</ul>
読まれないのなら読まれないで結構なのですが、Webサイトが存在する以上、なんらかのビジネスゴール：サイトの目的、ページレベルで言えば、してほしいアクションがあると思います。企業サイトであれば、資料請求のボタンを押すとかEコマースサイトならば商品をカートに入れるなどのアクションが考えられます。そういったアクションが長大なページの中に存在すれば、コンバージョンを下げる可能性も出てきます。
<div style="text-align: center;">決断に要する時間は、選択肢が増えるほど長くなる。
ヒック・ハイマンの法則</div>
つまり、目的を分割する必要があります。この辺はiPodの戦略がうまいかと思います。iPod, iTunes, iTunes Storeで目的を分けることで最適なエクスペリエンスを提供しています。考えてもみれば、iPodの小さな画面で曲名なんて編集したくないですよね。

Webサイトも同じで<span style="font-weight: bold;">1ページ 1テーマ 1スクリーン</span>を心がけることで、サイト制作者はユーザーに伝えたいことをより正確に伝えられるわけで、ユーザーもより理解が早くなる。そしてHTTPリクエストが必要以上に増えることもない。そのためには自分がサイトで何を伝えたいのか、ユーザーにどうしてほしいのか考えることで無駄をそぎ落とすことが可能です。

結局は人は求める結果が利益となると思うのなら待つのです。おいしいと評判のお店があると聞いたら並んで待つでしょ？僕もFlashの神様と言われる<a href="http://twitter.com/yugop">中村勇吾さん</a>が制作したFlashサイトなら3分でも待ちますよ。

しかし、一般的に、ユーザーが検索でたまたま見つけたサイトでは、あなたのサイトが本当は素晴らしいモノを提供していてもユーザーはその時点では知らないのです。ですので、そこで機会損失してしまうよりかはパフォーマンスをできる限り向上させておくのが吉となるのではないでしょうか。
<h3>5. Conclusion</h3>
パフォーマンスは収益やUXに大きく影響します。YSlowという計測ツールを手に入れました。パフォーマンスを上げるためにHTTPリクエストを減らすことが最優先事項です。そのためにはサイトで何をしたいのか、明確な目標を定めることが必要です。そうすれば、一貫性のあるデザインをすることができ、簡潔なコードにつながり、ハイパフォーマンスWebサイト！みんなHAPPY！

<img src="http://lh6.ggpht.com/_1drnogi3vdg/Swvxb30Xt_I/AAAAAAAAAtI/QRGYdfujud8/thank.jpg" alt="Thank You!" />

ありがとうございました。
Thank you!
