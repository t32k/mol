---
layout: post
title: HTTPリクエストを減らすために【CSS Sprite編】スプライト地獄からの解放
categories:
- performance
tags:
- maple
status: publish
type: post
published: true
excerpt: "このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっております。"
author:
  name: Koji Ishimoto
  twitter: t32k
  gplus: 104886596569728254273 
  bio: Front-end Developer
  image: t32k.png
---
このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっております。
<ul>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-overview/">【序章】HTTPリクエストは甘え</a></li>
	<li><strong>【CSS Sprite編】スプライト地獄からの解放</strong></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-webfont/">【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-datauri/">【DataURI編】遅延ロードでレンダリングブロックを回避</a></li>
	<li><a href="http://t32k.me/mol/log/reduce-http-requests-one-second/">【終章】我々には1000msの猶予しか残されていない</a></li>
</ul>
2日目は、HTTPリクエストを減らす最もポピュラーな手法、CSSスプライトについて説明します。

まずは動画をご覧頂きましょう。

<iframe src="//www.youtube.com/embed/s__XwfwxMW8" height="360" width="640" allowfullscreen="" frameborder="0"></iframe>
<ul>
	<li><a href="http://www.webpagetest.org/result/130816_VR_9E8/">img要素読み込み | WebPagetest Test Result</a></li>
	<li><a href="http://www.webpagetest.org/result/130816_J6_9EG/">CSS Sprite読み込み | WebPagetest Test Result</a></li>
</ul>
左が30個のアイコン画像をひとつ、ひとつimg要素として読み込んでいます。右は１つの背景画像（CSSスプライト）として読み込んでいます。この場合、表示完了までの差はCSSスプライトのほうが圧倒的に速いです。

<img class="aligncenter size-full wp-image-5249" alt="waterfall" src="/static/blog/2013/08/waterfall.png" width="885" height="552" />

これは前回のHTTPリクエストの仕組みを理解していれば当然のことといえます。つまり、ホスト名ごとの同時接続数やRTTが関係しています。上記のimg画像読み込みのウォーターフォールチャートを確認してみれば一目瞭然です。CSSスプライトすることで一つの画像ファイルサイズは重くなりますが、この場合、重要なのは<strong>Receiving</strong>の時間というより<strong>Waiting</strong>の時間なので、結果的にアイコン表示までの時間を短縮できています。

CSSスプライトの仕組み自体は簡単もので、任意の要素の中で背景画像の位置を調整して表示しています。実際に表示されるのは要素で指定したwidth/heightの分だけなので、あたかも1個の独立した画像のように見えます。

CSSスプライトは非常に便利ですが、問題点もあります。スプライトのジレンマというのがあり、ページ数、保守性、最適化の観点から評価します。スプライトをする上でこの3つの中から2つしかとれません。

<img class="aligncenter size-full wp-image-5245" alt="dilemma" src="/static/blog/2013/08/dilemma.jpg" width="470" height="260" />

例えば、多くのページ数を保守性を保ちながらスプライトすると、最適化はちょっとあきらめなければいけません。また、多くのページ数を可能な限り最適化すれば保守性はあきらめなければなりません。また、保守性を意識しつつ最適化すれば、適用できるページ数は少なくなってしまいます。

考えてもみてください、画像の変更があるたびにPhotoshopを開いて、画像を置き直して、その位置をルーラーで割り出す。それがRetina画像であれば、実際の<span class="code">background-position</span>サイズから半分にしないといけません。気の遠くなるような面倒くさいタスクです。面倒くさくなくてもヒューマンエラーというのは起こるもので、単純な割り算（この場合Retina対策として背景位置を半分にする）でも、何回も繰り返せば、ミスはあります。そしてそのミスに気づかず数時間ロスをすることもままです。

もう、なんというかCSSスプライトが嫌すぎてデザイナーと喧嘩することもしばしば。これでは精神衛生上よくありません。

そこでそのめんどくさいタスクSass/CompassのMixinにやってもらおうと思います。<a href="http://t32k.me/mol/log/spriting-with-compass/">以前に書いた記事</a>から変更しています。
<ul>
	<li><strong><a href="https://github.com/t32k/maple#mixins">t32k/maple/mixin</a></strong></li>
</ul>
まず、Mixinの説明する前に<a href="https://github.com/t32k/maple">Mapleプロジェクト</a>をダウンロードしてきます。

<a href="https://github.com/t32k/maple#-installation">Node.js, Ruby, Sass, Compassがインストール</a>されていること前提。

まずは<a href="https://github.com/t32k/grunt-init-maple">grunt-init-maple</a>をインストールしておきましょう。
<pre><code>$ npm install -g grunt-cli
$ npm install -g grunt-init
$ git clone https://github.com/t32k/grunt-init-maple.git ~/.grunt-init/maple --recursive
</code></pre>
<span class="code">grunt-init maple</span>を実行すると以下のようにMapleプロジェクトに必要なファイルがスキャフォルディングされ（落ちてき）ます。

<img class="aligncenter size-full wp-image-5154" alt="grunt-init" src="/static/blog/2013/08/grunt-init.gif" width="640" height="400" />

落ちてきたら、<span class="code">/src/tools</span>（Gruntfile, package.jsonがある場所）に移動し、必要なGruntプラグインをインストール（<span class="code">npm install</span>）しておきます。これで下準備はOKです。

