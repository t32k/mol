---
layout: post
title: データURIスキーム
categories:
- performance
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '24642'
---
今回の記事の主題はデータURIスキームとはなんぞいねってことなんですが、簡単に言いますと、このスキームを使うとサーバにリクエストすることなく、ページ内のコードに画像を埋め込むことができるという話です。スキームといえば、このほかにもhttp:、ftp:、mailto:なんてものがありますね。

ウェブパフォーマンスにとって高コストなものといえば、HTTPリクエストですから、それを使わず画像を表示できるということはこのスキームを使う最大のメリットと言えるでしょう。

<!--more-->

てなわけで、実際にどんなものか見てみましょう。例えば、隣にあるこのフィードアイコン<img src="http://www.feedburner.com/fb/images/pub/feed-icon16x16.png" alt="" /> はHTMLソースの中ではこんな感じでに記述されています。
<pre><code>&lt;img src="http://www.feedburner.com/fb/images/pub/feed-icon16x16.png" /&gt;</code></pre>
これをデータURIスキームを使って表現するとこんな感じになります↓
<pre><code>&lt;img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAKOSURBVHjadJNNSFRRGIbfc+6dO6OOOplDykSZaRCtnKRc+ANRUBFEm0gicxG0bGoVhERRYIvIjRAtW+UmW5QQQS6qRWQSWJRaUcjkT0LiVWfm/pzTd869M5LShe+eufC973m+n2Fj55KJymTt9ZgVy3AGMHoxvvEs/qZgDL4AlhbsAfv34g1TiRPxRMZbWwU3GQzO9clNhGcYBpkY4UlGiWRd5scnMvx5tUWano9IMoXy1pOUBPgz4xC/xv8r1hSexNKiB1Nhq6RIbQoVhy6i+MiCDffDEPyJITBvZZPYLwiQFFzVZ0Q45Moc8q8fwP34FGJ5FixaCevgBZT1DMNs7Nok9iikL8GyfWkZ3VgvhbljP6yOy2BbmzWR/+o2vM/PSmLfkchTaAIlsHa1ourSS5Sfvg8r3Q38mYb7+DzE9Ig2MDquAan2kth3AgKu0JSBapLCNranEWnPIHp2GDzZDEE3+1OBiXW4D4LHtViZCB/rBHJuHPmHp+CO3oK0Zyk7DvP4IGR1EwrPb673JX0mELslgvVRYW0O8usIvCe9AboyOdIPn1Ug9+Kupihr69ZiZSJFsYRwztbRO4icGARv6IT3ZkCTsKp68J2dyE2MQuZtsFgllbZHTyMsAVqsaldCVt8CtvsYPHsZzvtH+tZIc5e+sfBtLOhFYytRFAlYuGGED2clGNn8lO62m53U37y6XmM7M8E3onEIIpCSLp/vPyC31Bp6SUSsjmIbnO9jpVEZqbROzn15F5RDZs5CFs58FmaNBTZ5Ze+9hn11Genl/1mS0qjChumaCVvo2iViNXHkuD1g9Daxt7lVEQPMNpcSdah1pQb5kqho4yVXQc2iacHiMMpNFPia/jv/FWAAUTVTOunExzkAAAAASUVORK5CYII=" /&gt;</code></pre>
なんかわかりませんが、わっさー長くなりましたねw これは画像のバイナリデータをBase64で表現したものになります。はい、よくわからんですね... バイナリというのは<a href="http://e-words.jp/w/E38390E382A4E3838AE383AA.html">文字データ以外のデータ形式全般のこと</a>と書かれていますが、映画のマトリックスに出てくる数字の羅列みたいな感じを個人的には想像しています。まぁ、それをBase64ってゆう形式で表現し直しているって感じでしょうか。Base64に関してはこちらを参照↓
<blockquote>Base64は、データを64種類の印字可能な英数字のみを用いて、それ以外の文字を扱うことの出来ない通信環境にてマルチバイト文字やバイナリデータを扱うためのエンコード方式である。
<a href="http://ja.wikipedia.org/wiki/Base64">Base64 - Wikipedia</a></blockquote>
そういうわけで、より大きな画像をBase64に変換すればそれだけ結果も長く、容量が大きいものになります。例えば、先程のアイコンよりも大きいこのCSS Niteのバナーを変換してみましょう。
<img src="http://t32k.me/mol/wp-content/uploads/2010/03/lp9.png" alt="" />
<pre><code>&lt;img src="data:image/png;base64,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" /&gt;</code></pre>
ちょっとここでは分かりにくいですが、コピペしてテキストエディタで表示してみると差は歴然でしょう。

