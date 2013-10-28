---
layout: post
title: Google Analytics 非同期トラッキングコード再考
categories:
- analytics
- performance
tags:
- google analytics
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '28246'
  _aioseop_description: 非同期トラッキングコードが公式に推奨されるようになったので、ようやく重い腰を上げて調べてみた。長文です。。。
---
<a href="http://www.flickr.com/photos/subharnab/3779676969/"><img src="http://t32k.me/mol/file/2010/05/a.jpg" alt="" width="470" height="290" /></a>
<span style="color: #888888;"><em>by Subharnab</em></span>
<ul>
	<li><a href="http://analytics-ja.blogspot.com/2010/05/growing-google-analytics-ecosystem.html">Analytics 日本版 公式ブログ: 成長し続ける Google Analytics のエコシステム</a></li>
</ul>
非同期トラッキングコードが公式に推奨されるようになったので、ようやく重い腰を上げて調べてみた。長文です。。。

<!--more-->
<h3>目次</h3>
<ul>
	<li><a href="#section01">なぜ、非同期トラッキングコードが推奨されるのか？</a></li>
	<li><a href="#section02">読み込み時間の高速化 </a>
<ul>
	<li><a href="#section21">async属性に関して</a></li>
</ul>
</li>
	<li><a href="#section03">データの収集・精度の向上 </a>
<ul>
	<li><a href="#section31">トラッキングコードは&lt;/head&gt;の直前、&lt;body&gt;の直後？</a></li>
</ul>
</li>
	<li><a href="#section04">依存性からくるエラーの除去</a></li>
	<li><a href="#section05">まとめ</a></li>
</ul>
<h3 id="section01">なぜ、非同期トラッキングコードが推奨されるのか？</h3>
今回のトラッキングコードはurcin.js、ga.jsに続く大きな変更となります。非同期トラッキングコードの恩恵を受けるためには、以前のトラッキングコードを使用されている方は、当然変更しなければなりません。しかし、大規模サイトの場合などはアクセス解析担当者とコード実装者は違うことも多く、エンジニアさんにお願いしなければなりません。「え〜、前変えたばっかじゃん！」などと言われるかもしれません。。。そんな時にアクセス解析担当者はトラッキングコード変更のメリットを提示しなければなりませんね。

Analytics 公式ブログでは、非同期トラッキングコードの利点を以下のように説明しています。
<ul>
<blockquote>
	<li>ブラウザの実行順序改善によるページの読み込み時間高速化</li>
	<li>データの収集・精度の向上</li>
	<li>JavaScriptが完全に読み込まれていなかったときの依存性からくるエラーの除去</li>
<p style="text-align: right;"><a href="http://analytics.blogspot.com/2009/12/google-analytics-launches-asynchronous.html">Google Analytics Blog: Google Analytics launches async...</a></p>
</blockquote>
</ul>
てな感じで3つ挙げられているので、ひとつひとつ確認していきましょう。
<h3 id="section02">読み込み時間の高速化</h3>
これが、非同期トラッキングコード最大の利点なのではないでしょうか。やはり、<a href="http://t32k.me/mol/2010/04/using-site-speed-in-web-search-ranking/">Googleのランキングアルゴリズムに読み込む速度が加わった</a>手前、自社サービスがボトルネックとなっていては示しがつきませんしね。

非同期トラッキングコードについて説明していくのですが、まず前提知識としてページの読み込まれ方について解説します。HTTP/1.1の仕様に「ひとつのホスト名（EX: www.t32k.com, img.t32k.comなど）に対して並列ダウンロードできるコンポーネントは数は2つまで」と制限されています。（実際のブラウザ実装は6つとかだけど、IE6,7は2つまで）

<a href="http://t32k.me/mol/file/2010/05/1.png"><img class="fig" title="1" src="http://t32k.me/mol/file/2010/05/1.png" alt="" width="460" height="110" /></a>