その場所で<span class="code">grunt develop</span>して、<span class="code">http://localhost:8080/components/</span>を見に行きましょう。そこにスプライトした画像が表示されていますからDevToolsなどで確認してみましょう。
<pre><code>.sprt-a {
  background-image: url(/files/img/sprite/tabs-s3217a038c5.png);
  background-repeat: no-repeat;
  background-size: 120px 25px;
}
.sprt-a-bird1 {
  width: 30px;
  height: 25px;
  background-position: 0 0;
}
.sprt-a-bird2 {
  width: 30px;
  height: 25px;
  background-position: -30px 0;
...
</code></pre>
上記のようなスタイルが当たっているかと思います。コレ自体はCSSなので普通のCSSスプライトのコードです。
<pre><code>$map-tabs: sprite-map("/files/img/sprite/tabs/*.png", $layout: horizontal);

// 共通クラス
.sprt-a { @include sprite(parent, $map-tabs); }
// 個別クラス
.sprt-a-bird1 { @include sprite(child, $map-tabs, bird1); }
.sprt-a-bird2 { @include sprite(child, $map-tabs, bird2); }
.sprt-a-bird3 { @include sprite(child, $map-tabs, bird3); }
.sprt-a-bird4 { @include sprite(child, $map-tabs, bird4); }</code></pre>
実際のSassコードは上記です。特に、煩わしい<span class="code">background-position</span>が書いてないことが分かります。各画像の<span class="code">background-position</span>の算出は<span class="code">sprite</span>というMixinで定義してありますので、使う人は画像の位置をいちいちPhotoshopで測るといったことをしなくてもよくなります。

詳しく説明していきますと、<span class="code">$map-tabs:</span>で、スプライトしたい画像を指定しています。imgディレクトリ配下にspriteディレクトリを作ってそこにスプライト画像をおいておけば、普通の画像と区別できて便利です。このディレクトリの中に、スプライト前の１個１々独立した画像が入っています。これらの画像をCompassがまとめてくれるのです。

<img class="aligncenter size-full wp-image-5246" alt="dir" src="/static/blog/2013/08/dir.jpg" width="660" height="420" />

<span class="code">.sprt-a</span>で指定してある。<span class="code">@include sprite(parent, $map-tabs)</span>は、各スプライト画像の共通プロパティを吐き出す用に指定します。各スプライトのclassすべてに同じ<span class="code">background-image</span>のプロパティを吐き出されては冗長ですからね。

parentは親（共通）classであることを示し、$map-tabsは展開するスプライト画像を指定しています。

<span class="code">.sprt-a-bird1</span>のchildは子(個別)classであることを示し、$map-tabsは上記と同じく、第3引数で、そのスプライト画像で使いたい画像名を指定しています。ここではbird1を指定していますので、<span class="code">/files/img/sprite/tabs/bird1.png</span>の<span class="code">background-position</span>がはきだされるようになります。
<pre><code>// 個別クラスにwidth/height吐き出さない場合
.sprt-a { @include sprite(parent, $map-tabs, bird1, true); }
.sprt-a-bird1 { @include sprite(child, $map-tabs, bird1, true); }</code></pre>
もし、<strong>個別のスプライト画像が全て同じ場合</strong>、第4引数に<span class="code">true</span>をつけて<span class="code">@include</span>すれば、個別クラスにはサイズ指定されず、共通クラスにwidth/heightが記述されて、コード量を節約することができます。

このようにMixinを活用出来れば、フロントエンドデベロッパーはデザイナーからもらったアイコン画像を任意のディレクトリに放り込んで、コマンドを打つだけでスプライト画像を生成することができます。冷えきったデザイナーとの関係にも終止符をうてます。

また、Compassで生成したPNG画像は減色やメタ情報のストリップなどされていませんので、そのままではデプロイしてしまうのはいかんともしがたいです。通常、<a href="http://imageoptim.com/">ImageOptim.app</a>などのツールで画像を最適化する必要性がありますが、ドラッグ&amp;ドロップもめんどくさいので、というか忘れるので、Gruntタスクに<a href="https://github.com/JamieMason/grunt-imageoptim">grunt-imageoptim</a>というものを組み込みました。これはなんてことのないタスクで指定した画像を自動的に（imageOptim.appが立ち上がって）最適化してくれます。

<img class="aligncenter size-full wp-image-5159" alt="build" src="/static/blog/2013/08/build.gif" width="640" height="400" />

Mapleプロジェクトでは、<span class="code">grunt build</span>でCSSがlintされ、Compassでコンパイルされ、CSSがminifyされ、画像がimageOptimされるというタスクを組んでありますので、忘れることもありません。

Sass/Compassを使えばスプライトのジレンマから開放されます。しかし、なんでもかんでもスプライト画像に詰め込んでしまえば、今度はRTTではなくDLタイムが問題になってきます。

CSSスプライトに取り込む前に、
<ul>
	<li>本当に画像で表現しなければいけないのか？</li>
	<li>CSSで表現できないのか？</li>
	<li>どこを調整したらCSSだけで表現できるようになるのか？</li>
</ul>
などデザイナーさんと相談してみましょう。

なにごともバランスが重要です。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/ref=nosim/" target="_blank"><img alt="続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス" src="http://ecx.images-amazon.com/images/I/51GQNCMJsZL._SL160_.jpg" border="0" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462" target="_blank">続・ハイパフォーマンスWebサイト</a><img style="border: none;" alt="" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" width="1" height="1" />
Steve Souders </span><span><span>武舎 広幸</span></span>

オライリージャパン 2010-04-10

<a href="http://www.amazon.co.jp/%E7%B6%9A%E3%83%BB%E3%83%8F%E3%82%A4%E3%83%91%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%B3%E3%82%B9Web%E3%82%B5%E3%82%A4%E3%83%88-%E2%80%95%E3%82%A6%E3%82%A7%E3%83%96%E9%AB%98%E9%80%9F%E5%8C%96%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9-Steve-Souders/dp/4873114462%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114462" target="_blank">Amazonで詳しく見る</a> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
