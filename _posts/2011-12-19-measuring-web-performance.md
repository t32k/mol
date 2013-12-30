---
layout: post
title: Navigation Timingを使ってパフォーマンス計測（Google アナリティクス）
categories:
- analytics
- javascript
- markup
tags:
- html5
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '6045'
---
<blockquote>本来のAdvent Calendarとは、12月1日からクリスマスの25日まで、カードに作られた窓を1日に1つずつ開けていくというものです。一方、技術系のAdvent Calendarは、12月1日から25日までの間、毎日違う人が特定のテーマに沿ってブログ記事を書くというものです。もちろん、ここでのテーマは「HTML5」になります。HTML5に関することならなんでもOKです！

<a href="http://atnd.org/events/21987">HTML5 Advent Calendar 2011 : ATND </a></blockquote>
ども、HTML5 Advent Calendar 2011, 19日目担当のt32kでございます。今回もがんばります！

若干、9日目の<a href="https://twitter.com/#!/jovi0608">@jovi0608</a>さんとかぶってますが、気にせずNavigation Timingを実際にどのように利用できるかについて書きたいと思います。

<h2>Navigation Timing</h2>
<a href="http://www.w3.org/TR/navigation-timing/">Navigation Timing</a>は<a href="http://www.w3.org/2010/webperf/">W3C Web Performance Working Group</a>が策定している仕様の一つで、ページの読み込み時間やネットワークにかかる時間など取得することができる仕様です。2011年12月現在、<strong>IE9+</strong>, <strong>Firefox7+</strong>, <strong>Chrome6+</strong>, <strong>Android Browser 4.0+</strong> (<a href=" http://caniuse.com/nav-timing">When can I use Navigation Timing API?</a>) が対応しています。

取れるタイミングというのは以下のようにいっぱいありますｗ
<ol>
	<li>navigationStart</li>
	<li>unloadEventStart</li>
	<li>unloadEventEnd</li>
	<li>redirectStart</li>
	<li>redirectEnd</li>
	<li>fetchStart</li>
	<li>domainLookupStart</li>
	<li>domainLookupEnd</li>
	<li>connectStart</li>
	<li>connectEnd</li>
	<li>secureConnectionStart</li>
	<li>requestStart</li>
	<li>responseStart</li>
	<li>responseEnd</li>
	<li>domLoading</li>
	<li>domInteractive</li>
	<li>domContentLoadedEventStart</li>
	<li>domContentLoadedEventEnd</li>
	<li>domComplete</li>
	<li>loadEventStart</li>
	<li>loadEventEnd</li>
</ol>
これの何が嬉しいかと言いますと、これまでページのWebパフォーマンスを計測するとなると、BODY要素の始めのほうでnew DateしてgetTimeして、BODY要素の終わりのほうで、またnew DateしてgetTimeして差分を取るのが一般的な計測方法だと思うのですが、それですとサーバー側と接続したりする時間などが考慮されておらず、実際の体感時間とずれた計測結果になります。

むしろ、こういったレイテンシこそ読み込み時間の大半を占める部分で重要になってきます。つまり、Navigation Timingを使えばこのような部分も計測することができ、みんなハッピーということですね。
<pre><code>var timing = window.performance.timing;
var loadTime = timing.loadEventEnd – timing.navigationStart;</code></pre>
こんな感じで、サクっとページの読み込み時間というのが取れます。

<strong>参考</strong>
<ul>
	<li><a href="http://css.dzone.com/articles/using-html5s-navigation-timing">Using HTML5's Navigation Timing API to measure Page Load speed | Web Builder Zone</a></li>
	<li><a href="http://www.html5rocks.com/en/tutorials/webperformance/basics/">HTML5 Rocks - Measuring Page Load Speed with Navigation Timing</a></li>
	<li><a href="https://developer.mozilla.org/en/Navigation_timing">Navigation Timing - MDN </a></li>
</ul>
<div></div>
<h2>Measuring Web Performance</h2>
とはいっても、ちょっと僕JavaScriptよく分からないし、取れるタイミングも多くてよく分かんないっす。って方は大丈夫！あきらめないで（誰 ってことで、このNavigation Timingを活用した「<strong>サイトの速度</strong>」というGoogle アナリティクスのメニューから利用できます。
<ul>
	<li><strong><a href="http://analytics.blogspot.com/2011/05/measure-page-load-time-with-site-speed.html"> Google Analytics Blog: Measure Page Load Time with Site Speed Analytics Report </a></strong></li>