そんなわけで、データURIスキームの書式はこんな感じです。
<pre><code>data:[メディアタイプ][;base64],データ</code></pre>
まぁ変換ツールを使えば一発ですw
<h4>オンライン変換ツール</h4>
<ul>
	<li><a href="http://websemantics.co.uk/online_tools/image_to_data_uri_convertor/">Image To Data URI  Convertor - webSemantics</a></li>
	<li><a href="http://sveinbjorn.org/dataurlmaker">DataURLMaker | Sveinbjorn  Thordarson</a></li>
	<li><a href="http://www.scalora.org/projects/uriencoder/">data: URI image  encoder</a></li>
	<li><a href="http://software.hixie.ch/utilities/cgi/data/data">The data:  URI  kitchen</a></li>
</ul>
PHPが使える環境ならば、 file_get_contents関数ってのを使うと、画像修正の度にツールで変換することもなくなります。
<pre><code><span style="color: #888888;">&lt;img src="data:image/png;base64,</span>&lt;?php echo base64_encode(file_get_contents("../images/feed-icon16x16.png")) ?&gt;<span style="color: #888888;">"&gt;</span></code></pre>
<h3>容量の肥大化</h3>
ただ、問題点もちらほらあります。Base64で表現しますと、元のバイナリデータより30~40%大きくなってしまうことです。

<a href="http://t32k.me/mol/wp-content/uploads/2010/04/base64.png"><img class="fig" title="base64" src="http://t32k.me/mol/wp-content/uploads/2010/04/base64.png" alt="" width="470" height="270" /></a>
<em><span style="color: #808080;">Image To Data URI Convertor - webSemantics より</span></em>

上記のように、先程のフィードアイコンも元が764バイトに対して、Base64にエンコードした結果は1020バイトと約36%の増加となっています。というか、そもそもそのような長いコードをHTML内に記述すれば、フィードアイコンのある全てのページでHTML容量が増加してしまうことが考えられます。

そのような時は、外部CSSファイル内に記述し、キャッシュを効かすのがよいかなと考えます。こんな具合に↓
<pre><code>.hoge {
　width: 16px;　height: 16px;
　background-repeat: no-repeat;
　background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAKOSURBVHjadJNNSFRRGIbfc+6dO6OOOplDykSZaRCtnKRc+ANRUBFEm0gicxG0bGoVhERRYIvIjRAtW+UmW5QQQS6qRWQSWJRaUcjkT0LiVWfm/pzTd869M5LShe+eufC973m+n2Fj55KJymTt9ZgVy3AGMHoxvvEs/qZgDL4AlhbsAfv34g1TiRPxRMZbWwU3GQzO9clNhGcYBpkY4UlGiWRd5scnMvx5tUWano9IMoXy1pOUBPgz4xC/xv8r1hSexNKiB1Nhq6RIbQoVhy6i+MiCDffDEPyJITBvZZPYLwiQFFzVZ0Q45Moc8q8fwP34FGJ5FixaCevgBZT1DMNs7Nok9iikL8GyfWkZ3VgvhbljP6yOy2BbmzWR/+o2vM/PSmLfkchTaAIlsHa1ourSS5Sfvg8r3Q38mYb7+DzE9Ig2MDquAan2kth3AgKu0JSBapLCNranEWnPIHp2GDzZDEE3+1OBiXW4D4LHtViZCB/rBHJuHPmHp+CO3oK0Zyk7DvP4IGR1EwrPb673JX0mELslgvVRYW0O8usIvCe9AboyOdIPn1Ug9+Kupihr69ZiZSJFsYRwztbRO4icGARv6IT3ZkCTsKp68J2dyE2MQuZtsFgllbZHTyMsAVqsaldCVt8CtvsYPHsZzvtH+tZIc5e+sfBtLOhFYytRFAlYuGGED2clGNn8lO62m53U37y6XmM7M8E3onEIIpCSLp/vPyC31Bp6SUSsjmIbnO9jpVEZqbROzn15F5RDZs5CFs58FmaNBTZ5Ze+9hn11Genl/1mS0qjChumaCVvo2iViNXHkuD1g9Daxt7lVEQPMNpcSdah1pQb5kqho4yVXQc2iacHiMMpNFPia/jv/FWAAUTVTOunExzkAAAAASUVORK5CYII=);
}</code></pre>
さらに欲をいえば、肥大化したCSSファイルをgzip圧縮すれば、Base64で増加した分など微々たるものと言えるでしょう。

