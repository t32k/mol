---
layout: post
title: Google Analytics トラッキングスニペット再考（2012年モバイル版）
categories:
- analytics
- performance
tags:
- GA
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '8881'
  _aioseop_description: モバイルサイトに関してはGoogle Analytics トラッキングスニペットはbodyの閉じタグの直前においたほうが良いと思う話。
  _oembed_4d67249e07576a8f03ec2c33172f2122: <iframe width="500" height="281" src="http://www.youtube.com/embed/0AP15IXFBnc?feature=oembed"
    frameborder="0" allowfullscreen></iframe>
  _oembed_0ca3d51c7a448ce8ace54a672436579d: <iframe width="540" height="304" src="http://www.youtube.com/embed/0AP15IXFBnc?feature=oembed"
    frameborder="0" allowfullscreen></iframe>
  _oembed_49666f3e01517604a61f581fb306ed5d: <iframe width="540" height="304" src="http://www.youtube.com/embed/0AP15IXFBnc?feature=oembed"
    frameborder="0" allowfullscreen></iframe>
  _oembed_90c66ffbfb449660459b94f164463f50: <iframe width="500" height="281" src="http://www.youtube.com/embed/0AP15IXFBnc?feature=oembed"
    frameborder="0" allowfullscreen></iframe>
---
秋色日毎に深まりこんちわ、<a href="https://twitter.com/t32k">@t32k</a>だ。<a href="http://t32k.me/mol/log/remote-debugging-with-chrome-for-android/">前回も</a>少し言いましたが<a href="https://developers.google.com/speed/pagespeed/insights#url=http_3A_2F_2Ft32k.me_2Fmol_2F&amp;mobile=true">PageSpeedにモバイル版</a>というのがありまして、デスクトップ版とは少々違うことをこいつは物申してきます。テストするページにもよりますが例えば、デスクトップ版であれば、「<strong>ブラウザのキャッシュを活用する</strong>」や「<strong>圧縮を有効にする</strong>」がHigh priorityな対策としてよく指摘されます。モバイル版でもそれらは重要かつ効果のある対策ですが、さらに対応しておきたいのが「<strong>JavaScript の解析を遅延する</strong>」という対策です。

ざっくり言えば、そのJavaScriptが本当に必要になるまで後にとっておくということです。スマホなどの携帯端末は言うまでもなく、デスクトップPCに比べれば非力なので、このような端末ではJavaScriptを解析するのにもなかなか時間を要してしまうので、注意しましょうってことです。

PCサイトで、それも単純にドキュメント閲覧のようなページのパフォーマンス対策なんて、HTTPリクエストを減らすことだけ考えていれば十分事足りるなぁと個人的には考えています。ただ、最近やってるお仕事はスマホ向けのWebアプリ制作でして、JSゴリゴリ使ってます。。。この辺りのパフォーマンス対策というのをもうちょっと真剣に考えたいお年頃になってきたので、今回がんばってみます。

ただ、僕はJSは書けないので難しいことはよく分からんとです。お先真っ暗、八方塞がりです。唯一気になっていることは今のプロジェクトでhead要素に入れてあるGoogleアナリティクスのスニペットって本当にここでいいのか？ということです。これね、これ↓
<pre><code class="javascript">&lt;script type="text/javascript"&gt;
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XXXXX-X']);
  _gaq.push(['_trackPageview']);
  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();
&lt;/script&gt;</code></pre>
<div><!--more--></div>
<ul>
	<li><strong><a href="http://t32k.me/mol/log/asynchronous-tracking/">Google Analytics 非同期トラッキングコード再考 | MOL</a></strong></li>