</ul>
<div>この機能リリース当初は、下記のようなコードをトラッキングコードに追加する必要ありましたが</div>
<pre><code>_gaq.push(['_trackPageLoadTime']);</code></pre>
<a href="http://analytics.blogspot.com/2011/11/site-speed-now-even-easier-to-access.html">現在では、コード追加なしでレポートから確認することできる</a>と思います。なかったらコード追加して確認してみてください。
<p style="text-align: center;"><a href="/static/blog/2011/12/sitespeed.png"><img class="aligncenter  wp-image-3835 fig" title="sitespeed" src="/static/blog/2011/12/sitespeed.png" alt="" width="500" height="398" /></a></p>
これらの情報は、最初に述べたNavigation Timingに対応しているブラウザに、プラス、Google ツールバーをインストールしたInternet Explorer(9以前)からも情報を取得しています。

こういった情報が分かることで、読み込み時間が長いために離脱率が高いページなど改善の効果測定ができるようになります。

また、「<strong>技術</strong>」というリンクをクリックすればネットワーク、サーバーに関するタイミング情報も確認することができます。
<p style="text-align: center;"><a href="/static/blog/2011/12/tech.png"><img class="aligncenter  wp-image-3850 fig" title="tech" src="/static/blog/2011/12/tech.png" alt="" width="500" /></a></p>
<strong>参考</strong>
<ul>
	<li><a href="http://www.google.com/support/analyticshelp/bin/answer.py?answer=1205784">サイトの速度 - アナリティクス ヘルプ</a></li>
	<li><a href="http://analytics.blogspot.com/2011/12/greater-insights-from-site-speed-report.html">Google Analytics Blog: Greater insights from the Site Speed report - Technical section </a></li>
</ul>
<h2>Measuring Social Interaciton</h2>
<img title="social" src="/static/blog/2011/12/social.png" alt="" width="500" height="150" />

話は変わって、最近ソーシャルボタンが流行していますね、Twitter, Facebook, Google+などなどたくさんのいいね、シェアボタンがあります。ブログ読んでいると末尾にズラーッと並んだボタンをよく見かけます。あんなにつけて意味あるのかなーっと思ってしまいます。何よりも重いだろうよ。。。ってのが個人的な印象です。

しかし、そうゆうご時世かお仕事でも依頼があったので仕方なく実装したのですが、ちゃんと効果測定したいなと思い、Google アナリティクスで計測してみたいと思います。
<ul>
	<li><a href="http://code.google.com/intl/ja/apis/analytics/docs/tracking/gaTrackingSocial.html">Social Interaction Analytics - Google Analytics - Google Code</a></li>
</ul>
<pre><code>_gaq.push(['_trackSocial', network, socialAction, opt_target, opt_pagePath]);</code></pre>
基本となるのはこの_trackSocialという、_trackEventに似たメソッドです。これを利用して、Twitterのつぶやき数や、Facebookのいいね数をGoogle アナリティクス上から確認することができます。
<pre><code>// Facebook いいね
FB.Event.subscribe('edge.create', function(targetUrl) {
 _gaq.push(['_trackSocial', 'facebook', 'like', targetUrl]);
});</code></pre>
<pre><code>// Twitter つぶやき
twttr.events.bind('tweet', function(event) {
 if (event) {
 var targetUrl;
 if (event.target &amp;&amp; event.target.nodeName == 'IFRAME') {
 targetUrl = extractParamFromUri(event.target.src, 'url');
 }
 _gaq.push(['_trackSocial', 'twitter', 'tweet', targetUrl]);
 }
});</code></pre>
Facebook, Twitterに関しては、上記のコードを計測したいページに記述します。注意としては、iframe形式には対応していないので、公式サイトからいいねなどのウィジェットをダウンロードしてくるときはJavaScript形式にしてください。
<pre><code>&lt;a href="http://b.hatena.ne.jp/" onclick="_gaq.push(['_trackSocial', 'hatena', 'bookmark']);"&gt;...</code></pre>
Google+のプラス数は特に何もしなくても勝手に認識してくれます。

そのほかにも、はてなブックマーク、mixiチェックも実装しましたが、ブックマーク、チェック完了時点のイベントが取れない（分からない）ので、単純にonclick時にtrackSocialを飛ばす対応しました。この結果から出る数字というのは実際にブックマークされた数、チェック数ではないので注意してください。ただmixiチェックはmixiデベロッパーサイト、パートナーダッシュボードからCSV形式でいいね数、チェック数、いいね・チェックから流入数などがダウンロード可能なので、そこから確認してもいいかもしれません。

