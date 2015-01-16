---
date: 2009-10-07
title: CSSセレクタのパフォーマンスへの影響
subtitle: Performance Impact of CSS Selectors
excerpt: Performance Impact of CSS Selectors
---

+ [ASCII.jp：30分でできる！Webサイトを高速化する6大原則](http://ascii.jp/elem/000/000/457/457749/)

高速化する6大原則として『4.CSS セレクターは短く最適化せよ！』とこの記事では挙げられているのですが、原則というのはちょっと言い過ぎではないかと。少なくとも『3.HTTPリクエストは最小にせよ！』などと同列に考えるのは避けた方が良いかもしれません。

というのも、[ハイパフォーマンスWebサイト](http://www.amazon.co.jp/dp/487311361X/)の著者である[Steve Souders](http://stevesouders.com/)はこんなことを言っています。

> CSSセレクタを最適化するために時間を費やすのは価値のあることだとは思わない。もし、明日起きて世界中のサイトのCSSセレクタが奇跡的に最適化されていたのなら、私は遠くに行ってこう叫びたい。『誰も気づいてないですやん！！』

+ [High Performance Web Sites :: Performance Impact of CSS
Selectors](http://www.stevesouders.com/blog/2009/03/10/performance-impact-of-
css-selectors/)

Steve Soudersがなぜこう考えるのでしょうか？

彼はセレクタの違い（ベースライン、タグ、クラス、子、子孫セレクタ）によってレンダリング速度に違いが出るかテストを行いました。[テストページ](http://
stevesouders.com/tests/css-
selectors/index.html)には2000個のアンカーと2000個のCSSルールを含んでいます。

![CSS Selector Performance](/mol/images/2009/10-07-fig.jpg)

図；Performance Impact of CSS Selectors より

上記のグラフのような結果になったのですが、ここではブラウザ毎の比較は考慮せずにCSSセレクタのパフォーマンスに対する影響に注目してみると、最も早いケースと最も遅いケースで平均で50ミリ秒しか違わないと言うことです。さらに（今日の70%のユーザーにあたる）IE 6&7,Fx3に限って言えば、CSSセレクタ最適化をしても20ミリ秒しか改善されません。

テストケースを見てもらえれば分かると思いますが、あり得ない量のCSSコードになってます。一応、これは考えられうる最悪なケース（米国の主な大規模サイトの平均のCSSルール数は1000）を想定して考えられたテストなので、実際のサイトはもっと少ないのは言わずもがなです。

テストの結果を基にSteve Soudersはこう述べています。

> 大半のサイトにとって、CSSセレクタを最適化することで得られるメリットは小さいし、コストに見合わない。ただ、CSSセレクタのいくつかの種類やJavaScriptと影響しあうものに関しては極めて遅くなることがある。このあたり(offsetWidth, :hoverなど)は今後調べていきたい。


## 個人的雑感

とまぁ、そんな感じで費用対効果が見えませんね。既存サイトのCSSセレクタを書き換えていくようなことはお薦めいたしません。ゼロの状態からサイト構築するときに頭の隅に置いておくぐらいが良いのではないでしょうか。

また、子セレクタなり、子孫セレクタなり、適用範囲を狭めていくやり方は階層化されていて個人的には分かりやすいかなと思ったりもします。

```
/* こっちの方が好き */
#main .sentence {color:#000}
#sub  .sentence {color:#fff}
    
/* こっちの方がパフォ的に（程度は別として）良い */
.main-sentence {color:#000}
.sub-sentence {color:#fff}
```

このあたりは各自のコーディングスタイルを尊重すれば良いかと思います。パフォーマンスとメンテナンス性はトレードオフなところがあるので[どこかのGoogleみたい](http://www.suzukikenichi.com/blog/why-doesnt-google-
validate/)に偏執狂な感じになるのもどうかなとも思います。

あと、ユニバーサルセレクタもめんどくさいときは使いますね。全称セレクタも使うケースを考えたらmargin/paddingのリセットぐらいなもので、これも気に
する程度ではないかなと思っています。（気になる人はテストしてみて＞＜）

２年前の僕みたいに不安になって藁をもすがる思いで質問してしまう子もでてくるかもしれません。（ググレオレｗ）

+ [全称セレクタを用いたスタイルの正規化 | Web標準Blog](http://standards.mitsue.co.jp/archives/001247.html)

まぁそんなわけで、CSSセレクタで悩むぐらいならHTTPリクエストを減らしたほうが効果的なのでは。

## 参考サイト

+ [Writing Efficient CSS - MDC（邦訳）](https://developer.mozilla.org/ja/Writing_Efficient_CSS)

