---
date: 2013-08-22
title: HTTPリクエストを減らすために【DataURI編】遅延ロードでレンダリングブロックを回避
subtitle: CSS Sprite Automation.
categories: performance
excerpt: 4日目は、Data URI(インライン画像)ついて説明します。
ogimage: http://t32k.me/static/blog/2013/08/requests.gif
---

このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっている。

+ [【序章】HTTPリクエストは甘え](/mol/log/reduce-http-requests-overview/)
+ [【CSS Sprite編】スプライト地獄からの解放](/mol/log/reduce-http-requests-css-sprite/)
+ [【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ](/mol/log/reduce-http-requests-webfont/)
+ __【DataURI編】遅延ロードでレンダリングブロックを回避__
+ [【終章】我々には1000msの猶予しか残されていない](/mol/log/reduce-http-requests-one-second/)

4日目は、本ブログでも何回か話題にしているインライン画像についてです。

+ [データURIスキーム](/mol/log/data-uri-scheme/)
+ [CSS Sprite画像はDataURI画像にすべきか？](/mol/log/sprite-image-vs-inline-image/)

## Data URI画像のテスト結果について

以前の記事で私は以下のように述べましたが、これはいやらしい表現だ。

> DataURIの画像は、通常の画像に比べて6倍遅いとかゆう[記事](http://www.mobify.com/blog/data-uris-are-slow-on-mobile/)もある

このような『xxx倍高速化』、『xxx倍遅い』と言った表現は、わかりやすい反面、本質を見失ってしまう危険性がある。例えば、__10秒が1秒になるのも、1秒が0.1秒になるのもどちらも同じく『10倍速くなった』と表現__できる。

似たような例として、毎年のようにブラウザのJavaScriptエンジンがx倍高速化した！といったようなニュースを一度は聞いてるかと思うが、実体感としては、それほど速くなっていないように感じる。これも結局はブラウザのJS処理なんてものは何msという単位（あるいはもっと細かい単位かもしれません）での改善なので、そのような文脈での『x倍』というのは、実際は0.数ms程度の違いしかないということだろう。

このように『x倍速くなった・遅くなった』という表現をしているときは、注意が必要だ！（大人はみんな騙そうとしてくる）どうゆう文脈での何倍なのか、ちゃんと確認する必要がある。

> In the first condition, the src image attribute was specified to an image location known to be in the browser cache. This is called the binary condition.In the second condition, the src image attribute was specified to a pre- fetched data URI of the same image as in the first condition. This is called the data URI condition.Both conditions used the same image, a 17.8kB PNG. In both conditions, the same image was materialized 5 times. Materialization completion was measured by using the “load” event of the image object.When the load event for all 5 images fired, the test was marked as “complete” and results were recorded.

+ [On Mobile, Data URIs are 6x Slower than Source Linking | Mobify](http://www.mobify.com/blog/data-uris-are-slow-on-mobile/)

件のテスト条件は上記のとおりだ。まずテストに使われる画像だが17.8KBのPNGって結構でかい。。ちょっとしたアイコンどころじゃないよね？そもそも、その大きさの画像でテストする事自体どうなんだって気もする。

次に、画像のloadイベントが発生した時を完了と見なしている、そして通常の画像パスでの読み込みはブラウザキャッシュがある状態としている。

![Binary vs Data URI](http://t32k.me/static/blog/2013/08/image_0.png)

結果が上記のグラフ、Android2系はほっといてAndroid4系、iOS6の差を見てみるとだいたい100ms ~ 150msくらいだ。この差をどう捉えるかがネックだ。実際のケースで考えれば、17.6KBの画像を3G回線でHTTPリクエストすればラウンドトリップだけで200ms以上はかかるだろうし、また画像リクエストで同時接続数の1つを失ってしまい、後続のリソースのブロッキングをする可能性も出てくると考えれば、 150msくらい許容範囲ではないだろうか？

許容範囲であるかないかは、各々の状況というのがあると思うので各人で判断してもられば良いのだが、少なくとも『DataURI？あ、6倍遅いからダメ！』って短絡的に片付けるの良くない。


## Data URI画像の使いどころ

Data URI（インライン）画像ってどうゆうときに使うのだろうか？使わざるを得ないのだろうか？

HTTPリクエストを減らすという観点から言えば、大抵のものは前々回で話したようにCSSスプライトにしてしまえばよい。また単純な図形・アイコンでカラーバリエーションがあるようなものであればWebフォントにすればよい。

しかし世の中そんなに甘くない。下記のようなものはCSSスプライトできない。

+ border-image
+ background-image(縦横リピート)

まぁ、こうゆうのだろうね。

![サンプル](http://t32k.me/static/blog/2013/08/ss1.png)

ボタンの文字が決め打ちだったり、幅が決まってたりする場合は、単純にその画像をスプライトすればよい。だが、そうでもない場合は`border-image`にしたほうが、都合がよい。もちろん左端と右端と中央で画像を分けて各背景画像で対応するのもいいけど、やっぱり`border-image`がなにかと都合がよい。

あと背景画像は、X軸もしくはY軸リピートならなんとかできるが、縦横リピートになるとCSSスプライトではどうしようもできない。しかし、全体の背景にテクスチャ画像を貼るのもよくある表現だ。

ということで、DataURI使いたいと思います。インライン画像を考える上で重要なのは以下の3つ。

+ インライン画像はリクエストを発生させない
+ ファイルサイズが重くなる
+ スタイルシートに含めるとレンダリングブロックに繋がる

ちなみにCompassだと[下記のような関数](http://compass-style.org/reference/compass/helpers/inline-data/)を使うとbase64エンコードしてくれます。

```sass
.border{
    border-image: inline-image("/path/to/border-image.png");
}
```

では、3つめのインライン画像をCSSファイルに含んだ時のレンダリングブロック回避について考えていく。通常のスタイルとインライン画像の指定をしたCSSを分けてみることにする。

```html
<link rel="stylesheet" href="css/app.css">
<link rel="stylesheet" href="css/base64.css">
```

+ [Block : Include DataURI Source](https://dl.dropboxusercontent.com/u/356242/test/include-datauri/block.html)

感覚的には、こういったマークアップをしてしまいがちだが、これでも結局、インライン画像を含んだ重いbase64.cssが読み込まれるまでレンダリングが始まらない。

```javascript
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
+ [Defer : Include DataURI Source](https://dl.dropboxusercontent.com/u/356242/test/include-datauri/index.html)

遅延読み込みしたのが上記。

![](http://t32k.me/static/blog/2013/08/ss11.png)

+ [WebPagetest - Visual Comparison](http://www.webpagetest.org/video/compare.php?tests=130815_WY_66F,130815_9R_66G)

BlockとDeferをVideo Comparisonした結果が上記。Video Comparisonのテスト仕様上、Dulles, VA - IE 9の環境でしかテストできない、それゆえborder-imageが対応していない。遅延読み込みしたのが、0.2秒でレンダリングが始まっているのに対して、通常読み込みは0.5秒で完成している。

差を分かりやすくするために、base64.cssにはコメントアウトした長ーい文字列を記述し意図的にファイルサイズを増加させている。

+ [Defer : WebPagetest Test Result - Tokyo](http://www.webpagetest.org/result/130815_HC_66Z/)
+ [Block : WebPagetest Test Result - Tokyo](http://www.webpagetest.org/result/130817_22_D68/)

Chrome・3G回線でテストした詳細な結果でも、遅延読み込みしている方のStart Renderは1.786sに対して、通常読み込みは3.564sとかなり違う結果になった。もちろん遅延読み込みしている分、最終的なFully Loadedは遅くなる。

以上のように、懸念していたインライン画像を含む重いCSSによるレンダリングブロックを回避できるかと思うが、遅延読み込みが銀の弾丸かと言われれば、とうてい、そんな上等なものでない。苦肉の策感がにじみ出ている。

今回のような`border-image`を使ったボタンも高さや幅を限定してパターン数を絞ればCSSスプライトでまかなえることも可能だし、背景画像も`no-repeat`にできればCSSスプライトで収まる場合もある。そのようなことを考慮した上で、はじめて遅延読み込みするといった手段を採用すべきであろう。

なにごともバランスが重要だ。

