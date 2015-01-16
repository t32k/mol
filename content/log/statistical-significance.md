---
date: 2011-03-01
title: 施策前後のCV率に有意差はあるのか？
categories:
- analytics
---

<a href="http://www.flickr.com/photos/joost-ijmuiden/4768350290/"><img class="fig" title="Untitled" src="/static/blog/2011/02/statics.jpg" alt="" width="470" height="260" /></a>

<span style="font-size: x-small;"><span style="color: #888888;"><strong>By <a href="http://www.flickr.com/photos/joost-ijmuiden/">Joost J. Bakker IJmuiden</a></strong></span></span>

はい、タイトルのとおりでございます。とある改善を行いまして、その効果というのが誤差の範疇なのか、それとも効果があったのか（プラスマイナス問わず）知りたい状況に陥りましたんで、いろいろ調べてみましたよというお話。

Google Website Optimizer とか使えば、テストを実行してしばらくしたら勝手にこっちの方が何％優れてるよーって教えてくれるんですけど、今回のケースだと GWO の実装が難しかったので  Google Analytics で指標を読み取ることにしました。

<!--more-->

やりたいことはですね。手元にあるデータは施策前後の１週間毎のコンバージョン率（8週間分）がありますんで前後8週間の平均CV率を出して何％改善したのか確認したいわけです。で、今回の場合1%程度改善されたのですが、これって別になんにもしなくても1%上がっちゃったりするのか、それとも偶然ではない<a href="http://ja.wikipedia.org/wiki/%E6%9C%89%E6%84%8F"><strong>有意</strong></a>の差なのかってことを理解しようと思います。
<table border="0" width="470">
<tbody>
<tr>
<th style="background: #d9d9d9;"></th>
<th style="background: #d9d9d9; text-align: center;" scope="col">1w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">2w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">3w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">4w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">5w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">6w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">7w</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">8w</th>
</tr>
<tr>
<td style="background: #d7d6fe; text-align: right;">Before</td>
<td>93.82%</td>
<td>93.83%</td>
<td>93.23%</td>
<td>93.65%</td>
<td>93.99%</td>
<td>93.65%</td>
<td>93.95%</td>
<td>94.37%</td>
</tr>
<tr>
<td style="background: #ffbfdf; text-align: right;">After</td>
<td>94.73%</td>
<td>94.77%</td>
<td>94.18%</td>
<td>94.71%</td>
<td>94.99%</td>
<td>94.76%</td>
<td>94.45%</td>
<td>94.59%</td>
</tr>
</tbody>
</table>
<span style="font-size: x-small;">施策前後8週間のコンバージョン率の遷移</span>
<h3>まずはじめに</h3>
はい、大学で統計学の単位を取ったような気もしないわけでもないそうゆう気もしないわけでもないという感じなので、ほぼ統計的知識ゼロです。間違いなどあれば指摘してもらえると嬉しいです。

手始めに「<a href="http://www.google.co.jp/search?hl=ja&amp;q=%E6%9C%89%E6%84%8F%E5%B7%AE">有意差</a>」とかでググッてみるのですが、出てくるリソース読んでもさっぱりΣ(´∀｀；)なので、というか数式とか見た瞬間拒絶反応がでてくるのでウォームアップがてらこの本読んでみました。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274065707/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51EFK1XNQ5L._SL160_.jpg" border="0" alt="マンガでわかる統計学" width="124" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E3%83%9E%E3%83%B3%E3%82%AC%E3%81%A7%E3%82%8F%E3%81%8B%E3%82%8B%E7%B5%B1%E8%A8%88%E5%AD%A6-%E9%AB%98%E6%A9%8B-%E4%BF%A1/dp/4274065707%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4274065707" target="_blank">マンガでわかる統計学</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
高橋 信 トレンドプロ </span>&nbsp;

<span>オーム社  2004-07
売り上げランキング : 4991</span>

<span><a href="http://www.amazon.co.jp/%E3%83%9E%E3%83%B3%E3%82%AC%E3%81%A7%E3%82%8F%E3%81%8B%E3%82%8B%E7%B5%B1%E8%A8%88%E5%AD%A6-%E9%AB%98%E6%A9%8B-%E4%BF%A1/dp/4274065707%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4274065707" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
ルイちゃん可愛いよ(;´Д｀)ﾊｧﾊｧってことで、文系の僕でも数時間で苦なく読めました（ちゃんと理解はしてないけど）。やっぱり僕みたいなトーシローが最初からガチな統計本 or ドキュメントに手を出すのは玉砕必死です。こうゆうので耐性をつけてから望んだ方が良かったです。

