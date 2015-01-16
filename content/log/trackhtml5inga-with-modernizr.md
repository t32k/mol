---
date: 2010-12-02
title: ModernizrでHTML5時代のWeb技術をトラッッキング
categories:
- analytics
---
<blockquote><strong><a href="http://atnd.org/events/10497">JavaScript Advent Calendar 2010 : ATND</a></strong>
2010年12月1日から25日まで、毎日違う人が JavaScript にまつわるブログ記事を書く企画です。
参加表明した順番が日付（12月◯日）となります。</blockquote>
こうゆうおもしろい催し事があるみたいなので僕からは便利なJSライブラリの紹介をばしたいと思います。
<h3>What is Modernizr?</h3>
<a href="http://www.flickr.com/photos/24374884@N08/5141958757/"><img class="alignleft size-full wp-image-2020" title="newt" src="/static/blog/2010/12/newt.jpg" alt="" width="151" height="191" /></a>

まずはタイトルにもある <a href="http://www.modernizr.com/">Modernizr </a>ですが、これはHTML5時代のWeb技術、最近では「<strong>NEWT</strong>」、New Exciting Web Technologies （HTML5、CSS3、SVG、XHR2、Geolocation... などの技術総称）と呼ばれている技術がブラウザで実装されているか検出してくれるライブラリです。

最近、開発者の<a href="http://east.webdirections.org/2010/speaker/paul-irish/">Paul Irishさんが来日</a>してその存在を知りました（汗

<!--more-->

Modernizr を読み込んだページにアクセスすると自動的にHTML要素のclass属性に対応状況がこん感じで記述される具合です。

<img class="fig" title="firefox" src="/static/blog/2010/12/firefox.png" alt="" width="402" height="268" />
<em>Firefox 3.6.12</em>

<img class="fig" title="chrome" src="/static/blog/2010/12/chrome.png" alt="" width="403" height="230" />
<em>Google Chrome 7.0.517.44</em>

<img class="fig" title="opera" src="/static/blog/2010/12/opera.png" alt="" width="403" height="239" />
<em>Opera 10.63</em>

機能が実装されていばその機能名、実装されていなければno-が頭につく感じですね。おおもとのHTML要素にclass属性がついたので、
<pre><code>.borderradius .hoge div {
 /* border-radiusのプロパティを記述 */
}
.no-borderradius .hoge div {
 /* border-radiusに対応していないから画像で再現する記述とか */
}</code></pre>
こんな感じで子孫セレクタを使って実装状況に合わせたスタイルを記述することができます。
<pre><code>if (Modernizr.localstorage){
  // localstorage 使う！使う！
} else {
  // 代替手段として Cookie 使ったりとか
}</code></pre>
もちろんJavaScriptからもこんな感じで分岐処理することも可能です。
<h3>Track HTML5 in Google Analytics</h3>
この非常に便利な Modernizr を利用して、Google Analytics のレポート上でも確認できるようにしてくれるのが <a href="https://github.com/smeranda/trackHTML5inGA">trackHTML5inGA </a>です。Modernizr で検出したプロパティをカスタム変数（デフォルトではスロット#5を使用する）で取り込んで Google Analytics に渡す感じでしょうか。（<a href="http://t32k.me/mol/2010/10/google-analytics-custom-variables-part1/">カスタム変数についてはこちらを参照</a>）

使い方はModernizrとtrackHTML5inGA をダウンロードしてきて任意のサーバーにアップして以下のコードをGATC（Google Analytics Tracking Code）の後にでも挿入しておきましょう。（※非同期版トラッキングコードのみに対応）
<pre><code>&lt;script type="text/javascript"&gt;
   // トッラッキングしたいプロパティを記述
   featuresToTrack = ['video','audio'];
   (function(d, t) {
     var s=d.createElement(t),x=d.getElementsByTagName(t)[0];
     s.async=1;s.src='js/trackHTML5inGA.js';
     x.parentNode.insertBefore(s,x);
   })(document, 'script');
&lt;/script&gt;</code></pre>
上記のfeaturesToTrackの部分にトラッキングしたいプロパティ（40種類くらいトラッキングできるプロパティはあるけど、GAの仕様上、配列内に記述できる文字列は55byte以内に納めなければならない）を記述することで、GAのレポートの<em>ユーザー</em> &gt; <em>カスタム変数</em> に <em>HTML5</em> の項目できているのでクリックすると、任意のプロパティを実装しているブラウザのセッション数などがわかります。もちろん、コンバージョンを設定すれば、実装機能別の成果を確認することができます。

<img class="fig" title="customvar" src="/static/blog/2010/12/customvar.png" alt="" width="470" height="352" />
<em>上記の場合、borderradius/boxshadow/webworkers/applicationcache とborderradiusをトラッキング</em>

これをうまく使えば、CSS3アニメーションを使ったバリバリインタラクティブ登録フォームを作成してその成果を確かめたり、application cacheを大いに活用すればパフォーマンス的に良くなるわけですからapplication cacheを実装していないセグメントと比べてどのくらい成果が違うかなど確認できるかなど使い方はあなた次第！

単一のプロパティであれば、カスタムセグメントでブラウザのバージョンごとの実装状況を調べて自力でセグメント分けすればいいのですが、これが複数のプロパティ（ex. border-radiusかつCSS AnimationsかつGeolocation APIを実装しているブラウザとか）を対象とするとややこしくなるので、やはりそういう点ではこのtrackHTML5inGAを使うメリットがあるのではないでしょうか。

そういうわけで、Modernizr と trackHTML5inGA の紹介でした。
<h3>宣伝</h3>
さて、なんか後半はアクセス解析っぽい話になっちゃいましたけど、よかったのかな...と。心配ついでにせっかくJS大好きっ子が見てると思うのでkanazawa.jsの宣伝もしとこ。

kanazawa.js は金沢市、石川県、北陸の近辺の JavaScript デザイナー・プログラマによるコミュニティです。月1で勉強会を開いていくつもりなので、近くに寄ったときはぜひ参加してください！

<ul>
  <li><a href="http://kanazawajs.tumblr.com/">Tumblr</a></li>
  <li><a href="http://twitter.com/kanazawajs">Twitter</a></li>
  <li><a href="http://www.facebook.com/pages/kanazawajs/109048162494785">Facebook</a></li>
  <li><a href="http://www.ustream.tv/channel/kanazawajs">Ustream</a></li>
</ul>
