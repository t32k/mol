---
layout: post
title: Sassの親セレクタ参照&について
categories:
- css
tags:
- sass
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '2847'
---
<a href="http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#referencing_parent_selectors_">Sassの親セレクター参照の<strong>&amp;</strong></a>の話。

Sassでどんどんネストして書いてると「親セレクタ参照してーわー、できるなら親孝行してーわー」ってたまになりますよね。僕はそんなにならないんですけど、一番わかりやすい例としてリンクの擬似クラスがあります。こんな例です。

<!--more-->
<pre><code>// SCSS
#main {
  color: black;
  a {
    font-weight: bold;
    &amp;:hover { color: red; }
    &amp;:visited { color: blue; }
  }
}</code></pre>
↑上がコンパイルされて↓こんな風になります。
<pre><code>/* CSS */
#main {
  color: black;}
#main a {
  font-weight: bold;}
#main a:hover {
  color: red;}
#main a:visited {
  color: blue;}</code></pre>
Sassのコードだと、aのセレクタの下層にリンクの擬似クラスのスタイルがまとまり、コードが見やすくなってますね。この例だと<strong>&amp;</strong>の部分が#main aに置き換わるわけです。はい。

ほかには、モジュールごとでスタイルを変えたい時とか。
<pre><code>// SCSS
.mod {
　color: black;
　font-weight: bold;
　&amp;.hoge { color: red; }
　&amp;.fuga { color: blue; }
}</code></pre>
.modでひとつのモジュールの基本的なスタイルを記述して、.mod.hogeといった感じでclassの複数づけしたときに、基本スタイルから微妙に変化をつけるみたいなやりかたのときとかも便利です。たぶん。

これもまた、.modのブロックの中に派生するスタイルが１つにまとまっていてナイスな気がします。

んで、調子こいてこんな風にも&amp;を使うようになりました。
<pre><code>// local.scss
.kanazawa {
　color: blue;
　.ishikawa &amp; {
　　color: red;
　}
}</code></pre>
親が違う親を持っていた時のスタイルみたいな。なんか文字にすると複雑な家庭事情ですね。心中お察しします。
<pre><code>/* CSS */
.kanazawa {
　color: blue;}
.ishikawa .kanazawa {
　color: red;}</code></pre>
展開するとなんてことのない感じです。.kanazawaだと横浜の金沢なのか、石川の金沢なのわかんねーから、石川の金沢のときは文字を赤くしましょうよって思想です。たぶん。しらんけど。

んで、このCSSを流用したい。北陸で流用したいという欲情に駆られたのがこんな感じのHTML。
<pre><code>&lt;div class="hokuriku"&gt;
 北陸良いとこ～♪
 &lt;div class="ishikawa"&gt;
  細長い県なの～♪
  &lt;div class="kanazawa"&gt;
   そこの県庁所在地なの～♪
  &lt;/div&gt;
 &lt;/div&gt;
 &lt;div class="kanazawa"&gt;
  どこの金沢よ～。それどこ情報よ～。俺が寝てないってどこ情報よ～。
 &lt;/div&gt;
&lt;/div&gt;</code></pre>
今まで地方レベルで考えてこなかったんだけど、急に、.hokuriku（北陸地方）という上位概念がでてきて、この中でさっきのlocal.scssを流用したい場合。こんな感じなると思う。
<pre><code>// SCSS
.hokuriku {
 @import "local.scss";
}
// つまり↑これは↓これということ。
.hokuriku {
　.kanazawa {
　　color: blue;
　　.ishikawa &amp; {
　　　color: red;
　　}
　}
}</code></pre>
んで、コンパイル。
<pre><code>.hokuriku .kanazawa {
  color: blue;
}
.ishikawa .hokuriku .kanazawa {
  color: red;
}</code></pre>
問題は2個めのやつですよね。親参照使ったやつ。石川県北陸地方金沢市になっててイミフｗｗｗｗウケるｗｗｗｗｗ

HTML内では.hokurikuが最も祖先なので、この場合の.ishikawa .hokuriku .kanazawaのスタイルは有効になりませんね。実際のこの問題に出くわしたときは。もっとコード量が多くてなおかつ複雑で、この親参照の仕様をちゃんと理解せずにいたので、理解に時間がかかりました（スタイルがなぜか効かないので!importantしたりとか...）。なんでメモがてら書いておきました。

だからといって、<strong>&amp;</strong>使うなよってことはないです。最初に紹介したリンクパターンやモジュールパターンのような単純に<strong>”親”</strong>を参照しているものであれば、特に問題ないかと思います。親の更に親が〜といったような使い方も環境（HTML）が変わるようなことがないかぎり、特に問題無いと思うけど、いざ流用したいってなったとき（人生なにが起きるかわかりません）ネストの仕方によっては今回のようなことが起きてしまうなーって。て！
