---
date: 2013-08-21
title: HTTPリクエストを減らすために【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ
subtitle: grunt-webfont
categories: 
    - performance
excerpt: 3日目は、スマホ環境であればHTTPリクエストを減らすためにWebフォントの採用について考慮しても、やぶさかではないでしょう。
ogimage: /static/blog/2013/07/c2eef1dbac4917459d28818432f9c6b8.png
---

このシリーズはHTTPリクエストの理解を通じてWebパフォーマンスの重要性について考える5章構成になっている。

+ [【序章】HTTPリクエストは甘え](/mol/log/reduce-http-requests-overview/)
+ [【CSS Sprite編】スプライト地獄からの解放](/mol/log/reduce-http-requests-css-sprite/)
+ __【WebFont編】ドラッグ＆ドロップしてコマンド叩いてウェーイ__
+ [【DataURI編】遅延ロードでレンダリングブロックを回避](/mol/log/reduce-http-requests-datauri/)
+ [【終章】我々には1000msの猶予しか残されていない](/mol/log/reduce-http-requests-one-second/)

3日目は、スマホ環境であればHTTPリクエストを減らすためにWebフォントの採用を考慮しても、やぶさかではないだろう。

まずは下記の画像をご覧頂きたい。

![](/static/blog/2013/08/arrows.png)

これはプロジェクトで私が使用していたスプライト画像だが（実際は縦にして使用）、このような単純な形状、単色のアイコンであれば、Webフォント化したほうがなにかと都合がよい。

このスプライトであれば、__カラー__ × __矢印の向き__ × __シャドウの有無__ パターンの可能性があり、スプライトすれば1リクエストでおさまるが、それでも画像が肥大化していけば、__Receiving__が無視できない状況になってくる。

そこでWebフォント化すれば色は自由に変更可能だし、フォントなので`text-shadow`で影を当てることも可能、`font-size`で大きさも変更でき柔軟に対応することができる。

それではWebフォントって一体どうやって作るのだろうか？高いフォント作成アプリを購入しなければならないのだろうか？オンライン作成ツールもあるようだが、毎回、新規アイコン追加の度にそのツールのサイトを訪問しなければならないのだろうか？

+ [❍ IcoMoon - icon font & SVG icon sets](https://icomoon.io/)

以前は上記オンラインツールを使っていたが、やはり更新対応を考えるとめんどうだった。そうゆうわけで、[Maple](https://github.com/t32k/maple)プロジェクトでは[grunt-webfont](https://github.com/sapegin/grunt-webfont)を導入している。

前回の記事を見ながらMapleプロジェクトを準備してもらいたい。そのほかの必要環境として以下のものインストールしておく。[Homebrew](http://brew.sh/)も入っていなければインストールする。

```shell
$ brew install fontforge ttfautohint
$ brew install https://raw.github.com/sapegin/grunt-webfont/master/Formula/sfnt2woff.rb
```

あと事前に必要になるのはフォントの元となるSVGファイル。SVGファイルを作るうえで便利なテンプレートがあるのでそれを拝借する。

+ [cognitom/symbols](https://github.com/cognitom/symbols)


![](/static/blog/2013/07/c2eef1dbac4917459d28818432f9c6b8.png)

テンプレートを使ってMapleでは上記のようなイラレファイルを作成した。[iconmonstr](http://iconmonstr.com/)にはいろいろ使い勝手がいいアイコンが無料で配布されているので、ここから必要なものをとってくるのもいいだろう。Illustratorでアートボード別に書きだして、SVGファイルとして保存する。要注意なのはこのアートボードの空白部分も含めてSVGファイルなので気をつける。

![](/static/blog/2013/08/fontdir.png)

基本的にこの部分はデザイナーさんにやってもらえればよいことなので、フロントエンドデベロッパーは完成したSVGファイルを、`/src/files/font/svg`ディレクトリに投げ込んでコマンド打つだけだ。

```shell
$ grunt webfont
Running “webfont:dist” (webfont) task
Font ‘myfont-b5fd89266afbbfbfc281a0ce9a5bf50e’ with 13 glyphs created.
```

で、`/src/tools/`で`grunt webfont`を実行すれば上記のようなログとともに、.woffと.ttfと_myfont.scssが作成される。


```sass
// _setting.scss
//-------------------------------------
@import "../vendors/myfont";

// _myfont.scss
.icon-hoge:before {
content:"\f100";
}
```

_myfont.scssは_setting.scssで`@import`されていますので、特にCSSをいじる必要性はない。

![](/static/blog/2013/08/icon.png)

上記のように、`.icon-{SVGファイル名}`のクラスを当てれば、すぐさま使える。

Webフォント使えば、CSSスプライトに頼らなくても大丈夫だー＼(-o-)／って使う前は思っていたが、やはり単純な表現に限定される。グラデーションカラーかつシャドウ有りや、部分的に色を変えるなどはWebフォントでは無理があるので、そこはCSSスプライトを採用するか、デザインを少し調整してWebフォント化するかはデザイナーと相談すべきだろう。

またWebフォントも複数のアイコンのリクエストをまとめることができるが、Webフォント自体のリクエストが必要になるので、フォントがダウンロードされるまでは、当たり前だが表示されない。そのため数種類のパターンで収まることがわかっていればWebフォント化可能でもCSSスプライトでまとめることも考慮すべきだろう。

なにごともバランスが重要だ。