とはいえ、<a href="http://www.ietf.org/rfc/rfc2397">RFC2397</a> (<a href="http://www.darts.jp/reference/rfc/rfc2397-jp.txt">邦訳</a>)では、一応1024バイトまでと書いてあるし、Operaも4100バイトまでとのことなのでデータURIを適用する画像はアイコンなどの小さな画像に止めたほうが良いでしょう。
<h4>対応ブラウザ</h4>
<ul>
	<li>Firefox2+ (100KBまで)</li>
	<li>Safari</li>
	<li>Chrome</li>
	<li>Opera7.2+ (4100Bまで)</li>
	<li>IE8 (32KBまで)</li>
</ul>
そういうわけで、長々とデータURIについて説明してきたわけだけど、これって<strong>IE5-7が対応してない</strong>んですよね...orz で、これらのブラウザにはどう対処しましょうかと考えたところ、JavaScriptで適用するというやり方もあるみたいだけど、なんだか難しいね...
<ul>
	<li><a href="http://www.yomotsu.net/lab/javascripts/ie6_data-cheme">IE 7  以下で data スキームを URI 利用する | ヨモツネット</a></li>
	<li><a href="http://d.hatena.ne.jp/uupaa/20080904/1220462674">IE5〜IE7でも、 RFC2397(Dataスキーム, DataURI)を使えるようにした! - latest log</a></li>
</ul>
単純にCSSハックでIE7以下には通常の画像を読み込ませるので良いかなと<span style="text-decoration: line-through;">あきらめたり</span>考えたり...
<pre><code>.hoge {
　width: 16px;　height: 16px;
　background-repeat: no-repeat;
　background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAABGdBTUEAAK/INwWK6QAAABl0RVh0U29mdHdhcmUAQWRvYmUgSW1hZ2VSZWFkeXHJZTwAAAKOSURBVHjadJNNSFRRGIbfc+6dO6OOOplDykSZaRCtnKRc+ANRUBFEm0gicxG0bGoVhERRYIvIjRAtW+UmW5QQQS6qRWQSWJRaUcjkT0LiVWfm/pzTd869M5LShe+eufC973m+n2Fj55KJymTt9ZgVy3AGMHoxvvEs/qZgDL4AlhbsAfv34g1TiRPxRMZbWwU3GQzO9clNhGcYBpkY4UlGiWRd5scnMvx5tUWano9IMoXy1pOUBPgz4xC/xv8r1hSexNKiB1Nhq6RIbQoVhy6i+MiCDffDEPyJITBvZZPYLwiQFFzVZ0Q45Moc8q8fwP34FGJ5FixaCevgBZT1DMNs7Nok9iikL8GyfWkZ3VgvhbljP6yOy2BbmzWR/+o2vM/PSmLfkchTaAIlsHa1ourSS5Sfvg8r3Q38mYb7+DzE9Ig2MDquAan2kth3AgKu0JSBapLCNranEWnPIHp2GDzZDEE3+1OBiXW4D4LHtViZCB/rBHJuHPmHp+CO3oK0Zyk7DvP4IGR1EwrPb673JX0mELslgvVRYW0O8usIvCe9AboyOdIPn1Ug9+Kupihr69ZiZSJFsYRwztbRO4icGARv6IT3ZkCTsKp68J2dyE2MQuZtsFgllbZHTyMsAVqsaldCVt8CtvsYPHsZzvtH+tZIc5e+sfBtLOhFYytRFAlYuGGED2clGNn8lO62m53U37y6XmM7M8E3onEIIpCSLp/vPyC31Bp6SUSsjmIbnO9jpVEZqbROzn15F5RDZs5CFs58FmaNBTZ5Ze+9hn11Genl/1mS0qjChumaCVvo2iViNXHkuD1g9Daxt7lVEQPMNpcSdah1pQb5kqho4yVXQc2iacHiMMpNFPia/jv/FWAAUTVTOunExzkAAAAASUVORK5CYII=);
<span style="color: #888888;">  /* IE7 and below */  </span>
　*background-image: url(http://www.feedburner.com/fb/images/pub/feed-icon16x16.png);
}</code></pre>
まぁ、iPhone用サイトや、Firefoxのアドオンで使う画像など限定的な環境ならば全然使えると思うので試してはどうでしょうか。
<h3>参考サイト</h3>
<ul>
	<li><a href="http://www.websiteoptimization.com/speed/tweak/inline-images/">Inline Images with Data URLs - embed graphics inline with data uri scheme</a></li>
	<li><a href="http://www.nczonline.net/blog/2009/10/27/data-uris-explained/">Data URIs explained | NCZOnline</a></li>
	<li><a href="http://en.wikipedia.org/wiki/Data:_URI_scheme">data URI scheme - Wikipedia, the free encyclopedia</a></li>
</ul>
