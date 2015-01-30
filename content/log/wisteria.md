---
categories: development
date: 2015-01-28T18:14:51-08:00
excerpt: 誰も傷つけない、傷つけたくない、そんなかわいいCSSライブラリです。
ogimage: http://t32k.me/wisteria/img/hero.jpg
subtitle: A class selectors based harmless CSS library
title: Wisteria：デザインツールとしてのCSS
---

![](http://t32k.me/wisteria/img/hero.jpg)

+ [Wisteria.css: A class selectors based harmless CSS library.](http://t32k.me/wisteria/)
+ [t32k/wisteria](https://github.com/t32k/wisteria)

[Wisteria](http://t32k.me/wisteria/)というCSSライブラリ作った。基本的な用途としてはモックアップや後方互換とかそこまで考えなくていい、小規模の個人用のページとかで使われることを想定している。

[Skeleton](http://getskeleton.com/)という、すごくシンプルなCSSライブラリがあるのだが、僕はこれが好きで、ちょっとしたものとか作るときによく使用している。このブログもSkeletonをベースにしているくらいだ。

でも最近使ってて、なにかこう違和感というか、相容れないモノを感じたので、思い立って自分用のCSSライブラリを作ってみたのだ。


## Harmless

Wisteriaを作るにあたって、一番気をつけたことは無害であること。つまり要素にスタイリング（`h2 { font-size: 24px }`みたいな）しないことを徹底した。ほとんとクラスセレクタ（`.h2 { font-size: 24px }`みたいな）でしか定義していない。

これはなぜかというと、基本的に`h2`なんてものは見出しとして大きく扱われるべきだけど、それは__基本的に__であって小さい文字列の`h2`要素だって時としては存在する（重要な文言であったり、余白を使えば必ずしもフォントサイズが大きい必要がない）。そうゆうゆうわけで、Skeletonとか使ってると、`h2`要素にスタイルが定義されているので、この文字を小さくするために再定義しなければならない。

これ、__すごくめんどい__。

いや、本腰入れて開発しようとかだったら再定義なんなりするけど、ちょっとしたページを作ったり、サイズ感を試したいときに思考が妨げられる。


```css
 .h1, .u-fz1 { font-size: 6.4rem !important; }
 .h2, .u-fz2 { font-size: 4.8rem !important; }
 .h3, .u-fz3 { font-size: 3.6rem !important; }
 .h4, .u-fz4 { font-size: 2.4rem !important; }
 .h5, .u-fz5 { font-size: 2.0rem !important; }
 .h6, .u-fz6 { font-size: 1.8rem !important; } 
 .u-fz7 {  font-size: 1.6rem !important; } 
 .u-fz8 {  font-size: 1.4rem !important; }
 .small, .u-fz9 {  font-size: 1.2rem !important; }
 .u-fz10 {  font-size: 1rem !important; }
```

また、最近のCSSライブラリは[Normalize.css](http://necolas.github.io/normalize.css/)で初期化されているのが前提だけど、これもやめてほしい。デフォルトのスタイリングをうまく残して初期化するものだけど、僕はブラウザのデフォルトスタイルを熟知しているわけではない。だから要素ごとのマージンとかも一律ゼロにしたい。そうゆうよくわからないものを覚えるために時間をかけたくない。

ということで、Wisteriaでは[HTML5-Reset](https://github.com/murtaugh/HTML5-Reset)を使ってキレイにリセットしてある。僕は真っ白なキャンバスに描きたいのだ。


## Helper

Wisteriaには多くのヘルパークラスというか、ユーティリティ系のクラスを保持している。

```css
/*	#Spacing
\*------------------------------------*/
.u-ma { margin: auto !important; }
.u-mtn { margin-top: 0 !important; }
.u-mts { margin-top: .4rem !important; }
.u-mtm { margin-top: 1.6rem !important; }
.u-mtl { margin-top: 3.2rem !important; }
.u-mtx { margin-top: 4.8rem !important; }
.u-mbn { margin-bottom: 0 !important; }
.u-mbs { margin-bottom: .4rem !important; }
.u-mbm { margin-bottom: 1.6rem !important; }
.u-mbl { margin-bottom: 3.2rem !important; }
.u-mbx { margin-bottom: 4.8rem !important; }
.u-mn { margin: 0 !important; }
```

`.u-`から始まるもの。こうゆう単一的な仕事をするクラスを多くもつのは[Maple](https://github.com/t32k/maple)でもやったことだが、あれはイレギュラーなデザインに対応するためである。

しかし、Wisteriaでは問題の背景がちがう。先ほどのHTML5-Resetで完全にマージンなどもリセットしてあるので、自分でマージンを設定しなければならない。そのおかげで、自由自在に自分でスペースを調整することが可能だ。

マージン以外にも多くのヘルパークラスがあるのだが、これはこれで学習コストが高くつくかもしれない。ということで命名規則に関しては[Emmet](http://docs.emmet.io/cheat-sheet/)風味な短縮形を採用しているので、ヘルパークラスに理解してなくても、だいたい予想がつくだろう。

## Hi-Control

局所的なレイアウトはスペーシングのヘルパーでなんとかなるけど、全体的なレイアウトにはグリッドシステムが必要だ。それに関してはFlexboxをベースにしたグリッドシステムを採用している。

これが何が嬉しいかというと、`float`とかで頑張ってるグリッドシステムのCSSライブラリはグリッドセルに対して、例えば3分割したかったら `class="cell-1of3"` みたいに書かないけどいけない。これ覚えるの大変だし（そうでもないか）、分割数を変える度にいちいち書き直すのもめんどい。

```html
  <div class="g-row">
    <div class="g-col">1/6</div>
    <div class="g-col">1/6</div>
    <div class="g-col">1/6</div>
    <div class="g-col">1/6</div>
    <div class="g-col">1/6</div>
    <div class="g-col">1/6</div>
  </div>
  <div class="g-row g-row--collapse">
    <div class="g-col">1/3</div>
    <div class="g-col">1/3</div>
    <div class="g-col">1/3</div>
  </div>
  <div class="g-row">
    <div class="g-col">auto</div>
    <div class="g-col u-w80">80%</div>
  </div>
```
てことで、Wisteriaでは`.g-row`の列に`.g-col`の名前の要素を入れとくだけでうまいこと分割数に応じてやってくれる。Flexbox様々である。その分、最新ブラウザにしか対応しなくなるけど、あくまでモックアップや個人用途で使うことを考えれば、十分メリットのほうが大きい。

結局作ってみて、真っ白なキャンバスを自由に操れるツールがほしかったのだとおもう。

[![](/mol/images/2015/0128-00.jpg)](http://alistapart.com/article/understandingprogressiveenhancement)

Wisteriaを使ってモックサイトを作るとなると、HTMLのclass属性にヘルパークラスを書き込みまくることになって、__コンテンツとスタイルの分離__とは！という状況なんだけど、そもそもPhotoshopやSketchを使ってデザインをするにあたって、それらを分けて考えるかというと、NOだ。

Sketchに[Content generator sketch plugin](https://github.com/timuric/Content-generator-sketch-plugin)というものがあるように、アタリとはいえ、デザイナーはそこにどんなコンテンツが来るのか考えながらデザインしている。

## Designing in the browser
 
話戻って、このブログの静的なページデザインファイルなんてものはない、いわゆる[インブラウザデザイン](http://css.studiomohawk.com/in-browser-design/2011/04/16/designing_in_browser/)をして作ったわけだが、この時の違和感というか、やりにくさの原因が分かった。

結局、ブラウザでデザインするにはHTMLファイル（テンプレートファイル）とスタイルシートを行き来しなければならないのだ。そして下手にマークアップ脳もあるため、メンテナンス性を考えたCSS設計、命名の適当さなど考えると結局デザインしづらくなってしまう（デザインに集中できなくなってしまう）。

HTMLファイルにだけに集中して、ガシガシ書き込んでいけば、どんどんビジュアルが完成されていく。うん、実にやりやすい。インブラウザデザインと言って、最初からコンテンツとスタイルの分離を意識するからやりにくいのであって、いったん、それは忘れる必要がある（だからといって、style属性で書くように密結合することもない）。

Wisteriaを使えば、PhotoshopやSketchでマウスで操作するように（それに近い状態で）、ブラウザ上でデザインしていけるだろう。

僕はこうゆうのを求めていたんだ。




