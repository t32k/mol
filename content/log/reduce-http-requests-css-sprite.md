---
date: 2013-08-20
title: HTTPリクエストを減らすために【CSS Sprite編】スプライト地獄からの解放
subtitle: CSS Sprite Automation.
categories: 
    - performance
excerpt: 2日目は、HTTPリクエストを減らす最もポピュラーな手法、CSSスプライトについて説明します。
ogimage: /static/blog/2013/08/requests.gif
---

このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっている。

+ [【序章】HTTPリクエストは甘え](/mol/log/reduce-http-requests-overview/)
+ __【CSS Sprite編】スプライト地獄からの解放__
+ [【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ](/mol/log/reduce-http-requests-webfont/)
+ [【DataURI編】遅延ロードでレンダリングブロックを回避](/mol/log/reduce-http-requests-datauri/)
+ [【終章】我々には1000msの猶予しか残されていない](/mol/log/reduce-http-requests-one-second/)

2日目は、HTTPリクエストを減らす最もポピュラーな手法、CSSスプライトについて説明する。

まずは動画をご覧頂きたい。

<div class="fluid"><iframe src="//www.youtube-nocookie.com/embed/s__XwfwxMW8" frameborder="0" allowfullscreen></iframe></div>

+ [img要素読み込み | WebPagetest Test Result](http://www.webpagetest.org/result/130816_VR_9E8/)
+ [CSS Sprite読み込み | WebPagetest Test Result](http://www.webpagetest.org/result/130816_J6_9EG/)

左が30個のアイコン画像を一つ一つimg要素として読み込んでいるのに対して、右は１つの背景画像（CSSスプライト）として読み込んでいる。この場合、表示完了までの差はCSSスプライトのほうが圧倒的に速い。

![](/static/blog/2013/08/waterfall.png)

これは前回のHTTPリクエストの仕組みを理解していれば当然のことだろう。つまり、ホスト名ごとの同時接続数とRTTが大いに関係している。上記のimg画像読み込みのウォーターフォールチャートを確認してみれば一目瞭然だ。CSSスプライトすることで一つの画像ファイルサイズは重くなるが、この場合、重要なのはReceivingの時間というよりWaitingの時間なので、結果的にアイコン表示までの時間を短縮できている。

CSSスプライトの仕組み自体は簡単もので、任意の要素の中で背景画像の位置を調整して表示している。実際に表示されるのは要素で指定したwidth/heightの分だけなので、あたかも1個の独立した画像のように見えるだけだ。

CSSスプライトは非常に便利だが問題点もある。スプライトのジレンマというのがあり、__ページ数__、__保守性__、__最適化__ の観点から評価し、スプライトをする上でこの3つの中から2つしかとれない。

例えば、多くのページ数を保守性を保ちながらスプライトすると、最適化はちょっとあきらめなければいけない。また、多くのページ数を可能な限り最適化すれば保守性はあきらめなければならない。また、保守性を意識しつつ最適化すれば、適用できるページ数は少なくなってしまうようにだ。

画像の変更があるたびにPhotoshopを開いて、画像を置き直して、その位置をルーラーで割り出す。それがRetina画像であれば、実際のbackground-positionサイズから半分にしないといけない。気の遠くなるような面倒くさいタスクだ。面倒くさくなくてもヒューマンエラーというのは起こるもので、単純な割り算（この場合Retina対策として背景位置を半分にする）でも、何回も繰り返せば、ミスは必ずでてくる。そしてそのミスに気づかず数時間ロスをすることもままだ。

もう、なんというかCSSスプライトが嫌すぎてデザイナーと喧嘩することもしばしば。これでは精神衛生上よくない。

そこでそのめんどくさいタスクSass/CompassのMixinにやってもらおうと思う。

+ [CSS Sprite for Retina Display Maple.css](https://gist.github.com/t32k/e65534b5a8bb124e1cbe)

まず、Mixinの説明する前に私が作っている[Maple](https://github.com/t32k/maple)プロジェクトをダウンロードしてくる（Node.js, Ruby, Sass, Compassがインストールされていること前提）次に、grunt-init-mapleをインストールする。

```shell
$ npm install -g grunt-cli
$ npm install -g grunt-init
$ git clone https://github.com/t32k/grunt-init-maple.git ~/.grunt-init/maple –recursive
```

`grunt-init maple`を実行すると以下のようにMapleプロジェクトに必要なファイルがスキャフォルディングされる。

![Demo maple](/static/blog/2013/08/grunt-init.gif)

落ちてきたら、/src/tools（Gruntfile, package.jsonがある場所）に移動し、必要なGruntプラグインをインストール（npm install）しておく。これで下準備はOK。

その場所で`grunt develop`して`http://localhost:8080/components/`を見にいく。そこにスプライトした画像が表示されていますからDevToolsなどで確認してみる。

```css
.sprt-a {
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
…
```

上記のようなスタイルが当たっているかと思う。コレ自体はCSSなので普通のCSSスプライトのコードだ。

```sass
$map-tabs: sprite-map(“/files/img/sprite/tabs/*.png”, $date: horizontal);

// 共通クラス
.sprt-a { @include sprite(parent, $map-tabs); } 

// 個別クラス 
.sprt-a-bird1 { @include sprite(child, $map-tabs, bird1); } 
.sprt-a-bird2 { @include sprite(child, $map-tabs, bird2); } 
.sprt-a-bird3 { @include sprite(child, $map-tabs, bird3); } 
.sprt-a-bird4 { @include sprite(child, $map-tabs, bird4); }
```

実際のSassコードは上記。特に煩わしいbackground-positionが書いてないことが見てとれる。各画像のbackground-positionの算出はspriteというMixinで定義してあるので、使う人は画像の位置をいちいちPhotoshopで測るといったことをしなくてもよくなる。

説明すると`$map-tabs:`で、スプライトしたい画像を指定。imgディレクトリ配下にspriteディレクトリを作って、そこにスプライト画像をおいておけば、普通の画像と区別できて便利。このディレクトリの中にスプライト前の１個１々独立した画像が入っている。これらの画像をCompassがまとめてくれる。

![Dir](/static/blog/2013/08/dir.jpg)

.sprt-aで指定してある。`@include sprite(parent, $map-tabs)`は、各スプライト画像の共通プロパティを吐き出す用に指定する。各スプライトのclassすべてに同じbackground-imageのプロパティを吐き出されては冗長だから。

parentは親（共通）classであることを示し、$map-tabsは展開するスプライト画像を指定している。

.sprt-a-bird1のchildは子（個別）classであることを示し、$map-tabsは上記と同じく、第3引数でそのスプライト画像で使いたい画像名を指定している。ここではbird1を指定しているので、/files/img/sprite/tabs/bird1.pngのbackground-positionが生成される。

```sass
// 個別クラスにwidth/height吐き出さない場合
.sprt-a { @include sprite(parent, $map-tabs, bird1, true); }
.sprt-a-bird1 { @include sprite(child, $map-tabs, bird1, true); }
```

もし、個別のスプライト画像が全て同じサイズの場合、第4引数にtrueをつけて@includeすれば、個別クラスにはサイズ指定されず、共通クラスにwidth/heightが記述されて、コード量を節約することができる。

このようにMixinを活用出来れば、フロントエンドデベロッパーはデザイナーからもらったアイコン画像を任意のディレクトリに放り込んで、コマンドを打つだけでスプライト画像を生成することができる。冷えきったデザイナーとの関係にも終止符をうてる。

また、Compassで生成したPNG画像は減色やメタ情報のストリップなどされていないので、そのままではデプロイしてしまうのはいかんともしがたい。通常、ImageOptim.appなどのツールで画像を最適化する必要性があるが、ドラッグ&ドロップもめんどくさいので、というか忘れるので、Gruntタスクにgrunt-imageoptimというものを組み込んだ。これはなんてことのないタスクで指定した画像を自動的に（imageOptim.appが立ち上がって）最適化してくれる。

![Build](/static/blog/2013/08/build.gif)

Mapleプロジェクトでは、`grunt build`でCSSがlintされ、Compassでコンパイルされ、CSSがminifyされ、画像がimageOptimされるというタスクを組んであるので忘れることもない。

Sass/Compassを使えばスプライトのジレンマから開放される。しかし、なんでもかんでもスプライト画像に詰め込んでしまえば、今度はRTTではなくDLタイムが問題になってくる。

CSSスプライトに取り込む前に、

+ 本当に画像で表現しなければいけないのか？
+ CSSで表現できないのか？
+ どこを調整したらCSSだけで表現できるようになるのか？

などデザイナーさんと相談してみよう。

なにごともバランスが重要だ。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/51GQNCMJsZL._SL160_.jpg" alt="続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" name="azlinklink" target="_blank">続・ハイパフォーマンスWebサイト</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.1.18</div></div><div class="azlink-detail">Steve Souders,武舎 広幸,福地 太郎,武舎 るみ<br />オライリージャパン<br />売り上げランキング: 361407<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>