---
layout: post
title: CSSセレクタのパフォーマンスへの影響
categories:
- performance
tags:
- css
status: publish
type: post
published: true
meta:
  pvc_views: '13466'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/10/performance-impact-of-css-selectors.html
  _edit_last: '1'
---
<ul>
	<li><a href="http://ascii.jp/elem/000/000/457/457749/">ASCII.jp：30分でできる！Webサイトを高速化する6大原則</a></li>
</ul>
高速化する6大原則として『4.CSS セレクターは短く最適化せよ！』とこの記事では挙げられているのですが、原則というのはちょっと言い過ぎではないかと。少なくとも『3.HTTPリクエストは最小にせよ！』などと同列に考えるのは避けた方が良いかもしれません。

というのも、<a href="http://www.amazon.co.jp/gp/product/487311361X?ie=UTF8&amp;tag=warikiru-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=487311361X">ハイパフォーマンスWebサイト</a>の著者である<a href="http://stevesouders.com/">Steve Souders</a>はこんなことを言っています。
<blockquote>CSSセレクタを最適化するために時間を費やすのは価値のあることだとは思わない。もし、明日起きて世界中のサイトのCSSセレクタが奇跡的に最適化されていたのなら、私は遠くに行ってこう叫びたい。『誰も気づいてないですやん！！』
<a href="http://www.stevesouders.com/blog/2009/03/10/performance-impact-of-css-selectors/">High Performance Web Sites :: Performance Impact of CSS Selectors</a></blockquote>
Steve Soudersがなぜこう考えるのでしょうか？

彼はセレクタの違い（ベースライン、タグ、クラス、子、子孫セレクタ）によってレンダリング速度に違いが出るかテストを行いました。<a href="http://stevesouders.com/tests/css-selectors/index.html">テストページ</a>には2000個のアンカーと2000個のCSSルールを含んでいます。

<img src="http://lh4.ggpht.com/_1drnogi3vdg/SstjKcFzh2I/AAAAAAAAAnA/mcvVilvyBIg/css-selectors-top-ten-2000-color-513x497-revised.jpg" alt="CSS Selector Performance" />
図；Performance Impact of CSS Selectors より

上記のグラフのような結果になったのですが、ここではブラウザ毎の比較は考慮せずにCSSセレクタのパフォーマンスに対する影響に注目してみると、最も早いケースと最も遅いケースで平均で50ミリ秒しか違わないと言うことです。さらに（今日の70%のユーザーにあたる）IE 6&amp;7, Fx3に限って言えば、CSSセレクタ最適化をしても20ミリ秒しか改善されません。

テストケースを見てもらえれば分かると思いますが、あり得ない量のCSSコードになってます。一応、これは考えられうる最悪なケース（米国の主な大規模サイトの平均のCSSルール数は1000）を想定して考えられたテストなので、実際のサイトはもっと少ないのは言わずもがなです。

テストの結果を基にSteve Soudersはこう述べています。
<blockquote>大半のサイトにとって、CSSセレクタを最適化することで得られるメリットは小さいし、コストに見合わない。ただ、CSSセレクタのいくつかの種類やJavaScriptと影響しあうものに関しては極めて遅くなることがある。このあたり(offsetWidth, :hoverなど)は今後調べていきたい。</blockquote>
<h3>個人的雑感</h3>
とまぁ、そんな感じで費用対効果が見えませんね。既存サイトのCSSセレクタを書き換えていくようなことはお薦めいたしません。ゼロの状態からサイト構築するときに頭の隅に置いておくぐらいが良いのではないでしょうか。

また、子セレクタなり、子孫セレクタなり、適用範囲を狭めていくやり方は階層化されていて個人的には分かりやすいかなと思ったりもします。
<pre><code>/* こっちの方が好き */
#main .sentence {color:#000}
#sub  .sentence {color:#fff}

/* こっちの方がパフォ的に（程度は別として）良い */
.main-sentence {color:#000}
.sub-sentence {color:#fff}</code></pre>
このあたりは各自のコーディングスタイルを尊重すれば良いかと思います。パフォーマンスとメンテナンス性はトレードオフなところがあるので<a href="http://www.suzukikenichi.com/blog/why-doesnt-google-validate/">どこかのGoogleみたい</a>に偏執狂な感じになるのもどうかなとも思います。

あと、ユニバーサルセレクタもめんどくさいときは使いますね。全称セレクタも使うケースを考えたらmargin/paddingのリセットぐらいなもので、これも気にする程度ではないかなと思っています。（気になる人はテストしてみて＞＜）

２年前の僕みたいに不安になって藁をもすがる思いで質問してしまう子もでてくるかもしれません。（ググレオレｗ）
<ul>
	<li><a href="http://standards.mitsue.co.jp/archives/001247.html">全称セレクタを用いたスタイルの正規化 | Web標準Blog | ミツエーリンクス</a></li>
</ul>
まぁそんなわけで、CSSセレクタで悩むぐらいならHTTPリクエストを減らしたほうが効果的なので、興味ある方は<a href="http://www.cssnite-ishikawa.jp/">CSS Nite ISHIKAWA</a>(終了しました)までお越しください。
<h3>参考サイト</h3>
<ul>
	<li><a href="https://developer.mozilla.org/ja/Writing_Efficient_CSS">Writing Efficient CSS - MDC（邦訳）</a></li>
</ul>