上記のグラフは簡単なモデルですが、すべて同じホスト名から読み込んでいます。まず、htmlファイルが読み込まれ、画像などのコンポーネントが2個ずつ読み込まれていきます。

このとき、同じホスト名から読み込んでいる外部JavaScriptファイルがページの先頭で読み込まれていた場合はどうなるでしょうか？それを表したのが次のグラフです。

<a href="http://t32k.me/mol/file/2010/05/2.png"><img class="fig" title="2" src="http://t32k.me/mol/file/2010/05/2.png" alt="" width="460" height="110" /></a>

どうでしょうか。仕様どおりなら「script + img」と並列に読み込まれるはずですが、そうはならずにscriptファイルひとつしか読み込まれていません。つまり、scriptファイルを最初に読み込むでしまうとダウンロード・レンダリングが止まってしまいます。そのため、<a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/ref=nosim/">ハイパフォーマンスWebサイト、高速サイトの実現のための14のルール</a>のひとつ「ルール6：スクリプトは最後に置く」というものがあります。

<a href="http://t32k.me/mol/file/2010/05/3.png"><img class="fig" title="3" src="http://t32k.me/mol/file/2010/05/3.png" alt="" width="460" height="110" /></a>

このような理由から、非同期以前のトラッキングコードは&lt;/body&gt;の直前に置くことが推奨されています。出来る限りページ最下部に置くことでダウンロード・レンダリングを止めないようにしています。上記のグラフのような感じですね。ページを表示するために必要なコンポーネントはscriptの手前ですべて読み込まれているのでこれが最善策なのかなと。

<a href="http://t32k.me/mol/file/2010/05/4.png"><img class="fig" title="4" src="http://t32k.me/mol/file/2010/05/4.png" alt="" width="460" height="110" /></a>

しかし、非同期トラッキングコードはダウンロードの中断を考えなくてもいいので上記のようなグラフになります。なおかつ、Google Analyticsの解析コードga.jsは、www.google-analytics.comから読み込まれていますので、トラッキングコードを挿入したページを読み出すホスト名とは異なるはずなので、ページのレンダリングとは非同期に読む込むことができます。
<h4 id="section21">async属性に関して</h4>
<pre>ga.type = 'text/javascript'; ga.async = true;</pre>
話はちょっと変わりますが、非同期トラッキングコードについて調べていると、HTML5で定義されている<a href="http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async">async属性</a>によってこの非同期を実現しているのでasync属性に対応しているFx3.6しか効果がないと書いている人がちらほらいたのですが、それは誤解です。

<a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462">続・ハイパフォーマンスWebサイト</a>では、async属性を使わなくてもブラウザの実行をブロックしないスクリプトの読み込みテクニックとして以下の6つを挙げています。
<ul>
	<li>XHR eval</li>
	<li>XHR インジェクション</li>
	<li>iframe スクリプト</li>
	<li>Script DOM要素</li>
	<li>Script Defer</li>
	<li>document.writeによるSCRIPTタグ書き出し</li>
</ul>
今回の非同期トラッキングコードではSCRIPT要素をDOMを使って生成することで実現しています。なので、ほとんどのブラウザで非同期で読み込むことが可能です。async属性を記述しているのは明示的に非同期で読み込むことをブラウザに通知するためとGoogle Code Blogには書いてあります。
<blockquote>
<p style="text-align: left;">HTML5 "async" attribute in this part of the snippet. While it creates  the same effect as adding a &lt;script&gt; element to the DOM, it  officially tells browsers that this script can be loaded asynchronously.</p>
<p style="text-align: right;"><a href="http://googlecode.blogspot.com/2009/12/google-analytics-launches-asynchronous.html">Google Code Blog: Google Analytics Launches Async...</a></p>
</blockquote>
まぁ、実際のところどうなん？って感じなので、<a href="http://t32k.me/mol/2010/04/httpwatch/">HTTPWatch</a>(IE6で検証)で、とあるサイトの非同期トラッキングコードの実装の前後を計測したのが以下のウォーターフォールチャートです。