GREEのいいねに関してiframe形式でしかウイジェットが配布されてなかったのでお手上げです :(
<p style="text-align: center;"><a href="/static/blog/2011/12/socialaction.png"><img class="aligncenter  wp-image-3841 fig" title="socialaction" src="/static/blog/2011/12/socialaction.png" alt="" width="500" /></a></p>
実装してデータが集まると、Googleアナリティクスの「<strong>ソーシャル</strong>」のメニューからサイト内のソーシャルアクション数が確認できます。hatena:bookmark, mixi:checkは実際にブックマークが完了された数、チェックが投稿された数ではないこと考慮しておくにして、このサイトにおいてはFacebookのいいね！が多いねみたいなことが確認できます。
<h2>Practice</h2>
さて、ソーシャルインタラクションのウイジェットを置いたことで、当初に懸念していたページの読み込み時間はどーなっているでしょうか。

Google 「サイトの速度」で、ウイジェット設置前後の3週間を比較してみると、平均で<strong>0.8~1.0秒</strong>ほど読み込み時間が増加してしまいました。

<a href="http://www.gomez.com/download/aberdeen-gomez-best-in-class.pdf">Aberdeen Group (PDF)</a>というリサーチ会社が出したレポートによると、一般的に<strong>表示スピードが1秒遅くなると、PVは11%、CVは7%、顧客満足度は16%ダウンする</strong>といったことが報告されています。またこういった<a href="http://t32k.me/mol/log/performance-business/">ビジネスにおけるWebパフォーマンスの重要性</a>も訴えられています。

実際に、ソーシャルウイジェットを設置したサイトで、上記のような結果が起きたかといと、計測した3週間においては見受けられませんでした。というのもソーシャルウイジェット用にSCRIPT要素を5つくらい読み込んだのですが、BODY要素の最後の方に置いたので読み込みに時間はかかりますがレンダリングに対して余り影響しなかったのではないかと考えています。

とはいえ、利用率から考えてみると、<strong>ソーシャルアクション数 / ソーシャルウイジェットを置いたページのPV</strong>で算出してみると、<strong>0.2~0.01％</strong> という低い数値がでました。あんまり使われていないってことですね。。。

読み込み時間と言えば、Googleが読み込み時間をランキングに考慮するとかしないとか（最近まったく聞きませんね...）ありますし、単純に外部からスクリプトを多く読みこむことで、不具合の発生する確率も多くなるかもしれません。

やっぱりこんなもの取り外したい。でも取り外せないということで、単純にブックマークレット形式に変更しました。各ブックマークレットの方法は以下参照で。
<ul>
	<li><a href="http://pr.mixi.co.jp/2011/11/01/post-7.html#bookmarkle">気になるページをもっと共有しやすくする「mixiチェックブックマークレット」 | THINK SOCIAL</a></li>
	<li><a href="https://dev.twitter.com/docs/share-bookmarklet/translated/japanese">共有ブックマークレット | Twitter Developers</a></li>
	<li><a href="https://dev.twitter.com/docs/intents">Web Intents | Twitter Developers</a></li>
	<li><a href="http://b.hatena.ne.jp/register">はてなブックマーク - はてなブックマークをはじめる (セットアップ)</a></li>
	<li><a href="http://www.facebook.com/share_options.php">Share Bookmarklet | Facebook</a></li>
</ul>
現状は各ソーシャルウイジェットを生成するためにSCRIPT要素を読み込んでiframeを生成するパターンなのですが、ブックマークレットですと、投稿する利便性は落ちてしまいますがSCRIPT要素を読む込む必要もなくなるので安心です。非同期で読み込む方法も考えましたが、UIスレッドと非同期で読み込めるだけで読み込み時間自体は変わらないですし、なによりも管理が<a href="http://tokkono.cute.coocan.jp/blog/slow/index.php/xhtmlcss/asynchronous-loading-of-major-social-buttons/">複雑</a>です。
<p style="text-align: center;"><a href="/static/blog/2011/12/speed.png"><img class="aligncenter  wp-image-3847 fig" title="speed" src="/static/blog/2011/12/speed.png" alt="" width="500" /></a></p>
実際に施策後の経過を確認んしてみると変更前は3秒近くあった読み込み時間が、2秒台になりました。ソーシャルアクションに関しては、「いいね！」のブックマークレットがなくて「シェア」に変更する必要があったり、ソーシャルアクション計測するためのコードは元のiframeを生成するスクリプトに依存するので、それを読みこまなくなったため計測できず、単純にはてな、mixiチェックのようにclick数になり、正確な比較はできませんが、アクション数が激減したということは見受けられませんでした。

このサイトにおいて特にがっつりソーシャルと絡んでいくといった方向性もないので、パフォーマンスは犠牲にせずにこういった最小限のブックマークレットシェアボタンを置くというのが現実解かなと個人的には考えています。

ということで、結構マイナーだと思ってたNavigation Timingですが、Googleアナリティクス入れていれば実務でもガンガン使っていけると思いますんで、パフォーマンス改善に役立てもらえればと思います。
