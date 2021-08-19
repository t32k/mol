---
date: 2012-09-06
title: Sassの親セレクタ参照&について
categories: 
    - css
---
[Sassの親セレクター参照の&](https://sass-lang.com/documentation/style-rules/parent-selector)の話。

Sassでどんどんネストして書いてると「親セレクタ参照してーわー、できるなら親孝行してーわー」ってたまになりますよね。僕はそんなにならないんですけど、一番わかりやすい例としてリンクの擬似クラスがあります。こんな例です。


```scss
// SCSS
#main {
  color: black;
  a {
    font-weight: bold;
    &:hover { color: red; }
    &:visited { color: blue; }
  }
}
```

↑上がコンパイルされて↓こんな風になります。

```css
/* CSS */
#main {
  color: black;}
#main a {
  font-weight: bold;}
#main a:hover {
  color: red;}
#main a:visited {
  color: blue;}
```

Sassのコードだと、aのセレクタの下層にリンクの擬似クラスのスタイルがまとまり、コードが見やすくなってますね。この例だと **&** の部分が `#main a` に置き換わるわけです。はい。

ほかには、モジュールごとでスタイルを変えたい時とか。

```scss
// SCSS
.mod {
　color: black;
　font-weight: bold;
　&.hoge { color: red; }
　&.fuga { color: blue; }
}
```

`.mod` でひとつのモジュールの基本的なスタイルを記述して、`.mod.hoge` といった感じでclassの複数づけしたときに、基本スタイルから微妙に変化をつけるみたいなやりかたのときとかも便利です。たぶん。

これもまた、`.mod` のブロックの中に派生するスタイルが１つにまとまっていてナイスな気がします。

んで、調子こいてこんな風にも&amp;を使うようになりました。

```scss
// local.scss
.kanazawa {
　color: blue;
　.ishikawa & {
　　color: red;
　}
}
```

親が違う親を持っていた時のスタイルみたいな。なんか文字にすると複雑な家庭事情ですね。心中お察しします。

```css
/* CSS */
.kanazawa {
　color: blue;}
.ishikawa .kanazawa {
　color: red;}
```

展開するとなんてことのない感じです。`.kanazawa` だと横浜の金沢なのか、石川の金沢なのわかんねーから、石川の金沢のときは文字を赤くしましょうよって思想です。たぶん。しらんけど。

んで、このCSSを流用したい。北陸で流用したいという欲情に駆られたのがこんな感じのHTML。

```html
<div class="hokuriku">
北陸良いとこ～♪
    <div class="ishikawa">
        細長い県なの～♪
        <div class="kanazawa">
            そこの県庁所在地なの～♪
        </div>
    </div>
    <div class="kanazawa">
        どこの金沢よ～。それどこ情報よ～。俺が寝てないってどこ情報よ～。
    </div>
</div>
```

今まで地方レベルで考えてこなかったんだけど、急に、`.hokuriku`（北陸地方）という上位概念がでてきて、この中でさっきのlocal.scssを流用したい場合。こんな感じなると思う。

```scss
// SCSS
.hokuriku {
 @import "local.scss";
}
// つまり↑これは↓これということ。

.hokuriku {
　.kanazawa {
　　color: blue;
　　.ishikawa & {
　　　color: red;
　　}
　}
}
```

んで、コンパイル。

```css
.hokuriku .kanazawa {
  color: blue;
}
.ishikawa .hokuriku .kanazawa {
  color: red;
}
```

問題は2個めのやつですよね。親参照使ったやつ。石川県北陸地方金沢市になっててイミフｗｗｗｗウケるｗｗｗｗｗ

HTML内では `.hokuriku` が最も祖先なので、この場合の `.ishikawa .hokuriku .kanazawa` のスタイルは有効になりませんね。実際のこの問題に出くわしたときは。もっとコード量が多くてなおかつ複雑で、この親参照の仕様をちゃんと理解せずにいたので、理解に時間がかかりました（スタイルがなぜか効かないので!importantしたりとか...）。なんでメモがてら書いておきました。

だからといって、**&** 使うなよってことはないです。最初に紹介したリンクパターンやモジュールパターンのような単純に **親** を参照しているものであれば、特に問題ないかと思います。親の更に親が〜といったような使い方も環境（HTML）が変わるようなことがないかぎり、特に問題無いと思うけど、いざ流用したいってなったとき（人生なにが起きるかわかりません）ネストの仕方によっては今回のようなことが起きてしまうなーって。て！