<img class="fig" title="5" src="http://t32k.me/mol/file/2010/05/5.png" alt="" width="470" height="227" />
<em><span style="color: #888888;">&lt;/body&gt;直前に挿入したスタンダードトラッキングコードのチャート</span></em>

<img class="fig" title="6" src="http://t32k.me/mol/file/2010/05/6.png" alt="" width="470" height="226" />
<span style="color: #888888;"><em>&lt;/head&gt;直前に挿入した非同期トラッキングコードのチャート</em></span>

各コンポーネントの読み込み時間のブレもありますが、おおかた上記チャート図のような読み込まれ方をしています。灰色で強調されている部分がga.jsです。最初のチャート図は以前のように非同期ではないトラッキングコードで読み込んでいますので、ページの表示に必要なコンポーネントをすべて読み込んでからga.jsを読み込み、GIFリクエスト（最後のコンポーネント）をしています。

これが次の非同期トラッキングコードのチャートですと、コンポーネントのダウンロードをブロックしないので早い段階で読み込むことができ、GIFリクエスト（最後のコンポーネント）もページのレンダリングの前に完了しています。結果、ページ全体の読み込み時間は短くなっていますね。（上記の例だと200msぐらい）
<h3 id="section03">データの収集・精度の向上</h3>
パフォーマンス面の理由から最下部にしか置けなかったトラッキングコードですが、非同期で読み込むことができるようになったので、ページの上部におけるようになりました。つまり、それだけGoogle Analyticsを作動させるタイミングを早くすることができます。以前まではページが完全に読み込まれない状態でページ遷移した場合などは記録されないってことも想定されましたがその可能性が低くなったということです。
<h4 id="section31">トラッキングコードは&lt;/head&gt;の直前、&lt;body&gt;の直後？</h4>
パフォーマンスを気にすることなく、トラッキングコードは上部に置けるようになったのですが、これどこに置いたらよいの？と疑問があります。ところが、ヘルプの記事や管理画面の注意文によって言っていることがブレていて困りものです。
<blockquote>headセクションの最後ではなくてbodyセクションの最初です。
調べた限りでは、headセクションに記述するとIE6ではJavascriptの動きに問題が発生することがあるようです。
<p style="text-align: right;"><a href="http://www.suzukikenichi.com/blog/google-analytics-asynchronous-tracking-is-now-default/">Google  Analytics非同期トラッキングが標準設定に | 海外SEO情報ブ...</a></p>
</blockquote>
上記のブログではbodyセクションの最初って言ってますけど、それよりも何も「<strong>問題</strong>」ってなによ？って感じで気になったので調べてみました。それを問題にしているところの出典が明記されていないので、よくわかりませんが、たぶんこれが問題じゃないのかなと。
<ul>
	<li><a href="http://www.google.com/support/forum/p/Google+Analytics/thread?tid=5532c8dff3e8aa42&amp;hl=en">Async snippet causes IE6 to close with "operation aborted" - Google Analytics Help</a></li>
</ul>
IE6でなんかパーシングエラーになるそうです。その解決策としてBest Answerになってるのが、BASE要素をホゲホゲするか、HEAD要素に置いたトラキッングコードをBODY要素に置けばいいぜ！って書いてあります。うん、これっぽい。

んで、これ調べてると他にも関係ありそうな記事を見つけたので紹介。
<ul>
	<li><a href="http://www.stevesouders.com/blog/2010/05/11/appendchild-vs-insertbefore/">High Performance Web Sites :: appendChild vs insertBefore </a></li>
