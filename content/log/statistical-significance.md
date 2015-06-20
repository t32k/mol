---
date: 2011-03-01
title: 施策前後のCV率に有意差はあるのか？
subtitle:
categories: analytics
excerpt: はい、タイトルのとおりでございます。とある改善を行いまして、その効果というのが誤差の範疇なのか、それとも効果があったのか（プラスマイナス問わず）知りたい状況に陥りましたんで、いろいろ調べてみましたよというお話。
ogimage: http://t32k.me/mol/images/2015/statics/01.jpg
---

![](/mol/images/2015/statics/01.jpg)

はい、タイトルのとおりでございます。とある改善を行いまして、その効果というのが誤差の範疇なのか、それとも効果があったのか（プラスマイナス問わず）知りたい状況に陥りましたんで、いろいろ調べてみましたよというお話。

Google Website Optimizer とか使えば、テストを実行してしばらくしたら勝手にこっちの方が何％優れてるよーって教えてくれるんですけど、今回のケースだと GWO の実装が難しかったので  Google Analytics で指標を読み取ることにしました。

やりたいことはですね。手元にあるデータは施策前後の１週間毎のコンバージョン率（8週間分）がありますんで前後8週間の平均CV率を出して何％改善したのか確認したいわけです。で、今回の場合1%程度改善されたのですが、これって別になんにもしなくても1%上がっちゃったりするのか、それとも偶然ではない[有意](https://ja.wikipedia.org/wiki/%E6%9C%89%E6%84%8F)の差なのかってことを理解しようと思います。

__施策前後8週間のコンバージョン率の遷移__

|        | 1W     | 2W     | 3W     | 4W     | 5W     | 6W     | 7W     | 8W     |
|--------|--------|--------|--------|--------|--------|--------|--------|--------|
| Before | 93.82% | 93.83% | 93.23% | 93.65% | 93.99% | 93.65% | 93.95% | 94.37% |
| After  | 94.73% | 94.77% | 94.18% | 94.71% | 94.99% | 94.76% | 94.45% | 94.59% |


## まずはじめに

はい、大学で統計学の単位を取ったような気もしないわけでもないそうゆう気もしないわけでもないという感じなので、ほぼ統計的知識ゼロです。間違いなどあれば指摘してもらえると嬉しいです。

手始めに『有意差』とかでググッてみるのですが、出てくるリソース読んでもさっぱりなので、というか数式とか見た瞬間拒絶反応がでてくるのでウォームアップがてらこの本読んでみました。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274065707/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51EFK1XNQ5L._SL160_.jpg" alt="マンガでわかる統計学" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274065707/warikiru-22/" name="azlinklink" target="_blank">マンガでわかる統計学</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.6.19</div></div><div class="azlink-detail">高橋 信,トレンドプロ<br />オーム社<br />売り上げランキング: 1287<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274065707/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>


文系の僕でも数時間で苦なく読めました（ちゃんと理解はしてないけど）。やっぱり僕みたいなトーシローが最初からガチな統計本 or ドキュメントに手を出すのは玉砕必死です。こうゆうので耐性をつけてから望んだ方が良かったです。

はい、ということでもう一度トライしてみましょう。なんということでしょう。読める、読めるぞ！ってほどでもないけども、以前よりは頭に入っていきます。

## 有意差検定

そうゆうことでググリマックってたらどうやら僕がしたいのは__t検定__という奴っぽいです。

> 2組の標本について平均に有意差があるかどうかの検定などに用いられる。


Yeah!これこれ！で、さらにググリマックってたらドンピシャなリソース発見！検索した中でも一番文系フレンドリーで分かりやすそうです

+ [4.3　t検定 - ハンバーガー統計学](http://kogolab.jp/elearn/hamburger/chap4/sec3.html)

ここのサイトは本当に分かりやすいので、量もそんなには多くないので最初から全部読んでみるとよいと思います。

+ [ハンバーガー統計学にようこそ！](http://kogolab.jp/elearn/hamburger/)

さてどうやら、t検定を行う前段階として以下の2点を調べておく必要性がありそうなので、まずはそこから始めましょう。

さてどうやら、t検定を行う前段階として以下の2点を調べておく必要性がありそうなので、まずはそこから始めましょう。

+ __標本が正規分布に従うかどうか__
+ __標本の分散が等しいかどうか__

### Jarque-Bera 検定（標本が正規分布に従うかどうか）

t検定の wikipedia には正規分布かどうか調べるためには、コルモゴロフ-スミルノフ検定やシャピロ-ウィルク検定使えばいいよと書いてあるけど、どれも難しくて（どうやって計算するのか）わからなかった。Jarque-Bera 検定ならなんとかできそうなので、この検定で調べてみる。

とりあえず、正規分布というのは

> 正規分布 - 平均を山の中心として左右になめらかに広がった「つりがね型」をした分布

[![Jarque–Bera test](/mol/images/2015/statics/02.png)](https://en.wikipedia.org/wiki/Jarque%E2%80%93Bera_test)

n：標本数、S：歪度、K：尖度

[歪度](https://ja.wikipedia.org/wiki/%E6%AD%AA%E5%BA%A6)（わいど, Skewness）- 分布の非対称性を示す指標 [尖度](https://ja.wikipedia.org/wiki/%E5%B0%96%E5%BA%A6)（せんど、Kurtosis）- 分布のとんがり具合を表す指標

Jarque-Bera 検定の公式が上記になるんですけど、どうやらこのJBの値がだいたい6より小さければ、[有意水準が5％で正規分布と見做して構わない](http://okwave.jp/qa/q4076739.html)らしいです。

はい、いろいろ分かんないことだらけだけど、とりあえず数値だしてみるよ。 nは8週間分あるから、8。歪度はExeclのSKEW関数を使えば出てくるよ！尖度はExeclのKURT関数を使えば出てくるよ！

|        | 標本数 n | 歪度 S  | 尖度 K | JB     |
|--------|---------|--------|--------|--------|
| Before | 8       | -0.118 | 1.4396 | 0.7094 |
| After  | 8       | -0.864 | 1.2489 | 1.5145 |


で、計算結果するとでどちらも6以下でおｋ。これでどうやら正規分布として見なしてもよさそうですね。

※ 尖度の定義 Jarque-Bera 検定の調べていると、（K-3）としている公式を見かけますがこれは尖度の定義による違いだそうです。wikipediaによると「Excelの分析ツール等は正規分布の尖度を0としている」らしいので、今回の場合は、-3する必要性はなさそうです。

### F検定（標本の分散が等しいかどうか）

よし、標本が正規分布だと分かった次は分散が等しいかどうかだ。

[![](http://kusuri-jouhou.com/images/statistics/aa3.gif)](http://kusuri-jouhou.com/statistics/fkentei.html)

こういった感じのことを調べるんだね。ちなみに、分散というのは

> 分散 - データが平均値を中心にして、どのくらいばらついているのかを示した数値 

※ 標準偏差（Standard Deviation） ＝ 分散の平方根（ルート）

[![分散](http://upload.wikimedia.org/math/d/5/2/d52d28bc57dff2e28bfa2ae195f1bd37.png)](https://ja.wikipedia.org/wiki/%E5%88%86%E6%95%A3#.E6.A8.99.E6.9C.AC.E5.88.86.E6.95.A3)

シグマが出てきてもうアカンΣ(´∀｀；)！ってなったかた大丈夫、数列の総和って意味だよ。要は、

```
((データ－平均値)の２乗)の総和÷個数
```

ってことを言ってるだね。今回は２つの標本（データ）があるので、それぞれ分散を求める。分散はExeclのVARP関数を使えば出てくるよ！

[![F-test](http://upload.wikimedia.org/math/1/a/f/1afdd4bd258e9b84c2a42d1a8f195c2e.png)](https://en.wikipedia.org/wiki/F-test_of_equality_of_variances)

分子に大きい方の値を当てはめて、F値を出しましょう。

|        | 分散 S | 
|--------|--------|
| Before | 0.09   | 
| After  | 0.05   |

F値は`0.09/0.05`の1.8になります。あとは以下の公式に当てはめていくと・・・

> 自由度は分子の自由度df1＝n1-1、分母の自由度df2＝n2-1のF分布に従う。自由度が求まったらF分布表からFαを求めることができる。

> ・判定1≦F≦Fαのとき、P＞0.05となる→帰無仮説を棄却できない→等分散である。― [F検定 (等分散の検定)](http://kusuri-jouhou.com/statistics/fkentei.html)

df1, df2の自由度はどちらも8-1で、7となり、F分布表より、7×7の場所は3.79となり、1≦1.8≦3.79 が成り立つ、つまり等分散と言えることができます。

## t検定（Student’s t-test）

２つの標本は正規分布に従い、等分散と言えるのでようやくt検定としけこみたいところですが、もう一つだけ確認しておきたいことがあります。

### 対応の有無

標本の対応の有無というのは、2つの独立した母集団から標本を選んでくるのか、1つの母集団から標本を選んでくるのかということです。今回の場合、施策したサイトのユーザーの期間比較ですので、施策前後で同じユーザーというのは可能性が低いので、対応はないと判断しました。

### 対応のないt検定

ようやく、ほんとようやくです。ここまできたらあとは以下の資料を元に進めてくだけです。

1. 帰無仮説を立てる
2. 帰無仮説の否定である対立仮説を立てる
3. 有意水準を決める
4. 得られた標本を使って、指標tを計算する
5. 標本の数から自由度を計算する
6. t分布表の該当する自由度を見て、tが棄却域にはいっている（棄却）か、いない（採択）かを判定する
7. 結論を決める

#### 1. 帰無仮説を立てる

帰無仮説というのは「差はない」という仮説らしいです。この場合、「施策前後で差はない」という仮説を立てます。

#### 2. 対立仮説を立てる

帰無仮説とは反対の仮説であり、「施策前後で差がないとはいえない、つまり、差がある」という仮説を立てます。

#### 3. 有意水準を決める

どの程度の正確さをもって帰無仮説を棄却するのかという水準です。たいていは厳しくて1%、少し甘くて5%だそうなので、今回は5%とします。

#### 4. 指標tを計算する

```
t = (標本平均の差) / SQRT (( Aの不偏分散 / Aの標本数) + (Bの不偏分散 / Bの標本数))
```

これに当てはめていけばいいんだす！めんどくハンバーガー統計さんのとこにEXCELシートありますんで、そこに当てはめていけばでます。

> 不偏分散 - 母分散の推定値 = ((データ－平均値)の二乗)の総和 ÷(個数 - 1)

※ SQRT関数は平方根（ルート）を求める関数です！

よって、t値は-5.78

#### 5. 自由度を計算する

```
自由度 = (Aの標本数 - 1) + (Bの標本数 -1) = Aの標本数 + Bの標本数 - 2
```

A,Bも標本数8なので自由度は14です。

#### 6. 棄却か採択か

![](http://t32k.me/static/blog/2011/02/t.png)

#### 7. 結論を決める

自由度が14のとき、有意水準5% 2.145, 有意水準1% 2.977となります。これをt分布で表すと上記のようなグラフになります。今回の場合、t値は-5.78となり棄却域に入ります。

よって、最初に立てた帰無仮説は棄却され、施策前後で差がないとはいえない、つまり、差があると言えます。

はい、できたー！そらできたー！やたー！

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00DJ0Y7F2/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/510I1hBHTSL._SL160_.jpg" alt="完全独習　統計学入門" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00DJ0Y7F2/warikiru-22/" name="azlinklink" target="_blank">完全独習　統計学入門</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.6.19</div></div><div class="azlink-detail">小島 寛之<br />ダイヤモンド社<br />売り上げランキング: 1164<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00DJ0Y7F2/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

なんとかできたけど、細かいこと全然わかってないのでもう少し勉強しようと思いました(；´Д｀)

有意な差があると言えると証明できたけど、それが今回行った施策によるものかっていう点はまた別問題なので気をつけてください。
