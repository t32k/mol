---
date: 2013-08-22
title: HTTPリクエストを減らすために【DataURI編】遅延ロードでレンダリングブロックを回避
categories:
- performance
---
このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっております。
<ul>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-overview/">【序章】HTTPリクエストは甘え</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-css-sprite/">【CSS Sprite編】スプライト地獄からの解放</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-webfont/">【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ</a></li>
	<li><strong>【DataURI編】遅延ロードでレンダリングブロックを回避</strong></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-one-second/">【終章】我々には1000msの猶予しか残されていない</a></li>
</ul>
4日目は、本ブログでも何回か話題にしているインライン画像についてです。
<ul>
	<li><a href="http://t32k.me/mol/log/data-uri-scheme/">データURIスキーム</a></li>
	<li><a href="http://t32k.me/mol/log/sprite-image-vs-inline-image/">CSS Sprite画像はDataURI画像にすべきか？ </a></li>
</ul>
以前の記事で私は以下のように述べましたが、これはいやらしい表現です。

> DataURIの画像は、通常の画像に比べて6倍遅いとかゆう記事もあります
<a href="http://www.mobify.com/blog/data-uris-are-slow-on-mobile/">http://www.mobify.com/blog/data-uris-are-slow-on-mobile/</a>

こうゆう、『xxx倍高速化』、『xxx倍遅い』と言った表現は、わかりやすい反面、本質を見失ってしまう危険性があります。例えば、10秒が1秒になるのも、1秒が0.1秒になるのもどちらも同じく『10倍速くなった』と表現できます。

似たような例として、毎年のようにブラウザのJavaScriptエンジンがx倍高速化した！といったようなニュースを一度は聞いてるかと思いますが、実体感としては、それほど速くなっていないように感じます。これも結局はブラウザのJS処理というのは何msという単位（あるいはもっと細かい単位かもしれません）での改善なので、そのような文脈での『x倍』というのは、実際は0.数ms程度の違いしかないのかもしれません。

このように『x倍速くなった・遅くなった』という表現をしているときは、注意が必要です（大人はみんな騙そうとしてきます）！どうゆう文脈での何倍なのか、ちゃんと確認してみましょう。
> In the first condition, the src image attribute was specified to an image location known to be in the browser cache. This is called the binary condition.In the second condition, the src image attribute was specified to a pre- fetched data URI of the same image as in the first condition. This is called the data URI condition.Both conditions used the same image, a 17.8kB PNG. In both conditions, the same image was materialized 5 times. Materialization completion was measured by using the "load" event of the image object.When the load event for all 5 images fired, the test was marked as “complete” and results were recorded.

<a href="http://www.mobify.com/blog/data-uris-are-slow-on-mobile/">http://www.mobify.com/blog/data-uris-are-slow-on-mobile/</a>

件のテスト条件は上記のとおりです。まずテストに使われる画像ですが17.8KBのPNGって結構でかいですよ。。ちょっとしたアイコンどころじゃないですよね？そもそも、その大きさの画像でテストする事自体どうなんだって気もします。

次に、画像のloadイベントが発生した時を完了と見なしています、そして通常の画像パスでの読み込みはブラウザキャッシュがある状態としています。

<a href="http://www.mobify.com/blog/data-uris-are-slow-on-mobile/"><img class="aligncenter size-large wp-image-5194" alt="image_0" src="/static/blog/2013/08/image_0.png" width="540" height="405" /></a>

で、結果が上記のグラフです、Android2系はほっといてAndroid4系、iOS6の差を見てみるとだいたい100ms ~ 150msくらいです。この差をどう捉えるかですね。実際のケースで考えれば、17.6KBの画像を3G回線でHTTPリクエストすればラウンドトリップだけで200ms以上はかかるでしょうし、また画像リクエストで同時接続数の1つを失ってしまい、後続のリソースのブロッキングをする可能性も出てくると考えれば、 150msくらい許容範囲ではないでしょうか？

許容範囲であるかないかは、各々の状況というのがあると思うので各人で判断してもられば良いのですが、少なくとも『DataURI？あ、6倍遅いからダメ！』って短絡的に片付けるの良くないかと思います。

---

では、インライン画像ってどうゆうときに使うのでしょうか？使わざるを得ないのでしょうか？

HTTPリクエストを減らすという観点から言えば、大抵のものは前々回で話したようにCSSスプライトにしてしまえばよいのです、また、単純な図形・アイコンでカラーバリエーションがあるようなものであればWebフォントにすればよいでしょう。

しかし世の中そんなに甘くありません。下記のようなものはCSSスプライトできません。
<ul>
	<li><span class="code">border-image</span></li>
	<li><span class="code">background-image</span>(縦横リピート)</li>
