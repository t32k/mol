---
date: 2012-12-02
title: パフォーマンスからみるSass/Compass 第2回：CompassによるCSS Sprite
subtitle: CSS Preprocessor Advent Calendar 2012
categories: development
excerpt: パフォーマンスの勉強ができてなおかつSass/Compassのお勉強にもなるお得なシリーズまさかの2回目。Adventにぶつけてきた！
ogimage: http://t32k.me/static/blog/2012/12/compile.png
---

> Sass、Less、StylusなどCSS Preprocessorに関するAdvent Calendarです。― [CSS Preprocessor Advent Calendar 2012 - Adventar](http://www.adventar.org/calendars/1)

パフォーマンスの勉強ができてなおかつSass/Compassのお勉強にもなるお得なシリーズまさかの2回目。Adventにぶつけてきた！ややもするとシリーズものの2作目というのは駄作になりがちだが、そんなプレッシャーはねのけて乱反射！やっていくYO! 

これまでの：

+ [パフォーマンスからみるSass/Compass 第1回：Nestingと@import - MOL](http://t32k.me/mol/log/sass-nesting-and-import/)
+ [パフォーマンスからみるSass/Compass 番外編：MSは青かった - MOL](http://t32k.me/mol/log/compass-ie-hex-str-function/)

## CSS Spriteの利点・欠点

『ハイパフォーマンスWebサイト』の書籍には「高速サイトを実現する14のルール」というものがある。その中でも最も効果のある対策として「HTTPリクエストを減らす」ことを挙げている。HTTPリクエストというのは画像やJavaScriptファイル、CSSファイル等をWebページで読み込む（サーバーにリクエストする）ことを言う。

このリクエストが多ければ多いほど、HTMLページの読み込み速度は遅くなってしまう。フロント（マークアップ）側でできる対策としてはポピュラーなものとしてCSSスプライトという手法があり、これは複数の画像をひとつにまとめ、背景画像として`background-position`を調整することで一つ一つの画像として表示する方法だ。

<div class="rm">
<iframe src="https://www.youtube.com/embed/s__XwfwxMW8?controls=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></div>

+ [Minimize HTTP Requests! Requests 30 vs 1 (CSS Sprite) - YouTube](https://www.youtube.com/watch?v=s__XwfwxMW8)

CSSスプライトがいかに有用かは上記の動画を見てもらえれば分かるだろう。アイコン画像を30個を`img src=""`で読み込む場合と、30個のアイコンを全てひとつの画像にまとめたCSSスプライトで読み込む場合では（環境によっても変化はあるがこの場合）3倍の差が出た。

ただ、CSSスプライトにも問題がある。それは管理が非常に面倒な点だ。まずひとつひとつの画像をPhotoshopなどの画像編集ツールでまとめる必要あり、またその配置した画像の座標を`background-position`に反映させる必要がある。

+ [CSS Sprite Generator, Editor, and Code](http://www.ja.spritegen.website-performance.org/)

CSS Sprite Generatorのような便利なオンラインツールが存在するが、画像の変更があった場合、再度オンラインにアップロードしてコードをジェネレートする必要があったり、Retina対応を考えると自分で画像のサイズを半分にして計算しないといけない。 これでは、サービスリリース後などの度重なる改善・修正にマークアップが追いつかず不必要な画像までもそのままスプライト画像に残してしまった状態で無駄な転送量が発生してしまう。

実際に私がやっている案件でもグローバルナビゲーションや、カテゴリナビゲーションなどにスプライト画像を使用しHTTPリクエストを最小限に抑えている。リリース当時はきれいにまとまったスプライト画像も度重なるサービス改善で、スプライト画像のカテゴリアイコンがなくなったり、追加したりと何度も手入れをしなければならないことが発生し、その度に画像の作成・位置の再計算など非常に面倒な作業だった。

## Compassによる解決策

そこで目につけたのが、Compassフレームワークだ。Sassは開発当初から利用していたが、Compass自体は利用していなかった。Compassにはスプライトを簡単に利用できるAPIが備わっており、画像編集ソフトなど使わなくても画像を一つにまとめたり、それぞれの`background-position`を算出してくれる。 使い方は非常にシンプルだ。スプライト画像にまとめたい個々の画像を任意のディレクトリに格納しておき、`@import`でそのディレクトリを指定し、`@include all-ディレクトリ名-sprites`で展開するだけだ。

```sass
// 基本的なCompassスプライトの利用方法
@import "my-icons/.png";
@include all-my-icons-sprites;
```

上記のSCSSコードは下記のようにコンパイルされる。

```css
/* コンパイルされたCSS */
.my-icons-sprite,
.my-icons-fav,
.my-icons-hist,
.my-icons-my,
.my-icons-new {
  background: url("/images/my-icons-sab4abd7554.png") no-repeat;
}
.my-icons-fav { background-position: 0 -68px; }
.my-icons-hist { background-position: 0 -136px; }
.my-icons-my { background-position: 0 -204px; }
.my-icons-new { background-position: 0 0; }
```

また上記のコードではmy-iconsディレクトリ以下にある個々の画像をひとつのスプライト画像にまとめてくれる。 

![](http://t32k.me/static/blog/2012/12/compile.png)

ただ、基本的な利用方法ではRetina対応や、自分のコードスタイルに合わず、独自でmixinを作成する必要があった。

```sass
//　自分で定義したmixin
@mixin sprites($map, $map-item, $isCommon:false) {
  @if $isCommon {
    background-image: sprite-url($map);
    background-repeat: no-repeat;
    background-size: round(image-width(sprite-path($map)) / 2) round(image-height(sprite-path($map)) / 2);
  } @else {
    $pos-y: round(nth(sprite-position($map, $map-item), 2) / 2);
    width: round(image-width(sprite-file($map, $map-item)) / 2);
    height: round(image-height(sprite-file($map, $map-item)) / 2);
    background-position: 0 $pos-y;
  }
}
```

実際の使い方

```sass
// mapを指定する
// $spacingの引数で個々の画像のマージンを指定できる
// この値がなければぴっちり縦に並ぶことになる
$map-tabs: sprite-map("/files/img/sprites/tabs/", $spacing: 4px);

// 共通プロパティのextend
%tabs { @include sprites($map-tabs, common, true); }

// 共通プロパティ指定
i {
    @extend %tabs;
    position: relative;
    display: block;
    margin: 0 auto;
}

// 個別プロパティ指定
.tab-new i { @include sprites($map-tabs, new, false); }
.tab-fav i { @include sprites($map-tabs, fav, false); }
.tab-hist i { @include sprites($map-tabs, hist, false); }
.tab-mypage i { @include sprites($map-tabs, my, false); }
.tab-new.active i { @include sprites($map-tabs, new-on, false);}
.tab-fav.active i { @include sprites($map-tabs, fav-on, false); }
.tab-hist.active i { @include sprites($map-tabs, hist-on, false); }
.tab-mypage.active i {@include sprites($map-tabs, my-on, false); }
```

上記のコードでは、実際の画像ファイルの縦・横サイズを半分にして計算し、Retina対応をしている。等倍の画像ファイルも用意するのであればメディアクエリーを利用し分岐処理のコードを追加すれば良い。

このコードの肝というか、個人的に重要だと思っているのはこの`image-width(sprite-path($map)`部分である。これはスプライトした画像のパスを取り、その`width`を返すものだ。通常のCSSやSassではこのようにファイルアクセスしそのファイルの情報を得るということはできなかった。故に、人力で`background-position`を割り出すという面倒なことをやっていたのだ。

これより、非常に簡単にCSSスプライトの画像を管理できるようになった。なぜならスプライトしたい画像をまとめたディレクトリに画像を追加・削除・修正することで、Compassがそれを検知し自動的にスプライト画像を再生成し、`background-position`の値をコードに反映してくれる。 これにより度重なるトライ・アンド・エラーに対して、時間的・モチベーション的にも余裕をもって改善のイテレーションを回せるようになった。

+ [CSS Sprite Helpers for Compass | Compass Documentation](http://compass-style.org/reference/compass/helpers/sprites/)
+ [Spriting with Compass | Compass Documentation](http://compass-style.org/help/tutorials/spriting/)

![](http://t32k.me/static/blog/2012/12/sprites.png)

また気をつけなければならないことに、簡単にCSS Spriteできるようになったからといってすべての画像をスプライト画像にまとめることがないようにしたい。可能な限りHTTPリクエストを減らすことは良いことだが、何事も限度がある。たとえばサイトで使うすべての画像をまとめてしまえば、そのどれか一つでも更新があれば再度リクエストしなければならない。

これはキャッシュ保持できる期間が短くなってしまうことを意味し、結果的に応答性の悪いサイトになってしまう。ヘッダー画像のような大きな画像も含めば、初期ロード時にかなり待たなければならず体感速度的にも大きな影響がある。

またそのような大きな画像と上記のような小さなアイコンが縦に並べば、空白の部分が多く生じる。ホワイトスペース部分はファイルサイズに影響しないが画像を表示するのにメモリを多く必要としてしまうため、これは非力なモバイルデバイス端末では無視できない事象である。

そのため、私は種類ごと、どのページでその画像が呼び出されるのかといった基準でスプライト画像を分けて管理している。タブバーで使われるものはtabsディレクトリ、矢印系のものはarrowsディレクトリに分けてなど、スプライト画像を作成している。

## さらなる最適化のために

スプライト画像のPNGはCompassによって生成されるわけだが、これはRubyライブラリのchunky_pngを使用している。何ぶん画像を生成するので重たい処理だ。Cで書かれた拡張機能のoily_pngをインストールすると生成を早くすることができる。インストールは簡単だ。`gem install oily_png`を打つだけで、あとはCompassが自動で認識してくれる。

またまた、Compassで生成された画像はもちろん最適化されていないので[ImageOptim.app](https://imageoptim.com/)などで最適化する必要がある。imageOptimをかけると、中には半分くらいファイルサイズを減量させることも可能で、この手間をかけるのとかけないのでは大きな違いだ。ただ、スプライトの画像を何度も追加・削除・修正するたびにimageOptim.appを起動し、ドラッグ・アンド・ドロップなんて真似事はめんどくさいの極みである。

そこでGruntである。Gruntについては@ahomuブログを参照してもらえると良いだろう。gurnt deployといった具合にリリースする前にかますオリジナルタスク、またはwatchタスクに下記のような画像最適化タスクを入れておけば自動的に最適化してくれる。

いかがだっただろうか。CSS Spriteという一見複雑な作業も1つ1つのタスクに分けて考えれば機械にできることなので、そういったものはすべて機械に任せるようにし人間はもっとクリエイティブなことに集中したほうが良い。幸いなことに、Sass/CompassやGruntのように機械と対話する環境は以前よりもずっと整備されてきているので利用しない手はない。そう、この波に乗るっきゃない(・ω<)