はい、ということでもう一度トライしてみましょう。なんということでしょう。読める、読めるぞ！（ムスカ風）ってほどでもないけども、以前よりは頭に入っていきます。
<h2>有意差検定</h2>
そうゆうことでググリマックってたらどうやら僕がしたいのはt検定という奴っぽいです。
<blockquote>2組の標本について平均に有意差があるかどうかの検定などに用いられる。
<a href="http://ja.wikipedia.org/wiki/T%E6%A4%9C%E5%AE%9A">t検定 - Wikipedia</a></blockquote>
Yeah!これこれ！で、さらにググリマックってたらドンピシャなリソース発見！検索した中でも一番文系フレンドリーで分かりやすそうです（・(ｪ)・）
<ul>
	<li><strong><a href="http://kogolab.jp/elearn/hamburger/chap4/sec3.html">4.3　t検定 - ハンバーガー統計学</a></strong></li>
</ul>
ここのサイトは本当に分かりやすいので、量もそんなには多くないので最初から全部読んでみるとよいと思います。
<ul>
	<li><strong><a href="http://kogolab.jp/elearn/hamburger/">ハンバーガー統計学にようこそ！</a></strong></li>
</ul>
さてどうやら、t検定を行う前段階として以下の2点を調べておく必要性がありそうなので、まずはそこから始めましょう。
<ul>
	<li><strong>標本が正規分布に従うかどうか</strong></li>
	<li><strong>標本の分散が等しいかどうか</strong></li>
</ul>
<h3>Jarque-Bera 検定（標本が正規分布に従うかどうか）</h3>
<a href="http://ja.wikipedia.org/wiki/T%E6%A4%9C%E5%AE%9A#.E5.89.8D.E6.AE.B5.E9.9A.8E">t検定の wikipedia</a> には正規分布かどうか調べるためには、コルモゴロフ-スミルノフ検定やシャピロ-ウィルク検定使えばいいよと書いてあるけど、どれも難しくて（どうやって計算するのか）わからなかった。Jarque-Bera 検定ならなんとかできそうなので、この検定で調べてみる。

とりあえず、正規分布というのは、

<strong>正規分布</strong> - 平均を山の中心として左右になめらかに広がった「つりがね型」をした分布

はい、数学の時間によく見たあれです。

<a href="http://en.wikipedia.org/wiki/Jarque-Bera_test"><img class="alignnone" title="Jarque-Bera_test" src="http://upload.wikimedia.org/math/1/4/0/14084be9ee2c2a037f1cfbc4562cdba2.png" alt="" width="181" height="48" /></a>

n：標本数、S：歪度、K：尖度

<a href="http://ja.wikipedia.org/wiki/%E6%AD%AA%E5%BA%A6"><strong>歪度</strong></a>（わいど, Skewness）- 分布の非対称性を示す指標
<a href="http://ja.wikipedia.org/wiki/%E5%B0%96%E5%BA%A6"><strong>尖度</strong></a>（せんど、Kurtosis）- 分布のとんがり具合を表す指標

Jarque-Bera 検定の公式が上記になるんですけど、どうやらこのJBの値がだいたい6より小さければ、<a href="http://okwave.jp/qa/q4076739.html">有意水準が5％で正規分布と見做して構わないらしい</a>です。

はい、いろいろ分かんないことだらけだけど、とりあえず数値だしてみるよ。
nは8週間分あるから、8。歪度はExeclのSKEW関数を使えば出てくるよ！尖度はExeclのKURT関数を使えば出てくるよ！
<table border="0" width="370">
<tbody>
<tr>
<th style="background: #d9d9d9;"></th>
<th style="background: #d9d9d9; text-align: center;" scope="col">n</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">S</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">K</th>
<th style="background: #d9d9d9; text-align: center;" scope="col">JB</th>
</tr>
<tr>
<td style="background: #d7d6fe; text-align: right;">Before</td>
<td style="text-align: right;">8</td>
<td style="text-align: right;">-0.118</td>
<td style="text-align: right;">1.4396</td>
<td style="text-align: right;">0.7094</td>
</tr>
<tr>
<td style="background: #ffbfdf; text-align: right;">After</td>
<td style="text-align: right;">8</td>
<td style="text-align: right;">-0.864</td>
<td style="text-align: right;">1.2489</td>
<td style="text-align: right;">1.5145</td>
</tr>
</tbody>
</table>
で、計算結果するとでどちらも6以下でおｋ。これでどうやら正規分布として見なしてもよさそうですね。