</ul>
はい、2年前にこの記事を書いたのは僕でして、そこでは<code>&lt;/head&gt;</code>の直前に入れるということで結論づけました。ただこれはPCサイト前提での話なので、今のスマホ時代にも通じるのかもう一度考えてみましょう。
<h2>script要素の読み込みと評価</h2>
<p style="text-align: center;"><a href="/static/blog/2012/09/fig_1.png"><img class="aligncenter" src="/static/blog/2012/09/fig_1.png" alt="JavaScript resource fetching, parsing and evaluation" width="500" /></a></p>
<p style="text-align: right;"><a href="http://calendar.perfplanet.com/2011/lazy-evaluation-of-commonjs-modules/">Performance Calendar » Lazy evaluation of CommonJS modules</a> より</p>
script要素を入れることでかかるコストについて上記の図のような感じですね。LatencyとDownloadが読み込みに関わるところで、普通にscript要素を読み込むと、通常のリソースは並列ダウンロードできるのに対して、script要素は他のリソースのダウンロードをブロッキングします。まぁ、scriptを早い段階で読み込むとそれだけページ表示に余計に時間がかかってしまいます。この点でノンブロッキングな読み込みを実現したのがGoogle Analyticsの非同期トラッキングコードで並列ダウンロードが可能となりました。また、トラッキング用のJSファイルにはga.jsには12時間の有効期限が設定されているので、次ページビュー、当日中くらいのセッション再開後もキャッシュが有効となり、LatencyとDownloadの部分は省略できます。

ただ、お気付きの通りParsingとEvaluationはキャッシュがあろうがなかろうが毎回コストを支払わなければなりません。しかもParsingとEvaluationの実行中はレンダリングが止まってしまいます。PCサイトであればこの点が無視できるほど短い時間で完了するので、head要素においても大した影響がないということでした。事実、<a href="https://twitter.com/tobie">@tobie</a>さんの<a href="http://calendar.perfplanet.com/2011/lazy-evaluation-of-commonjs-modules/">記事でもjQeuryのParsingとEvaluation</a>のコストはMacBook Proが<strong>35ms</strong>に対して、iPhone4が<strong>320ms</strong>かかっている調査結果でした。つまり、jQueryを使おうが使わまいが、キャッシュが効いてようが効いてまいが、iPhone４ユーザーはjQueryが読み込まれている時点で毎回320ms（設置場所によっては）レンダリングが止まる時間ができるということです。

[caption id="" align="aligncenter" width="500"]<a href="http://www.slideshare.net/souders/javascript-performance-at-sfjs"><img class=" " src="/static/blog/2012/09/load_scripts_async.png" alt="2009 load scripts async" width="500" height="375" /></a> Google Analyticsの非同期トラッキングコードはノンブロッキングに読み込みできるが、<br />script実行中はレンダリングを止める。[/caption]
<h2>Google Analyticsの実行コスト</h2>
そこでこのjQueryのテストのGoogle Analytics版を作ってみました。
<ul>
	<li><a href="http://dl.dropbox.com/u/356242/cost_ga.html">http://dl.dropbox.com/u/356242/cost_ga.html</a></li>
</ul>
Google Analyticsは基本的にページビュー計測を目的に入れると思いますので、単純に評価だけでなく毎ページごと実行（ビーコン画像発行）されると想定したテストです。
<p style="text-align: center;"><a href="/static/blog/2012/09/fig2.png"><img class="aligncenter" src="/static/blog/2012/09/fig2.png" alt="" width="500" /></a></p>
上記のページで10回アクセスしてその平均値をグラフにしました。詳細は下記スプレッドシートにまとめてあります。
<ul>
	<li><a href="https://docs.google.com/spreadsheet/ccc?key=0ApycgWz4whD1dHhIWXVSTTRobEN1elFtYndPb0FIcFE#gid=0">Cost of Execute Google Analytics</a></li>
</ul>
iPhone3Gは論外ですけど、今現在でも広く使われてそうな機種（iPhone4やGALAXY S2）でも100ms~200msくらい実行に時間がかかっています。これがhead要素に入ってるこということは、それ以降のレンダリングが100ms~200msストップしているということになります。（実際の実装状況をかんがみるともう少し掛かりそうな気がする）

100msというとニールセン博士の<a href="http://www.usability.gr.jp/alertbox/20100621_response-times.html">ウェブサイトの応答時間</a>では<strong>"0.1秒までなら応答が瞬時に返ってきたという印象を与える</strong>"と述べていますので、Google Analytics だけでこの貴重な0.1秒使ってしまうことは非常にもったいないと個人的には考えます。
<h2><code>&lt;/head&gt;</code>か<code>&lt;/body&gt;</code>か</h2>
では、単純に<code>&lt;/body&gt;</code>の直前にスニペットを配置しても問題無いのでしょうか？Steve Soudersは<a href="http://www.slideshare.net/souders/javascript-performance-at-sfjs">JavaScript Performance (at SFJS)</a>でGoogle Analyticsのスニペットの設置場所についてまとめています。