</ul>
まぁ、こうゆうのですよね。

<img class="aligncenter size-full wp-image-5196" alt="ss" src="/static/blog/2013/08/ss1.png" width="556" height="154" />

ボタンの文字が決め打ちだったり、幅が決まってたりする場合は単純にその画像をスプライトすればよいのですが、そうでもない場合は<span class="code">border-image</span>にしたほうが、都合が良いです。もちろん左端と右端と中央で画像を分けて各背景画像で対応するのもいいけど、やっぱり<span class="code">border-image</span>がなにかと都合が良いです。

あと背景画像は、X軸、Y軸リピートならなんとかできるけど、縦横リピートになるとCSSスプライトではどうしようもできないです。でも、全体の背景にテクスチャ画像を貼るのもよくある表現です。

ということで、DataURI使いたいと思います。インライン画像を考える上で重要なのは以下の3つです。
<ul>
	<li>インライン画像はリクエストを発生させない</li>
	<li>だがファイルサイズが重くなる</li>
	<li>CSSファイルに含めるとレンダリングブロックに繋がる可能性あり</li>
</ul>
ちなみにCompassだと下記のような関数を使うとbase64エンコードしてくれます。

```css
.border{
	border-image: inline-image("/path/to/border-image.png");
}
```

<ul>
	<li><a href="http://compass-style.org/reference/compass/helpers/inline-data/">Compass Inline Data Helpers | Compass Documentation</a></li>
</ul>
では、3つめのインライン画像をCSSファイルに含んだ時のレンダリングブロック回避について考えて行きましょう。

それで、通常のスタイルとインライン画像の指定をしたCSSを分けてみました。

```html
<link rel="stylesheet" href="css/app.css">
<link rel="stylesheet" href="css/base64.css">
```

<ul>
	<li><a href="http://t32k.github.io/test/include-datauri/block.html">Block : Include DataURI Source </a></li>
</ul>
感覚的には、こういったマークアップをしてしまいがちですが、これでも結局、インライン画像を含んだ重いbase64.cssが読み込まれるまでレンダリングが始まりません。

```html
<script>
(function(d){
  var c = d.createElement('link');
  c.rel = 'stylesheet';
  c.href = 'css/base64.css';
  var s = d.getElementsByTagName('script')[0];
  s.parentNode.insertBefore(c, s);
})(document);
</script>
```

<ul>
	<li><a href="http://t32k.github.io/test/include-datauri/">Defer : Include DataURI Source </a></li>
</ul>
ですので、遅延読み込みしたのが上記です。

<a href="http://www.webpagetest.org/video/compare.php?tests=130815_WY_66F,130815_9R_66G"><img class="aligncenter size-full wp-image-5198" alt="ss1" src="/static/blog/2013/08/ss11.png" width="840" height="365" /></a>

<a href="http://www.webpagetest.org/video/compare.php?tests=130815_WY_66F,130815_9R_66G">WebPagetest - Visual Comparison</a>

BlockとDeferをVideo Comparisonした結果が上記です。Video Comparisonのテスト条件上、Dulles, VA - IE 9の環境でしかテストできませんので、border-imageは対応していないため表示されていません、あしからず。遅延読み込みしたのが、0.2秒でレンダリングが始まっているのに対して、通常読み込みは0.5秒で完成しています。

差を分かりやすくするために、base64.cssにはコメントアウトした長ーい文字列を記述しファイルサイズを増加させています。
<ul>
	<li><a href="http://www.webpagetest.org/result/130815_HC_66Z/">Defer : WebPagetest Test Result - Tokyo</a></li>
	<li><a href="http://www.webpagetest.org/result/130817_22_D68/">Block : WebPagetest Test Result - Tokyo</a></li>
</ul>
Chrome,3G回線でテストした詳細な結果でも、遅延読み込みしている方の<strong>Start Renderは1.786s</strong>に対して、通常読み込みは<strong>3.564s</strong>とかなり違う結果になりました。もちろん遅延読み込みしている分、最終的なFully Loadedは遅くなります。

以上のようにすれば、懸念していたインライン画像を含む重いCSSによるレンダリングブロックを回避できるかと思います。

遅延読み込みが銀の弾丸かと言えば、とうてい、そんな上等なものでありません。苦肉の策感がにじみ出ています。今回のようなborder-imageを使ったボタンも高さや幅を限定してパターン数を絞ればCSSスプライトでまかなえることも可能ですし、背景画像もno-repeatにできればCSSスプライトで収まる場合もあります。そのようなことを考慮した上で、はじめて遅延読み込みするといった手段を採用すべきです。

なにごともバランスが重要です。
