---
layout: post
title: サイトの速度
categories:
- analytics
- performance
tags: []
status: publish
type: post
published: true
excerpt: "ごきげんいかがでしょう。みなさんはスマホWebアプリ作っていて、自分の作ったものは速いのか遅いのか気になりませんかね？僕は木に泣くりまくりすてぃです。"
cover_image: /2013/04-15-timer.jpg
---
<a href="http://www.flickr.com/photos/wwarby/3296379139/">Stopwatch | By wwarby Flickr!</a>

こんにちわ、あなたの<a href="https://twitter.com/t32k">@t32k</a>、ごきげんいかがでしょう。みなさんはスマホWebアプリ作っていて、自分の作ったものは速いのか遅いのか気になりませんかね？僕は木に泣くりまくりすてぃです。

そうゆうわけなもんで、表示速度とか計測してみようって話になるじゃないですかー、まさかストップウォッチで計測しないとは思うんですけどー、一応どのようにスピードを計測、そのアプリの性能を評価すればよいのか一緒に考えてみましょう。

僕が昔、ゴメス・コンサルティング（現：<del>コンピュウェア</del> モーニングスター） の<a href="http://t32k.me/mol/log/gomez/">セミナーに行ってきた時の話</a>ですが、ここの会社はサイトパフォーマンスの計測サービスを提供していて、計測で重要なのは『<strong>定期的かつ継続的かつ同手法にてパフォーマンス測定</strong>』と言っておられました。

サービスリリース時はスモールスタートなのでアプリもコンパクトですからスピードは速めかもしれません。しかし月日がたつにつれて、多くの機能が実装され、それに伴いサイトのスピードが落ちてはなんの意味もありません。計測した日がたまたま速かったのかもしれませんし、たまたま遅かったのかもしれませんので、定期的かつ継続的にかつ計測する必要性があります。また、1回目と2回目の測定条件（環境）が違ったりしては参考になりません。ましてや数ms単位でしのぎを削る我々にとってこの辺はシビアでかつ正確であってほしいわけです。

ですから、ストップウォッチや計測コードを毎回差し込むといった人間の手による対応ではコストが高すぎますし不正確な計測しか出来ません。そこですべてを自動化し計測する必要性があります。

## すべてを自動化ってそんなことできるの？

大抵のサイトに実装されているであろうGoogle アナリティクスを使えば可能です。

![](/mol/file/2013/04/s11.png)

上記Google アナリティクスのレポートから『<strong>平均表示時間</strong>』等を確認できます。『平均表示時間』と書いてありますが、英語メニューでは『Avg. Page Load Time』ですので、『平均読み込み時間』が適切かと思われます（ラベリングおかしい（●｀ε´●））
<blockquote>平均表示時間 - ページの読み込みにかかった平均時間（秒）