http://www.youtube.com/watch?v=0AP15IXFBnc

<strong><code>&lt;/head&gt;の場合</code></strong>
<ul>
	<li>script loads later</li>
	<li>beacon fires later</li>
	<li>blocks fewer async(Opera)</li>
	<li>may block rendering</li>
</ul>
<strong><code>&lt;/body&gt;の場合</code></strong>
<ul>
	<li>script loads last</li>
	<li>beacon fires late</li>
	<li>doesn’t block async</li>
	<li>doesn’t block rendering</li>
</ul>
はい、結局トレードオフの関係にあります。スニペットを単純に下に置けばレンダリングをブロックしませんが、その分ビーコン画像の発行が遅れます。そもそも、非同期トラッキングコードがリリースされた時のメリットにデータの収集・精度の向上が挙げられています。つまり、スニペットがページ下部にあればページを完全にロードしないで次のページへ遷移してしまった人などが計測できなくなります。この部分をどう捉えるかで設置場所は決まってくるでしょう。

そもそも、ページ読み込み完了も待てないページビューをページビューとしてカウントしてもいいもなのかという個人的な疑問もあります。というより、ユーザーの満足度 &gt;&gt;&gt; (越えられない壁 )  &gt;&gt;&gt; アクセス解析の精度だと考えるので僕はスマホサイトに関しては<code>&lt;/body&gt;</code>の直前に設置したほうが良いと考えます。(スマホ用のga.js作ればいいのにと思ったり。jQueryにおけるZeptoみたいにIE対応とか考えなかったらもう少しシンプル・軽量化出来ると思うけど。)

ちなみに、<a href="https://github.com/h5bp/html5-boilerplate/blob/master/index.html">HTML5のボイラープレート</a>（ひな形）を見てみると、デスクトップ、モバイル版ともに&lt;/body&gt;の直前に配置されています。
<blockquote>Finally, an optimized version of the latest Google Analytics tracking code is included. Google recommends that this script be placed at the top of the page. Factors to consider: if you place this script at the top of the page, you’ll be able to count users who don’t fully load the page, and you’ll incur the max number of simultaneous connections of the browser.
<p style="text-align: right;"><a href="https://github.com/h5bp/html5-boilerplate/blob/master/doc/html.md#google-analytics-tracking-code">Google Analytics Tracking Code</a></p>
</blockquote>
注意書きとしても同じようなことが言われています。あと、head要素に置けばビーコン画像リクエストによる同時接続数の1つを消費してしまうことも懸念点としてあげられています。

最後に自分が使ってるスニペット置いときますね。
<pre><code class="javascript">&lt;script id="gaq"&gt;
　var _gaq=[['_setAccount','UA-XXXXX-X'],['_trackPageview']];
　(function(d){var g=d.createElement('script'),s=d.getElementById('gaq');g.async=1;
　g.src=('https:'==location.protocol?'//ssl':'//www')+'.google-analytics.com/ga.js';
　s.parentNode.insertBefore(g,s)}(document));
&lt;/script&gt;</code></pre>
<a href="https://gist.github.com/3792738">Google Analytics Tracking Snippet — Gist</a>
<h3>あわせて読みたい</h3>
<ul>
	<li><a href="http://readhn-jp.blogspot.jp/2012/02/javascript.html">ブラウザって毎回Javascriptを解析するの？</a></li>
	<li><a href="http://mathiasbynens.be/notes/async-analytics-snippet">Optimizing the asynchronous Google Analytics snippet · Mathias Bynens</a></li>
	<li><a href="http://tokkono.cute.coocan.jp/blog/slow/index.php/web-technology/non-blocking-asynchronous-loading-of-css-javascript/">CSS/JavaScriptのAsynchronous Loadingをめぐる熱い論議 | ゆっくりと…</a></li>
</ul>
