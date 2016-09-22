---
date: 2012-09-28
title: Google Analytics トラッキング スニペット再考（2012）
categories:
    - analytics
---


秋色日毎に深まりこんちわ、@t32kだ。前回も少し言いましたがPageSpeedにモバイル版というのがありまして、デスクトップ版とは少々違うことをこいつは物申してきます。テストするページにもよりますが例えば、デスクトップ版であれば、__「ブラウザのキャッシュを活用する」__ や __「圧縮を有効にする」__ がHigh priorityな対策としてよく指摘されます。モバイル版でもそれらは重要かつ効果のある対策ですが、さらに対応しておきたいのが __「JavaScript の解析を遅延する」__ という対策です。

ざっくり言えば、そのJavaScriptが本当に必要になるまで後にとっておくということです。スマホなどの携帯端末は言うまでもなく、デスクトップPCに比べれば非力なので、このような端末ではJavaScriptを解析するのにもなかなか時間を要してしまうので、注意しましょうってことです。

PCサイトで、それも単純にドキュメント閲覧のようなページのパフォーマンス対策なんて、HTTPリクエストを減らすことだけ考えていれば十分事足りるなぁと個人的には考えています。ただ、最近やってるお仕事はスマホ向けのWebアプリ制作でして、JSゴリゴリ使ってます。。。この辺りのパフォーマンス対策というのをもうちょっと真剣に考えたいお年頃になってきたので、今回がんばってみます。

ただ、僕はJSは書けないので難しいことはよく分からんとです。お先真っ暗、八方塞がりです。唯一気になっていることは今のプロジェクトでhead要素に入れてあるGoogleアナリティクスのスニペットって本当にここでいいのか？ということです。これね、これ。

```html
<script type="text/javascript">
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XXXXX-X']);
  _gaq.push(['_trackPageview']);
  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();
</script>
```

+ [Google Analytics 非同期トラッキングコード再考（2010） - MOL](https://t32k.me/mol/log/asynchronous-tracking/)

はい、2年前にこの記事を書いたのは僕でして、そこでは`</head>`の直前に入れるということで結論づけました。ただこれはPCサイト前提での話なので、今のスマホ時代にも通じるのかもう一度考えてみましょう。

## script要素の読み込みと評価

[![fig_1.png (500×300)](/static/blog/2012/09/fig_1.png)](http://calendar.perfplanet.com/2011/lazy-evaluation-of-commonjs-modules/)

script要素を入れることでかかるコストについて上記の図のような感じですね。LatencyとDownloadが読み込みに関わるところで、普通にscript要素を読み込むと、通常のリソースは並列ダウンロードできるのに対して、script要素は他のリソースのダウンロードをブロッキングします。まぁ、scriptを早い段階で読み込むとそれだけページ表示に余計に時間がかかってしまいます。この点でノンブロッキングな読み込みを実現したのがGoogle Analyticsの非同期トラッキングコードで並列ダウンロードが可能となりました。また、トラッキング用のJSファイルにはga.jsには12時間の有効期限が設定されているので、次ページビュー、当日中くらいのセッション再開後もキャッシュが有効となり、LatencyとDownloadの部分は省略できます。

ただ、お気付きの通りParsingとEvaluationはキャッシュがあろうがなかろうが毎回コストを支払わなければなりません。しかもParsingとEvaluationの実行中はレンダリングが止まってしまいます。PCサイトであればこの点が無視できるほど短い時間で完了するので、head要素においても大した影響がないということでした。事実、@tobieさんの記事でもjQeuryのParsingとEvaluationのコストはMacBook Proが35msに対して、iPhone4が320msかかっている調査結果でした。つまり、jQueryを使おうが使わまいが、キャッシュが効いてようが効いてまいが、iPhone４ユーザーはjQueryが読み込まれている時点で毎回320ms（設置場所によっては）レンダリングが止まる時間ができるということです。

![ Google Analyticsの非同期トラッキングコードはノンブロッキングに読み込みできるがscript実行中はレンダリングを止める](/static/blog/2012/09/load_scripts_async.png)

## Google Analyticsの実行コスト

そこでjQueryのテストのGoogle Analytics版を作ってみました。Google Analyticsは基本的にページビュー計測を目的に入れると思いますので、単純に評価だけでなく毎ページごと実行（ビーコン画像発行）されると想定したテストです。10回アクセスしてその平均値をグラフにしました。

![](/static/blog/2012/09/fig2.png)

iPhone3Gは論外ですけど、今現在でも広く使われてそうな機種（iPhone4やGALAXY S2）でも100ms~200msくらい実行に時間がかかっています。これがhead要素に入ってるこということは、それ以降のレンダリングが100ms~200msストップしているということになります。（実際の実装状況をかんがみるともう少し掛かりそうな気がする）

100msというとニールセン博士のウェブサイトの応答時間では“0.1秒までなら応答が瞬時に返ってきたという印象を与える“と述べていますので、Google Analytics だけでこの貴重な0.1秒使ってしまうことは非常にもったいないと個人的には考えます。

## headか、bodyか

では、単純に`</body>`の直前にスニペットを配置しても問題無いのでしょうか？Steve SoudersはJavaScript Performance (at SFJS)でGoogle Analyticsのスニペットの設置場所についてまとめています。

`</head>`の場合

+ script loads later
+ beacon fires later
+ blocks fewer async(Opera)
+ may block rendering

`</body>`の場合

+ script loads last
+ beacon fires late
+ doesn’t block async
+ doesn’t block rendering

はい、結局トレードオフの関係にあります。スニペットを単純に下に置けばレンダリングをブロックしませんが、その分ビーコン画像の発行が遅れます。そもそも、非同期トラッキングコードがリリースされた時のメリットにデータの収集・精度の向上が挙げられています。つまり、スニペットがページ下部にあればページを完全にロードしないで次のページへ遷移してしまった人などが計測できなくなります。この部分をどう捉えるかで設置場所は決まってくるでしょう。

そもそも、ページ読み込み完了も待てないページビューをページビューとしてカウントしてもいいもなのかという個人的な疑問もあります。というより、ユーザーの満足度 >>> (越えられない壁 )  >>> アクセス解析の精度だと考えるので僕はスマホサイトに関しては`</body>`の直前に設置したほうが良いと考えます。(スマホ用のga.js作ればいいのにと思ったり。jQueryにおけるZeptoみたいにIE対応とか考えなかったらもう少しシンプル・軽量化出来ると思うけど。)

ちなみに、HTML5のボイラープレート（ひな形）を見てみると、デスクトップ、モバイル版ともに</body>の直前に配置されています。

> Finally, an optimized version of the latest Google Analytics tracking code is included. Google recommends that this script be placed at the top of the page. Factors to consider: if you place this script at the top of the page, you’ll be able to count users who don’t fully load the page, and you’ll incur the max number of simultaneous connections of the browser.

注意書きとしても同じようなことが言われています。あと、head要素に置けばビーコン画像リクエストによる同時接続数の1つを消費してしまうことも懸念点としてあげられています。

## 参考

+ [ブラウザって毎回Javascriptを解析するの？](http://readhn-jp.blogspot.jp/2012/02/javascript.html)
+ [Optimizing the asynchronous Google Analytics snippet · Mathias Bynens](https://mathiasbynens.be/notes/async-analytics-snippet)
+ [CSS/JavaScriptのAsynchronous Loadingをめぐる熱い論議 | ゆっくりと…](http://tokkono.cute.coocan.jp/blog/slow/index.php/web-technology/non-blocking-asynchronous-loading-of-css-javascript/)



