---
date: 2012-08-08
title: パフォーマンスからみるSass/Compass 番外編：MSは青かった
categories: 
    - css
---
2回も続いてないのにまさかの番外編！ここぞ変化球！キエル消える魔球！！

ってことで、最近Androidの相手ばかりしていて、「IE... そんな女もいたよね」って感じでしたが、ちょっとハマったので忘備録。グラデーションを使ったデザインをCSSで再現しようとした話。ということでCSSグラデーションのスニペットを<a href="http://www.colorzilla.com/gradient-editor/">Ultimate CSS Gradient Generator</a>で吐き出してみたんですわ。
<pre><code>/* CSS */
.gradient {
 background: -moz-linear-gradient(top, #000 0%, #595959 100%);
 background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#000), color-stop(100%,#595959));
 background: -webkit-linear-gradient(top, #000 0%,#595959 100%);
 background: -o-linear-gradient(top, #000 0%,#595959 100%);
 background: -ms-linear-gradient(top, #000 0%,#595959 100%);
 background: linear-gradient(to bottom, #000 0%,#595959 100%);
 filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#000', endColorstr='#595959',GradientType=0 );
}</code></pre>
<!--more-->

まぁ、こんな感じなのができますわな。で、意気揚々とIEでチェックしてみたらグラデーションが青かったんですよ！黒色のグラデーションが青かったんですよ！びっくりデスヨ！

同僚の<a href="https://twitter.com/hiloki/">@hiloki</a>さん曰く、どうやら僕が<em>startColorstr</em>の部分のHEXカラーを#000000ではなく、#000であとで修正したらからイケなかったらしいです。ちゃんと6バイトで記述したらイケました。どうやらこうゆうことらしいですよ↓
<blockquote>IE does recognize hex colors, but not the kind you're using. Only those with 6 hexadecimals (#RRGGBB) or 8 hexadecimals (#AARRGGBB; only works in the gradient filter!) will work. It will also accept named colors.
<p style="text-align: right;"><a href="http://stackoverflow.com/questions/4737477/why-does-this-css-gradient-show-up-with-the-wrong-colours-in-ie-7">Why does this CSS gradient show up with the wrong colours in IE 7? - Stack Overflow</a></p>
</blockquote>
短縮コード理解できないってどんだけ◯◯なんだよ！ったく！そんな！#000000とか見たら#000にしたくなっちゃうだろ！それが人の性ってもんでしょうに！って同僚に言ったら、そうでもないらしいですね....

まぁ今回は僕の手癖が悪かったからしょうが無いとしても、縮小化ツールによっては短縮しちゃうものもあるでしょ？というか<a href="http://sass-lang.com/docs/yardoc/file.SASS_CHANGELOG.html#_style">Sassの:compressedにしたら短縮</a>してしまうやん（v3.1.20はしなかったけど）どーしたらいいですかね...
<h2>Compass: ie-hex-str()</h2>
まぁ<a href="https://github.com/nex3/sass/issues/280">同じような問題にぶち当たった人</a>も多く、回避策としてはどうやらie-hex-str()ってCompassの関数を使えば良いとのこと。
<ul>
	<li><a href="http://kuroir.com/post/14557689480/compass-ie-hex-str  ">Compass: ie-hex-str() | Mario "Kuroir" Ricalde</a></li>
</ul>
これを使うと、#000やblackと指定しても
<pre><code>// SASS
@import "compass";
.ms-gradient {
	filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#{ie-hex-str(#000)}', endColorstr='#595959',GradientType=0 );
}</code></pre>
このようにコンパイルされます。
<pre><code>/* CSS */
.ms-gradient {
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#FF000000', endColorstr='#595959',GradientType=0 );
}</code></pre>
8バイトになってるのは、#AARRGGBBってことで、最初の2バイトはアルファ値でFFだから不透明度100%ってことですね。これはIEさん認識できるらしいです。いやしかしですよ、IEごときで、なにゆえCompassをインストールしなきゃならんのか！面倒くさい！ってことで、ブライトネス1%上げて短縮されないように#010101にしました。

そもそも画像でやれよ！って言うのは無しね！HTTPリクエスト減らしてなんぼだかんね！

んで、最初のバグに戻るけどなんで黒いのグラデーションが青色になったのかというと、startColorが#000で認識できなかったので、Default Color が青だからそれが適用されたんだね！
<blockquote>
<p style="text-align: left;">Default. Blue.</p>
<p style="text-align: right;"><a href="http://msdn.microsoft.com/en-us/library/ms532930(v=VS.85).aspx">StartColorStr Property (Gradient) </a></p>
</blockquote>

なるほど！バイバイ！