</ul>
GoogleでWebパフォーマンスのエバンジェリストしている<a href="http://twitter.com/souders">Steve Souders</a>さんのブログ記事なんですが、Google Analyticsの非同期トラッキングコードの変遷について解説しています。
<pre>var ga = document.createElement('script');
ga.src = ('https:' == document.location.protocol ?
    'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
ga.setAttribute('async', 'true');
document.documentElement.firstChild.appendChild(ga);
<span style="color: #888888;">//2009年12月段階のベータ版のトラッキングコード</span></pre>
--
<pre>var ga = document.createElement('script');
ga.type = 'text/javascript'; ga.async = true;
ga.src = ('https:' == document.location.protocol ?
    'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
var s = document.getElementsByTagName('script')[0];
s.parentNode.insertBefore(ga, s);
<span style="color: #888888;">//2010年の2月の段階のトラッキングコード</span></pre>
どこが変わったのですかね。。。まぁちょいちょい微妙に違うのですが、ここでもっとも重要な変更点はSCRIPT要素をDOMで生成した後、ページに挿入するメソッドを、appendChildからinsertBeforeに変更した点です。

なんでこんなことをしたのかとSteve Souders考えるにjQueryで同じような問題があったので参考にしたのではないかと。
<blockquote>head = document.getElementsByTagName ("head")[0] ||
document.documentElement;
<span style="color: #888888;">// Use insertBefore instead of appendChild to circumvent an IE6 bug.
// This arises when a base node is used (<a href="http://dev.jquery.com/ticket/2709">#2709 </a>and <a href="http://dev.jquery.com/ticket/4378">#4378</a>).</span>
head.insertBefore(script, head.firstChild);</blockquote>
この#2709の問題ってGoogle Analyticsヘルプでの問題と同じじゃね？つまり、insertBeforeメソッドにすることでIE6のバグは治ったのではないかと僕は推測しました。

んで、もうちょっと調べてみると、ドンピシャな質問がヘルプフォーラムで投げられていました。
<ul>
	<li><a href="http://www.google.com/support/forum/p/Google+Analytics/thread?tid=4e634e0982427593&amp;hl=en">Where should Asynchronous code be placed as seen instruction for 2 different places - Google Analytics Help</a></li>
</ul>
<strong>Q. </strong>ヘルプの各記事で&lt;/head&gt;の直前、&lt;body&gt;の直後とトラッキングコードの挿入位置が違ってるけど、どっちやねん？

<strong>A. </strong>旧バージョンは&lt;body&gt;の直後に置くことでバグ回避してたけど、最新バージョンだったらその問題も起きないねん。ヘルプは今直してるとこやさかい、堪忍して。だから、位置は別にどっちでもええで。

みたいなやりとりですね。2010/5/20の回答なのでこれが最新の情報かな。あれ？答え出た？って感じなんですけど、まだ信用できません。このBest answerのBrian Kuhnって誰？と思ったので調べて見ますと、<a href="http://twitter.com/briankuhn">Twitterで発見</a>。ga.js作ってるGoogleのエンジニアさんじゃないっすか！てか、<a href="http://googlecode.blogspot.com/2009/12/google-analytics-launches-asynchronous.html">非同期トラッキングコードリリースの公式ブログ</a>書いてるのこの人じゃないっすか！つか、Twitterでも同じような質問されてるじゃないっすか！
<blockquote>
<p style="text-align: left;">@tgwilson @BigBryC - Nothing changed. There's just a couple lingering pages with the old instructions. We're fixing them. Head is preferred.</p>
<p style="text-align: right;"><a href="http://twitter.com/briankuhn/status/14340466143">http://twitter.com/briankuhn/status/14340466143</a></p>
</blockquote>
Brian... あなたにもっと早く出会えていれば....

まぁ、そんなわけで、BODY要素に置かなければならない理由としてのIE6バグはフィックスされている。んで、非同期なのでどこにコードを置いても大丈夫だけど、HEAD要素に置くのが慣例的だし、Brianさんも好みだそうです。データの収集・精度を考えると少しでも上部に置くほうがベター（&lt;/head&gt;の直前と&lt;body&gt;の直後じゃ、あんまかわらんけどｗ）なんで&lt;/head&gt;の直前で良いのかなと僕は結論づけしました。

それにしても、ヘルプの記事とか修正したら月日記入して欲しいね。。。どっちが最新か分からない＞＜
<h3 id="section04">依存性からくるエラーの除去</h3>
これまで見てきて非同期ってワンダホー♪って思うのですが、そもそもなぜスクリプトファイルが読み込まれると並列ダウンロードがブロックされるのでしょうか？その理由として、開発者としては上部に置いたコードが先に実行されるという前提の上で実装をしています。もし、A.js、B.jsの順番でHTMLファイル内に読み込んで、非同期のためにB.jsの方が早く読み込みが完了されちゃったとします。B.jsの中にはA.jsで定義されたオブジェクトなど使われているので、当然未定義になってエラーが返される、なんてことが考えられます。例えるなら、jquery.js読み込む前に、jquery-plugin.jsが読み込まれては問題なわけですよ。

なので、非同期で読み込む場合はコードの実行順序を考慮する必要性があります。Google Analyticsの非同期トラッキングコードでは、前半部分がそれに対応した部分になっています。
<pre id="line17">  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XXXXX-X']);
  _gaq.push(['_trackPageview']);</pre>
JavaScriptを嗜む程度の自分なのであまり詳しくないですが、このコードを初めて見たとき、なんか見慣れないなと思いました。なんでこうゆう書き方をしているのかなと。<a href="http://googlecode.blogspot.com/2009/12/google-analytics-launches-asynchronous.html">Google Code Blog</a>を読む分には、ga.jsが読み込まれていない状態でvar _gaqにはただの配列が代入されて、そのコマンドが配列中に記録されてキュー待ち状態になる。んで、ga.jsが読み込まれると_gaqはオブジェクトになってキュー待ちのコマンドを実行していくという感じです。

まぁ、よく分かりませんが、とりあえず、コードの実行順序を維持するためにこのような書き方になったということが理解できて良かったです。ということで、ga.jsが読み込まれなかったとしてもただの配列の中に蓄えられるだけなのでエラーになる可能性が低くなったということです。
<h3 id="section05">まとめ</h3>
というわけで、非同期トラッキングコードについて、Webデザイナーの自分が背伸びをして調べたわけですが、ほんっと<a href="http://twitter.com/t32k/status/14137281670">【急募】アクセス解析エンジニア</a>って感じました。だって分かんないもん、JavaScript＞＜　先日の<a href="http://togetter.com/li/23955">a2isummit</a>でも
<h4>「マーケッターに技術を、技術者にマーケティングを」</h4>
と言われていたように、互いの領域について知る必要性があるのかなとひしひし感じています。いやほんと、アクセス解析エンジニアはいいポジションだと思う。絶対チヤホヤされるよｗ
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/487311361X/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51hIDIWHmYL._SL160_.jpg" border="0" alt="ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール" width="125" height="160" /></a></td>
<td valign="top"><a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank">ハイパフォーマンスWebサイト ―高速サイトを実現する14のルール</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
武舎 広幸

オライリージャパン  2008-04-11
売り上げランキング : 14801
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-5.gif" alt="" />

<a href="http://www.amazon.co.jp/%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E9%AB%98%E9%80%9F%E3%82%B5%E3%82%A4%E3%83%88%E3%82%92%E5%AE%9F%E7%8F%BE%E3%81%99%E3%82%8B14%E3%81%AE%E3%83%AB%E3%83%BC%E3%83%AB-Steve-Souders/dp/487311361X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D487311361X" target="_blank">Amazonで詳しく見る</a> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></td>
</tr>
</tbody>
</table>
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51apDotzVxL._SL160_.jpg" border="0" alt="続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス" width="125" height="160" /></a></td>
<td valign="top"><a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462" target="_blank">続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
武舎 広幸

オライリージャパン  2010-04-10
売り上げランキング : 33600
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-3-0.gif" alt="" />

<a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462" target="_blank">Amazonで詳しく見る</a> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></td>
</tr>
</tbody>
</table>