<span style="font-size: x-small;">※ 尖度の定義
Jarque-Bera 検定の調べていると、（K-3）としている公式を見かけますがこれは尖度の定義による違いだそうです。wikipediaによると「E<a href="http://ja.wikipedia.org/wiki/%E5%B0%96%E5%BA%A6#2種類の定義">xcelの分析ツール等は正規分布の尖度を0としている</a>」らしいので、今回の場合は、-3する必要性はなさそうです。</span>
<h3>F検定（標本の分散が等しいかどうか）</h3>
よし、標本が正規分布だと分かった次は分散が等しいかどうかだ。

<a href="http://kusuri-jouhou.com/statistics/fkentei.html"><img title="F検定(等分散の検定) " src="http://kusuri-jouhou.com/images/statistics/aa3.gif" alt="" width="460" height="48" /></a>

こういった感じのことを調べるんだね。ちなみに、分散というのは

<strong>分散</strong> - データが平均値を中心にして、どのくらいばらついているのかを示した数値
<span style="color: #000000; font-size: x-small;"> ※標準偏差（<span style="color: #888888;">Standard Deviation</span>） ＝ 分散の平方根（ルート）</span>

<a href="http://ja.wikipedia.org/wiki/%E5%88%86%E6%95%A3#.E6.A8.99.E6.9C.AC.E5.88.86.E6.95.A3"><img class="alignnone" title="s^2=\frac{1}{n}\sum_{i=1}^{n}(\bar{x}-x_i)^2" src="http://upload.wikimedia.org/math/d/5/2/d52d28bc57dff2e28bfa2ae195f1bd37.png" alt="" width="160" height="48" /></a>

シグマが出てきてもうアカンΣ(´∀｀；)！ってなったかた大丈夫、数列の総和って意味だよ。要は、

((データ－平均値)の２乗)の総和÷個数

ってことを言ってるだね。今回は２つの標本（データ）があるので、それぞれ分散を求める。分散はExeclのVARP関数を使えば出てくるよ！

<a href="http://en.wikipedia.org/wiki/F-test_of_equality_of_variances"><img class="alignnone" title="F-test" src="http://upload.wikimedia.org/math/1/a/f/1afdd4bd258e9b84c2a42d1a8f195c2e.png" alt="" width="70" height="48" /></a>

分子に大きい方の値を当てはめて、F値を出しましょう。
<table border="0" width="200">
<tbody>
<tr>
<th style="background: #d9d9d9; text-align: right;"></th>
<th style="background: #d9d9d9; text-align: right;">S<sup>2</sup></th>
</tr>
<tr>
<td style="background: #d7d6fe; text-align: right;">Before</td>
<td style="text-align: right;">0.09</td>
</tr>
<tr>
<td style="background: #ffbfdf; text-align: right;">After</td>
<td style="text-align: right;">0.05</td>
</tr>
</tbody>
</table>
F値は0.09/0.05の1.8になります。

あとは以下の公式に当てはめていくと,,,
<blockquote>自由度は分子の自由度df1＝n1-1、分母の自由度df2＝n2-1のF分布に従う。自由度が求まったら<a href="http://kusuri-jouhou.com/statistics/bunpuhyou.html">F分布表</a>からFαを求めることができる。

・判定1≦F≦Fαのとき、P＞0.05となる→帰無仮説を棄却できない→等分散である。

<a href="http://kusuri-jouhou.com/statistics/fkentei.html">F検定(等分散の検定) </a></blockquote>
df1, df2の自由度はどちらも8-1で、7となり、F分布表より、7×7の場所は3.79となり、