ga:avgPageLoadTime = (ga:pageLoadTime / ga:pageLoadSample) * 0.001
平均表示時間（秒）= ページの読み込みの合算値 (ミリ秒）÷ サンプル数 × 0.001
<p style="text-align: right;"><a href="https://developers.google.com/analytics/devguides/reporting/core/dimsmets/sitespeed">Site Speed - Dimensions &amp; Metrics Reference </a></p>
</blockquote>
と言った計算式で算出されております。これであればサイトの全ページを計測でき、なおかつ平均なので、ある程度ならした数値を得ることができます（外れ値は別途カスタムレポートとかで除外することもできます）し、パフォーマンス改善もPVの多いとこから対応したほうが効率的だということが理解できるでしょう。

<strong><span style="color: #333399;">[追記]</span></strong>　コメントに指摘されたように、値にばらつきがあるような場合（凹凸形状な分布）だとやはり、中央値を確認すべきなので、<strong>[分布]</strong>タブをクリックすれば、どの値の範囲に多いのか確認できます。
<p style="text-align: center;"><a href="/mol/file/2013/04/fig.png"><img class="aligncenter size-large wp-image-4889 fig" title="Distribution" src="/mol/file/2013/04/fig.png" alt="" width="540" height="340" /></a></p>
またディレクトリごとで読み込み時間の違いを確認したり、端末ごとでの読み込み時間を確認するといったことも可能でしょう。

さて、この読み込み時間ってのはどこから取ってきてるのかと言いますと、<a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html">Navigation Timing</a>という仕様を実装しているブラウザからです。ユーザーがページ遷移するとネットワークの接続、サーバーレスポンス、ブラウザ読み込みにかかった時間が自動的にブラウザに記録され、その情報をGAがサーバーに送ってるといった感じです。
<p style="text-align: center;"><img class="size-full wp-image-4848 aligncenter" title="Before" src="/mol/file/2013/04/f1.png" alt="" width="640" height="300" /></p>
これまでというか、一昔前まではそうゆうことを計測しようと思うと上記のようなコードを挿入して計測していた気がします。これをページの読み込み時間と定義してしまうのは、いささか問題があります。Aのページの読み込みを考えれば、当然Bとなど他のページから遷移したと想定され、Bのページのリンクを押してから、Aのベージの読み込み完了までが本来の意味での（体感的な）読み込み時間と考えるべきでしょう。つまり、上記のコードではネットワークやサーバーのやり取りの部分が考慮されてないことを意味します。またそもそも<a href="http://ejohn.org/blog/accuracy-of-javascript-time/">JavaScriptでの時間計測は不正確</a>ということも懸念されます。
<p style="text-align: center;"><img class="aligncenter size-full wp-image-4836" title="After" src="/static/blog/2013/04/f2.png" alt="" width="640" height="340" /></p>
より体感に近い読み込み時間を考慮すれば上図のような流れを計測すべきです。このような計測をJavaScriptだけで行おうとするとやや複雑な処理を記述しなければなりません。そんなめんどくさいことしなくても計測できるようになったのが、Navigation timingです。

<a href="/mol/file/2013/04/s21.png"><img class="size-large wp-image-4838 fig" title="技術" src="/static/blog/2013/04/s21.png" alt="" width="540" height="445" /></a>

もう一度、GAのレポート（[コンテンツ] &gt; [サイトの速度] &gt; [ページ速度]）を見てみると、『平均表示時間』の以外にも様々な指標が確認できるでしょう。
<ol>
	<li><strong>平均リダイレクト時間</strong>（ページを読み込む前にリダイレクトにかかった平均時間。リダイレクトがなければ0になる）</li>
	<li><strong>ドメインの平均ルックアップ時間</strong>（ページのDNS名前解決にかかった平均時間）</li>
	<li><strong>サーバーの平均接続時間</strong>（サーバーとのTCPコネクション確立に要した平均時間）</li>
	<li><strong>サーバーの平均応答時間</strong>（サーバーがユーザーリクエストに応答するまでの時間。ユーザーの所在地からサイトのサーバーにアクセスするネットワークの通信時間も含まれる）</li>
	<li><strong>ページの平均ダウンロード時間</strong>（ ページ（のみ）のダウンロードにかかった時間）</li>
</ol>
<strong>[エクスプローラ]</strong>タブの<strong>[技術]</strong>にはネットワークとサーバーに関する指標がレポーティングされています。『平均表示時間』の大半がこの部分で占められていれば、フロントエンドエンジニアではなくサーバーサイドエンジニアに文句を言いましょう。

<a href="/mol/file/2013/04/s3.png"><img class="size-large wp-image-4837 fig" title="DOM速度" src="/static/blog/2013/04/s3.png" alt="" width="540" height="445" /></a>
<ol>
	<li><strong>平均ドキュメントインタラクティブ時間</strong>（ドキュメントがパースされるのにかかった平均時間。このときDOMは完全に読み込まれてはいないが、ユーザー操作可能な状態。またユーザーの所在地からサイトのサーバーにアクセスするネットワークの通信時間も含まれる）</li>
	<li><strong>平均ドキュメントコンテンツ読み込み時間</strong>（ドキュメントがパースされDOMContentLoadedを実行するのにかかった平均時間。このときDOMは読み込まれているがCSSや画像などのリソースが読み込みが完了しているわけではない）</li>
</ol>
<strong>[エクスプローラ]</strong>タブの<strong>[DOM速度]</strong>にはドキュメント解析に関する指標がレポーティングされています。『平均表示時間』の大半がこの部分で占められていればDOMが複雑すぎるのでしょう。コーダーに文句を言いましょう。

平均ドキュメントインタラクティブ時間と平均ドキュメントコンテンツ読み込み時間はほぼ同義って思っていいでしょう（ここで差が出るケースがわからない）。

とりあえずこれらのレポートは特に手間を要することなくGAスニペットが挿入されていれば、サイトユーザーの1%のサンプリングレートで記録されるので、ほっといてもデータ溜まっていきます。1%じゃサイトの規模的に足りないって方は<a href="https://developers.google.com/analytics/devguides/collection/gajs/methods/gaJSApiBasicConfiguration#_gat.GA_Tracker_._setSiteSpeedSampleRate">_setSiteSpeedSampleRate()</a>を使えばサンプルレートを調整できます。
<ul>
	<li><a href="https://support.google.com/analytics/answer/1205784?hl=ja&amp;ref_topic=1282106">サイトの速度について - アナリティクス ヘルプ</a></li>
</ul>
&nbsp;

## 対応しているブラウザは？

さて、 このNavigation Timingに対応したブラウザってどんなもんなんでしょう。ヘルプには下記のように書いてありました。
<blockquote>サイトの速度のトラッキングは、HTML5 Navigation Timing インターフェース対応のブラウザか、Google ツールバーがインストールされたブラウザからの訪問に対してのみ行われます。該当する主なブラウザには、Chrome、Firefox 7 以降、Internet Explorer 9 以降、Android 4.0 以降のブラウザと、Google ツールバーがインストールされた Internet Explorer の以前のバージョンなどがあります。</blockquote>
ほうほう、Navigation Timingに対応してなくても、PCだとGoogleツールバー入れてたらいいんだね。って、俺の知りたいのはスマホだ、iOSだ！ということで。
<p style="text-align: center;"><a href="http://caniuse.com/#search=Navigation%20Timing%20API"><img class="aligncenter  wp-image-4873 fig" title="Navigation Timing" src="/mol/file/2013/04/f9b438c86a9e68bc50b3b9b65b4fca5e.png" alt="" width="870" /></a></p>
Can I use...で見てみると、iOS全滅じゃん！Desktop Safariでさえ対応してないと見ると、Appleさんは対応する気がないんでしょうかね...(´・ω・`)

とはいえ、<a href="http://japanese.engadget.com/2013/04/02/android-4-0-55/">Android4.0以降がバージョン別シェア半数</a>を超えたとかニュースで言っておりましたし、今後のモバイルの主流になっていくの当然であり、十分な量のデータサンプルを収集することも難なくできるでしょう。
<p style="text-align: center;"><a href="http://www.browserscope.org/?category=network&amp;v=top-m&amp;ua=Android%202.3%2CAndroid%204%2CiPhone%205%2CiPhone%206"><img class="aligncenter  wp-image-4875 fig" title="Browserscope" src="/mol/file/2013/04/cad4f2acb23f9d4aa554d564aa920837.png" alt="" width="870" /></a></p>
 また、Android4.0以降であればパフォーマンスの観点からいってもiOSとひけをとりません（むしろ4.0のほうがいいくらい）なので、Android4.0で集められたGAレポートのデータを暫定的にiOSでもこのくらいの読み込み時間かなーと考えといても良いかなと個人的には考えています。

## もうちょっと詳しく...

<p style="text-align: center;"><a href="https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming/Overview.html"><img class="aligncenter size-full wp-image-4866 fig" title="Navigation Timing" src="/mol/file/2013/04/nt.png" alt="" width="870" height="540" /></a></p>
もうちょっと細かく、Navigation Timingの仕様を見てみましょう。上図は仕様書にも書いて有るNavigation Timingの概要です。なんかいっぱいタイミングがあってごちゃごちゃします。まぁこのように細かく分けることでどこがボトルネックか突き止めることができるってもんです。とはいえ覚えきれないので、もっと大雑把に考えたのが下図。

<img class="aligncenter size-full wp-image-4840" title="three" src="/mol/file/2013/04/f3.png" alt="" width="400" height="340" />

ブラウザー、ネットワーク、サーバーの登場人物は3人です。『読み込み時間』とひとくくりに言っても3つのカテゴリーに分けて考えることができます。つまり問題を整理して対応策を考えることできます。

さらに、ブラウザー、ネットワーク、サーバーで色分けし、先ほどのGAレポートの項目とNavigation Timingの項目を照らし合わせたのが下の図。

<img class="aligncenter size-full wp-image-4861" title="f4" src="/mol/file/2013/04/f4.png" alt="" width="750" height="750" />

やっべーわかりやっしーちょーわかりやっしー。

とこのように、Google アナリティクスの『サイトの速度』を利用すれば、公正でかつ正確なサイトのパフォーマンス評価をすることが可能です。また、それに対する策も考えやすいといったように開発者にやさしい機能となっていますので、みなさんじゃんじゃん使ってみてください。

最後に地域が日本で、ブラウザーがAndroidのスマホ用のサイトの速度カスタムレポート作っときました。
<ul>
	<li><strong><a href="https://www.google.com/analytics/web/template?uid=tyEajMvPSySkw9VSN6vzMg">Navigation Timing用カスタムレポート</a>（スマホ用）</strong></li>
</ul>

最後にGAの『サイトの速度』レポートはできて日が浅く（そもそもNavigation Timing自体仕様が勧告でない）、データが集まりにくかったりかゆいところに手がとどかなかったりするのは致し方無いかないう印象です。もし、お金払ってでももっと正確なデータが欲しいという方は、<a href="http://www.keynotesystems.jp/#!measurement-and-monitoring/c196n">Keynote Systemsのような有料の計測サービス</a>を利用するのもひとつの手段かと思います。

## 参考

<ul>
	<li><a href="http://www.html5rocks.com/en/tutorials/webperformance/basics/">Measuring Page Load Speed with Navigation Timing - HTML5 Rocks</a></li>
	<li><a href="http://www.igvita.com/2012/04/04/measuring-site-speed-with-navigation-timing/">Measuring Site Speed with Navigation Timing - igvita.com</a></li>
	<li><a href="http://blog.d-bow.com/post/17368332231/measuring-page-load-times-navigation-timing-api-vs">dblog, Measuring Page Load times: Navigation Timing API vs Inline JavaScript with the Date object</a></li>
	<li><a href="http://www.html5rocks.com/ja/tutorials/internals/howbrowserswork/">ブラウザのしくみ: 最新ウェブブラウザの内部構造 - HTML5 Rocks</a></li>
	<li><a href="http://66.7percentangel.com/2011/12/breaking-down-onload-event-performance-bookmarklet/">Breaking Down onLoad Event – Performance Bookmarklet | Kasia Drzyzga</a></li>
</ul>
