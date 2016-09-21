---
date: 2014-12-24
title: Smashing Magazineのパフォーマンス改善ケースが凄まじい件
subtitle: Improving Smashing Magazine’s Performance
categories: 
    - development
cover_image: "/2014/12-24-cover.jpg"
excerpt: 12/13にバンクーバーで開催されたThe Style & Class Conference 2014に参加して感銘を受けたのでVitaly Friedman氏のセッションを紹介するよ。
---

[Frontrend Advent Calendar 2014 - Qiita](http://qiita.com/advent-calendar/2014/frontrend)の24日目。たぶん。知らんけど。

![The Style & Class Conference 2014](/mol/images/2014/12-24-fig01.jpg)

ちょっと前になるが12/13にバンクーバーで開催された[The Style & Class Conference 2014](http://www.eventbrite.com/e/the-style-class-conference-tickets-13842235499)に参加してきた。前日に[Smashing Conference](http://smashingconf.com/)が、ウィスラーというバンクーバーから比較的近い所で開催されていて、本当はそっちに行きたかったんだけど高額なため、地元コミュニティのほうにだけ参加した。ウィスラーの方の記事は[@ygoto3が書いてたっぽい。](http://www.ygoto3.com/?p=107)

Smashing Conferenceで登壇していた[John Allsopp](https://twitter.com/johnallsopp)氏や[Val Head](https://twitter.com/vlh)氏もこのカンファレンスで登壇するということで、『なんだ、ウィスラーのついでかよー』と思い全然期待してなかったのだが、行ってみたらカンファレンス全体の構成などすごく考えられていて、とても素晴らしいカンファレンスだった。

そんなわけで、今回はその中で最も気に入った[Vitaly Friedman](https://twitter.com/smashingmag)氏のセッションを紹介したいと思う。

## Improving Smashing Magazine's Performance

![Vitaly Friedman](/mol/images/2014/12-24-fig02.jpg)

+ [Improving Smashing Magazine's Performance: A Case Study](http://www.smashingmagazine.com/2014/09/08/improving-smashing-magazine-performance-case-study/)

講演内容と同じ内容と思われる記事がすでに9月に上がっているみたい。バックエンドからフロントエンドまでいろいろなことやってみるみたいで、めちゃめちゃ長文なので時間あるときにでも読んでおくとよい。その中でも僕が気に入ったのがCritical CSSの対応をしていたことだ。

### Critical Rendering Path

Critical Rendering Pathとは、HTML/CSS/JSなどのバイトの取得からピクセルとしてレンダリングする必須処理までの間の段階のことを言い、Critical CSSとはページの最初のレンダリングをブロックする可能性のあるCSSのことを言う。

[![Critical Rendering Path](http://t32k.me/static/blog/2013/07/31.png)](https://docs.google.com/presentation/d/1IRHyU7_crIiCjl0Gvue0WY3eY_eYvFQvSfwQouW9368/present?slide=id.p19)

なぜCSSがレンダリングをブロックするのかというと、上図の通り、レンダリングを完成するにあたってブラウザはDOMとCSSOM(CSSオブジェクトモデル)が必要なわけでして、スタイルシートがダウンロードされない限りレンダリングが開始されないわけだ。

1. HTML マークアップを処理して DOM ツリーを作成
2. CSS マークアップを処理して CSSOM ツリーを作成
3. DOM と CSSOM を組み合わせてレンダーツリーを作成
4. レンダーツリーでレイアウトを実行して各ノードの形状を計算
5. 各ノードを画面にペインティング

+ [Render-tree construction, Layout, and Paint — Web Fundamentals](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ja)

少なくともブラウザに何かが描画されるまでには上記のような流れをふまないといけない。

そうゆうわけで、是が非でも速く描画するために、Critical Rendering Pathの最適化をしようとすると以下のことに気をつけなければならない。

+ クリティカル リソース数の最小化
+ クリティカル バイト数の最小化
+ クリティカル パス長の最小化

ことCSSだけに関して言えば、リソース数の最小化はスタイルシートを何個も読み込まず、1個にまとめればよいし、バイト数の最小化は[CSSO](https://github.com/t32k/grunt-csso)や[gzip](https://github.com/t32k/speed/blob/master/articles/gzip.md)をかけてやればよい。

まぁそれらはそんなに難しいことではないので、すぐにでも対応できると思われる。問題なのはクリティカル パス長（音的にリヴァイ兵長みたいな感じなので以後Critical Path Lengthと表記する）の最適化だ。

基本的には外部スタイルシートとして読み込むファイルを1個にまとめれば、HTML読み込んで、そのCSSを読み込むのがCritical Path Lengthの最短じゃねーのかと思うが、それではGoogle様が認めてくれない。

試しに、[PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/?hl=ja)で僕のプロフィール（単純な静的ページで外部CSSファイル1個）ページ：[t32k.me](http://t32k.me/)を計測してみると、『__スクロールせずに見えるコンテンツのレンダリングをブロックしている JavaScript/CSS を排除する__』なことを言われモバイル評価で89点といった結果が返ってきた。

![PageSpeed Insights：Before](/mol/images/2014/12-24-fig03.png)

で、対処法として[CSSの配信を最適化](https://developers.google.com/speed/docs/insights/OptimizeCSSDelivery)しなさいと言われる。こっちの説明より[Web Fundamentals](https://developers.google.com/web/fundamentals/)の説明のほうが分かりやすいのでこっちを引用。

> __インライン レンダリング ブロック CSS__  
クリティカル CSS は、HTML ドキュメント内で直接インライン化することをおすすめします。これにより、クリティカル パスの追加ラウンドトリップが削減され、適切に設定できれば、HTML が唯一のブロック リソースの場合に「1 ラウンドトリップ」のクリティカル パス長が実現できます。  
― [PageSpeed Rules and Recommendations](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/page-speed-rules-and-recommendations)

つまり、外部スタイルシートを読み込んでいては1.) HTMLを読み込む、2.) 外部CSSファイルを読み込むので、最低でも2ラウンドトリップ（往復）しないといけない。ゆえに描画が遅くなるのでHTML内にインラインで記述しなよっと仰せられておる。

でも、だからといって全部CSSをインライン化しちゃうとHTMLが膨れ上がっちゃう。TCPスロースタートのせいで1回目のレスポンスで送信できるサイズは14KBなので、オーバーしちゃう。この辺りは以前に__HTTPリクエストを減らすためにシリーズ__で記事を書いたので参照してほしい。

+ [【序章】HTTPリクエストは甘え — MOL](http://t32k.me/mol/log/reduce-http-requests-overview/)
+ [【終章】我々には1000msの猶予しか残されていない — MOL](http://t32k.me/mol/log/reduce-http-requests-one-second/)

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/ref=nosim/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/51x2sA8N%2BTL._SL160_.jpg" alt="ハイパフォーマンス ブラウザネットワーキング―ネットワークアプリケーションのためのパフォーマンス最適化" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/ref=nosim/" name="azlinklink" target="_blank">ハイパフォーマンス ブラウザネットワーキング</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2014.12.24</div></div><div class="azlink-detail">Ilya Grigorik,和田 祐一郎,株式会社プログラミングシステム社<br />オライリージャパン<br />売り上げランキング: 130931<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116767/warikiru-22/ref=nosim/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

または、[Ilya Grigorik](https://www.igvita.com/)大先生の本を読んでおいた方がいい。

だもんで、必要なCSSだけインライン化しましょうよってことになる。それ（[Above the Fold](http://www.suzukikenichi.com/blog/above-the-fold%E3%81%A8%E3%81%AF/)）に必要なCSS、つまりCritical CSSを検出するのがnpmモジュールの[CriticalCSS](https://github.com/filamentgroup/criticalcss)だ。

[![ATFの例](/mol/images/2014/12-24-fig05.jpg)](http://www.filamentgroup.com/lab/performance-rwd.html)

簡単に説明すれば上図のようにファーストビュー（Above the Fold）だけに使うCSSを抽出してくれる。

ちなみにGruntプラグインで利用できるので、これを使って僕のプロフィールページ：t32k.meを改善してみる。

+ [filamentgroup/grunt-criticalcss](https://github.com/filamentgroup/grunt-criticalcss)

```javascript
grunt.initConfig({
  criticalcss: {
    custom_options: {
      options: {
        url: "http://localhost:8000",
        width: 1024,
        height: 768,
        outputfile: "_templates/includes/critical.css",
        filename: "skeleton.min.css"
      }
    }
  }
});
```

こんな感じでGruntfileの方は記述する。重要なのはwidht/heightで、ここで自分の好きなAbove the Foldを定義する。で出力したCSSをテンプレート側で読み込む。

今回は、1.) CriticalCSSでクリティカルCSSを生成、2.) CSSOでミニファイ、3.) Jadeでコンパイル読み込むという流れ。詳しくはGitHubにあげてあるので参照してね。

+ [t32k.github.io/Gruntfile.js](https://github.com/t32k/t32k.github.io/blob/master/Gruntfile.js)

で、Full CSSの方は、後から非同期で読み込む。こうしないとレンダリングをブロックするので。あ、ちなみにほぼ[Skeleton.css](http://getskeleton.com/)をそのまま使ってる(^_^;)

```html
<script>
/*!
  loadCSS: load a CSS file asynchronously.
  [c]2014 @scottjehl, Filament Group, Inc.
  Licensed MIT
*/
function loadCSS(href, before, media) {
  var ss = window.document.createElement('link');
  var ref = before || window.document.getElementsByTagName('script')[0];
  var sheets = window.document.styleSheets;
  ss.rel = 'stylesheet';
  ss.href = href;
  ss.media = 'only x';
  ref.parentNode.insertBefore(ss, ref);
  return ss;
}
loadCSS('/skeleton.min.css');
</script>
<noscript>
  <link rel="stylesheet" href="/skeleton.min.css">
</noscript>
```

で、Critical CSSに対応した結果をPageSpeedにかけてみると、

![PageSpeed Insights：After](/mol/images/2014/12-24-fig04.png)

めでたく、先ほどの指摘はクリアできました。わーい、97点٩(๑❛ᴗ❛๑)۶

ちなみに『ブラウザのキャッシュを活用する』はGitHub Pagesなので僕からHTTP Headerを変更できないのでほっとく。

## Speed Index <= 1000

なにをもって速いとするのか？というのは重要な問題だ。PageSpeed Insightのスコアも一種の指標となるだろうが、もう少し細かく検証したい。（事実、PageSpeedのスコアは90点くらいまでなら簡単に取れる）

最近は読み込み時間が体感速度を表しているように思えない。各種SNSボタンのJSが大量に読み込まれるが、それらは非同期で読み込まれるために実際の読み込み時間と体感速度には大きな乖離が見られるし、何千pxという長大なページで2,3スクロールしないと見えないような画像が読み込み時間にカウントされるのはどうだろう。はたまたdomContentLoadedだったらどうだろうか、うーん、あんましフロント関係なくね？

そんなこんなで現時点で一番有用な指標と個人的に考えているのが、WebPagetestで計測できる[Speed Index](https://github.com/t32k/webpagetest-doc-ja/blob/master/using-webpagetest/metrics/speed-index/index.md)だ。Speed Indexに関しても以前記事を書いた。

+ [WebPagetest in 5 minutes — MOL](http://t32k.me/mol/log/webpagetest-5-minutes/)

> So how fast is fast enough? A Speed Index of under 1000. And for professionals that get there, they should shoot for delivering the critical-path view (above the fold) in the first 14Kb of the page. — Paul Irish

Smashing Magazineの講演でも触れられていたが、やはりどれだけ速ければいいのかという問いに対して、[Web業界のベネディクト・カンバーバッチ](https://twitter.com/snookca/status/543210094431723520)である[Paul Irish](https://twitter.com/paul_irish)氏が言及していたようにSpeed Indexが1000以下になるのが望ましい。これは去年も来日してた時に言っていたのでGoogle様はそれを目標にしているのだろう。そうゆうわけでのクリティカル・パスの最適化である。

Smashing Magazineでは[grunt-perfbudget](https://github.com/tkadlec/grunt-perfbudget)を使って、定期的にWebPagetestを回していたらしい（CLIからWPTを動かすにはAPI Keyが必要なので個別に作者に連絡しなければならない）。

![](/mol/images/2014/12-24-fig06.png)

+ [WebPagetest - Visual Comparison](http://www.webpagetest.org/video/compare.php?tests=141223_RD_GJJ%2C141223_RX_G9D&thumbSize=200&ival=100&end=visual)

今回の改善によるSpeed Indexの変化だけど、GitHub Pagesでカスタムドメインしているため、どうしても最初にリダイレクトが入ってしまうせいで、改善前後のSpeed Indexは微減（2097 -> 1940）だが、Start Renderは1.8秒から1.6秒と確実に速くなっている。

Smashing Magazineのケースでも一連の改善の結果、1000近くにまで削減することができたそうだ。その結果、『__SmashingMagはサンパウロからEDGE回線で読むことができるただ一つのサイトだ__』と講演の最後にブラジルの読者からのツイートを誇らしげに紹介していたVitaly Friedman氏の笑顔が忘れられない。

## まとめ

そうゆうわけで、Smashing Magazineの改善ケースでやってること自体は特に目新しい物はないが、ひとつひとつのことを丁寧にしっかりやってる点が素晴らしいと思う。しかもSmashing Magazineのような長年運用している大規模かつ複雑なサイトでCritical CSSの対応などは相当めんどくさかったに違いない（もっと詳しく聞きたかった）。今回の簡単な静的ページであるプロフィールページの改善もめんどくさかったし。

結局、山ほどあるパフォーマンス改善策に優先度を決め、ゴールを決め、フロントとバックエンドをまとめ、戦略をもってパフォーマンス改善できる人なんてそうそういないよね？てか、対象となる知識大杉、てか、Vitaly Friedman氏ハンパなくね？って思った。

Smashing Magazineにはスーパーマンがいたけど、個人的にはもっと他のケースも知りたいというか、泥臭いのに共感したいと思っている。だって世の中そんなうまくいかないし、[テキスト主体で画像少なめのページでこれ速いだろうって言っても意味ねーし](http://httparchive.org/trends.php?s=Top1000&minlabel=Dec+15+2013&maxlabel=Dec+1+2014#bytesImg&reqImg)、世の中もっとゴテゴテしてるし複雑だ。この辺は緑の顔の緑の会社の人をチェックしていれば、いつか闇がにじみだしてくるのではと期待している。

+ [2014年のWebパフォーマンスふりかえり - 来年以降の期待etc ::ハブろぐ](http://havelog.ayumusato.com/develop/performance/e637-web_performance_2014.html)

僕の来年の目標はやっぱり、Speed Indexの知名度が低いのも[WebPagetest.org](http://www.webpagetest.org/)の見た目がうさくさいのが原因だと思っているので、リニューアルデザインをプルリクしてあげたいと思う。たぶん。知らんけど。