1≦1.8≦3.79 が成り立つ、つまり等分散と言えることができます。
<h3>t検定（Student's t-test）</h3>
２つの標本は正規分布に従い、等分散と言えるのでようやくt検定としけこみたいところですが、もう一つだけ確認しておきたいことがあります。
<h4>対応の有無</h4>
標本の対応の有無というのは、2つの独立した母集団から標本を選んでくるのか、1つの母集団から標本を選んでくるのかということです。今回の場合、施策したサイトのユーザーの期間比較ですので、施策前後で同じユーザーというのは可能性が低いので、対応はないと判断しました。
<h4>対応のないt検定</h4>
ようやく、ほんとようやくです。ここまできたらあとは以下の資料を元に進めてくだけです。
<ul>
	<li><strong><a href="http://kogolab.jp/elearn/hamburger/chap4/sec3.html">4.3　t検定 - ハンバーガー統計学</a></strong></li>
</ul>
流れは以下のとおりですがな。
<ol>
	<li>帰無仮説を立てる</li>
	<li>帰無仮説の否定である対立仮説を立てる</li>
	<li>有意水準を決める</li>
	<li>得られた標本を使って、指標tを計算する</li>
	<li>標本の数から自由度を計算する</li>
	<li>t分布表の該当する自由度を見て、tが棄却域にはいっている（棄却）か、いない（採択）かを判定する</li>
	<li>結論を決める</li>
</ol>
<strong>1. 帰無仮説を立てる</strong>

帰無仮説というのは「差はない」という仮説らしいです。この場合、「施策前後で差はない」という仮説を立てます。

<strong>2. 対立仮説を立てる</strong>

帰無仮説とは反対の仮説であり、「施策前後で差がないとはいえない、つまり、差がある」という仮説を立てます。

<strong>3. 有意水準を決める</strong>

どの程度の正確さをもって帰無仮説を棄却するのかという水準です。たいていは厳しくて1%、少し甘くて5%だそうなので、今回は5%とします。

<strong>4. 指標tを計算する</strong>

t＝（標本平均の差）／SQRT（（Aの不偏分散／Aの標本数）＋（Bの不偏分散／Bの標本数））

これに当てはめていけばいいんだす！めんどくハンバーガー統計さんのとこにEXCELシートありますんで、そこに当てはめていけばでます。

<strong>不偏分散</strong> - 母分散の推定値 ＝（（データ－平均値）の二乗）の総和÷（個数-1）

<span style="font-size: x-small;">※ SQRT関数は平方根（ルート）を求める関数です！</span>

よって、t値は-5.78

<strong>5. 自由度を計算する</strong>

自由度＝（Aの標本数－1）＋（Bの標本数－1）＝Aの標本数＋Bの標本数－2

A,Bも標本数8なので自由度は14です。

<strong>6. 棄却か採択か</strong>

<img class="alignnone size-full wp-image-2532" title="t" src="/static/blog/2011/02/t.png" alt="" width="470" height="301" />

<strong>7. 結論を決める</strong>

自由度が14のとき、有意水準5% 2.145, 有意水準1% 2.977となります。これをt分布で表すと上記のようなグラフになります。今回の場合、t値は-5.78となり棄却域に入ります。

よって、最初に立てた帰無仮説は棄却され、施策前後で差がないとはいえない、つまり、差があると言えます。

はい、できたー！そらできたー！やたー！

なんとかできたけど、細かいこと全然わかってないのでもう少し勉強しようと思いました(；´Д｀)
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4478820090/warikiru-22/ref=nosim/"><img class="fig" src="http://ecx.images-amazon.com/images/I/51-vAi68VSL._SL160_.jpg" border="0" alt="完全独習 統計学入門" width="113" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E5%AE%8C%E5%85%A8%E7%8B%AC%E7%BF%92-%E7%B5%B1%E8%A8%88%E5%AD%A6%E5%85%A5%E9%96%80-%E5%B0%8F%E5%B3%B6-%E5%AF%9B%E4%B9%8B/dp/4478820090%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4478820090" target="_top">完全独習 統計学入門</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
小島 寛之 </span>&nbsp;

<span>ダイヤモンド社  2006-09-29
売り上げランキング : 1395</span>

<span><a href="http://www.amazon.co.jp/%E5%AE%8C%E5%85%A8%E7%8B%AC%E7%BF%92-%E7%B5%B1%E8%A8%88%E5%AD%A6%E5%85%A5%E9%96%80-%E5%B0%8F%E5%B3%B6-%E5%AF%9B%E4%B9%8B/dp/4478820090%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4478820090" target="_top">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
あ、有意な差があると言えると証明できたけど、それが今回行った施策によるものかっていう点はまた別問題なので気をつけてまし。
