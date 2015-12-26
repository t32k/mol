---
date: 2010-03-04
title: Google AnalyticsでSafariのバージョンを確認するフィルタ
categories: analytics
---
Safariのシェア並びにバージョン別のシェアが知りたくて、Google Analyticsで確認してみたらびっくり、バージョンじゃなくてビルド番号なんだね、こやつは。

`ユーザー &gt; PC環境 &gt; ブラウザ &gt; Safari`

こんなんわかんないよヽ(`Д´ﾒ)ﾉ ﾌﾟﾝｽｶ！ってことで、これをなんとかフィルタで書き換えたい欲望に駆られました。<a href="http://ja.wikipedia.org/wiki/Safari#.E3.83.90.E3.83.BC.E3.82.B8.E3.83.A7.E3.83.B3.E5.B1.A5.E6.AD.B4">Wikipedia</a>で確認してみると、どうやら<strong>410番台が2.x系</strong>、<strong>520番台が3.x系</strong>、<strong>530番台が4.x系</strong>だと分かる。1.x系はちょっとごちゃごちゃしているのと、シェアも少ないだろうということでスルーの方向で。

で、書いてみたフィルタがこれ。

<img class="fig" src="http://farm5.static.flickr.com/4023/4405869024_13a7018cd4.jpg" alt="" />

<span style="color: #888888;"><em>Analytics 設定 &gt; プロファイル設定 &gt; 新しいフィルタを作成</em></span>

<em> </em>
<pre><span style="color: #888888;">// 4.x系</span>
^53(.)+

<span style="color: #888888;">// 3.x系</span>
^52(.)+

<span style="color: #888888;">// 2.x系</span>
^41(.)+</pre>
<em>検索する文字列 </em>をバージョンごとに上記のように変更して、フィルタを作らなきゃいけないのがめんどくさい。適用してみたこれ↓

<img class="fig" src="http://farm5.static.flickr.com/4020/4405869032_5140a6de05.jpg" alt="" />

数日後、適用されたプロファイルがこれ↓（3分間クッキングみたい）

<img class="fig" src="http://farm3.static.flickr.com/2770/4405103923_6a6c708701.jpg" alt="" />

だいたいのシェアが確認できます。僕のやりたかったこれ！一応満足。
<h3>反省点</h3>
まぁ、<em>アドバンスフィルタ</em> の <em>次の文字を含む で</em>上記の正規表現を入力したら、バージョン毎のセッション数が出るので、出た数値をExcelで円グラフにすれば早いですｗ

フィルタで加工してしまえば、もう元のデータに戻せないので汎用性を考えるとあまりおススメしません。今回僕はフィルタの勉強のためにしたのが大きいです。Safari 5なんてものが出たらまたフィルタかけないといけませんしね。

<a href="http://code.google.com/intl/ja/apis/analytics/docs/gdata/gdataDeveloperGuide.html">Google Analytics Data Export API</a> が使えたら一番スマートですかね。勉強します...
