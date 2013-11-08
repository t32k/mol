---
layout: post
title: 部屋とYシャツと私
subtitle: Good-bye Compass, Good-bye Ruby.
categories: maple
status: publish
type: post
excerpt: "「部屋とYシャツと私」は、平松愛理の8枚目のシングル。"
---

部屋とYシャツと私、AutoprefixerとSpritesmithとLibsassの話。

愛しの[Maple](https://github.com/t32k/maple)フレームワークというか、Grunt詰め合わせセットですが、GruntはNode.js依存で、使っているCSSプリプロセッサはSassなのでRuby依存で、なんだかキメラみたいで気持ち悪い。いっそのこと、StylusにしてNode.jsで統一しようか、むしろ[Middleman](http://middlemanapp.com/)みたいにRubyで統一するか、考えものだ。とりあえずはCompassを辞めてみようという結論に至ったので代替案を探る。


MapleでCompassを使っている理由は2つ。

+ ベンダープレフィックスを付ける手間をなくしたい
+ CSSスプライトを自動化したい

これらをGruntプラグインでなんとか置き換えれないものか。

## grunt-autoprefixer

+ [nDmitry/grunt-autoprefixer](https://github.com/nDmitry/grunt-autoprefixer)

ちょうど、[myakura氏のブログで取り上げられていたAutoprefixer](http://myakura.hatenablog.com/entry/2013/09/30/035244)が便利そうなので、これのGruntプラグインがないか探したらもちろんあった。

```js
autoprefixer: {
  options: {
    browsers: ['ios >= 5', 'android >= 2.3']
  },
  dist: {
    src: '../files/css/maple.css'
  },
}
```

Gruntの設定も至極簡単だ。対象のCSSファイルとと対応するバージョンを指定するだけだ。
あとは正規のプロパティ書いておくだけ、Autoprefixerがバージョンに応じてベンダープレフィックス付きのプロパティを追加・削除してくれる。

Compassのミックスインによる書き方よりも、真っ当というか、なんかこっちの実装のほうが素敵だと素直に思った。あと対応するバージョンの指定方法も、CompassみたいにベンダーごとにON/OFFするんじゃなくて、`last 2 versions`といった書き方もできたり、[蟹ｳｾﾞ](https://twitter.com/tacamy/status/398400127259262977)のデータを元にしてあったりと柔軟に指定できるのも魅力かな。

## grunt-spritesmith

+ [Ensighten/grunt-spritesmith](https://github.com/Ensighten/grunt-spritesmith)

CSSスプライトを自動化するためにCompassを使用しはじめたのもあって、移行しんどかった。使い勝手的には[Compass Sprite](https://gist.github.com/t32k/e65534b5a8bb124e1cbe)のほうが今のところは良いと思う。 

しかし、Spritesmithに変更することでCSSプリプロセッサに依存せずにCSSスプライトの自動化を手に入れることができる。MapleではSass用にコードを吐き出してるけど、Stylus用にも吐き出せるし、生のCSSでもできる。

```css
$_bird1: 0px 149px 0px -149px 60px 49px 302px 198px "/files/img/sprite/tabs.1383826639213.png";
$_bird2: 0px 0px 0px 0px 180px 147px 302px 198px "/files/img/sprite/tabs.1383826639213.png";
$_bird3: 182px 0px -182px 0px 120px 98px 302px 198px "/files/img/sprite/tabs.1383826639213.png";
$_bird4: 62px 149px -62px -149px 60px 49px 302px 198px "/files/img/sprite/tabs.1383826639213.png";

// $list: <X> <Y> <Offset X> <Offset Y> <Width> <Height> <Total Width> <Total Height> <Image Path>

@mixin sprite($isParent, $sprite) {
  @if $isParent == "parent" {
    $imagePath: nth($sprite, 9);
    background-image: url("#{$imagePath}");
    background-repeat: no-repeat;
    background-size: round( nth($sprite, 7) / 2 ) round( nth($sprite, 8) / 2 );
  } @else {
    width: round( nth($sprite, 5) / 2 );
    height: round( nth($sprite, 6) / 2 );
    background-position: round( nth($sprite, 3) / 2 ) round( nth($sprite, 4) / 2 );
  }
}
```

Spritesmithはタスクを実行すると、任意の画像をスプライト画像にまとめて、上記のようなコードを吐き出してくれる。要は、`$_bird1`のようなスプライト画像のWidth/Heightやオフセット値をまとめたリスト型の変数を提供してくれるので、あとはそのデータを使って自分で独自のミックスイン（Retina対応している）を作成すればよい。このデータさえあればCompassの関数を使わなくて良くなる。


```js
sprite: {
  dist: {
    dt: '<%= Date.now() %>',
    src: '../files/img/sprite/tabs/*.png',
    destImg: '../files/img/sprite/tabs.<%= sprite.dist.dt %>.png',
    imgPath: '/files/img/sprite/tabs.<%= sprite.dist.dt %>.png',
    destCSS: '../files/css/sass/libs/_sprite.scss',
    algorithm: 'binary-tree',
    padding: 2,
    cssTemplate: 'spritesmith.mustache'
  }
}
```
各画像のオフセット値が分かるので`binary-tree`という、単純に縦並べ、横並べじゃなくてCompassの`Smart`みたいな、詰め込んだ並べ方ができるのも良さげ。

Gruntでの設定がややめんどいし、キャッシュバスターのために`Date.now()`の値をファイル名に入れてるけど、タスクが実行される度に画像に変更がなくても新たにスプライト画像を生成してしまうし、以前のスプライト画像もCompassみたいに勝手に削除されない。この辺、もうちょっと頑張ってみる必要性がある。


## Libsass

+ [sindresorhus/grunt-sass](https://github.com/sindresorhus/grunt-sass)

ということで、Compassの呪縛からはとりあえず解放されたのでSassもC実装の[Libsass](http://libsass.org/)にしてみた。LibsassはRubyで書かれていたSassのコンパイラーをCで書きなおしたもの。それをNode.jsから利用できるにしたのが[node-sass](https://github.com/andrew/node-sass)で、それのGruntプラグインが[grunt-sass](https://github.com/sindresorhus/grunt-sass)。要はSassだけどRubyがいらないシロモノ。


しかもCで書かれているので、[爆速でコンパイルされるらしい](http://www.damln.com/log/sassc-and-bourbon-it-works/)よ（まだ大きいファイルで試してないけど）とりあえず今んとこ絶賛開発中でSCSSファイルしかコンパイルできてないし、RubySassでうまくコンパイルされるけど、Libsassではコンパイルできないってバグもあるし、ご利用は慎重にって感じ。個人的にはそんなにSassっぽいというかCSSプリプロセッサ全開！な書き方してないし、変数使えたらいいなぁ程度なので、そこまで困らないはず。。。

というわけで、Sass使いながらでも、

[Good-bye Compass, Good-bye Ruby.](https://github.com/t32k/maple/commit/fb621dbda3634b25575618b16a49560a4000a5d2)

できました。おしまい(・ω<)

