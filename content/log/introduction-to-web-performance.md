---
date: 2009-11-29
title: ウェブサイトパフォーマンス入門
subtitle: Introduction to Website Performance
categories: 
    - report
excerpt: 大企業で行われているノウハウを自分たちの仕事へ応用出来るレスポンスの改善方法を紹介します。
ogimage: http://www.websiteoptimization.com/speed/tweak/average-web-page/growth-average-web-page2014.png
---

<iframe src="//www.slideshare.net/slideshow/embed_code/658403" width="510" height="420" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>

+ [Web Directions East 2009 ワークショップ](http://east.webdirections.org/wde/2009/workshop/#nicole-sullivan)

## Nicole Sullivan （ニコール・サリバン）

3000以上にも昇る大規模サイトの最適化に携わって来た Nicole Sullivan は、現在 Yahoo! のパフォーマンスエンジニアと最適化のエバンジェリストとして国内外のセミナーで講演。Webサイトに関する研究だけでなく、プロジェクト管理もこなすマルチタスクなリーダーシップを発揮。フロントエンドエンジニアとしての高いスキルを持つ。

+ [Stubbornella](http://www.stubbornella.org/content/)
+ [Nicole Sullivan (@stubbornella) | Twitter](https://twitter.com/stubbornella)
+ [Nicole Sullivan | SlideShare](http://www.slideshare.net/stubbornella)


## なぜパフォーマンスについて話すのか？

### 速い方が良い！

速くて困ることは特にない

### サイトは年々巨大化している

[![](http://www.websiteoptimization.com/speed/tweak/average-web-page/growth-average-web-page2014.png)](http://www.websiteoptimization.com/speed/tweak/average-web-page/)

現在のサイトはWebページというよりもアプリケーション化していて複雑になってきている2003年頃に比べ、ページサイズは3倍になっている。

ユーザーにとってはWebアプリケーションもDesktopアプリケーションも同じ。 どちらも同じ性能を求められる。

### 時は金なり

+ Amazon : +100ms 売上が1%落ちる
+ Yahoo! : +400ms 完全にページをローディング（full-page traffic）するユーザーが5-9%減る
+ Google : +500ms 検索数が20%落ちる

> Shopzilla : -3.5sec CVは7-12%, PVは25%アップした

[Shopzilla's Site Redo - You Get What You Measure: Velocity 2009 - O'Reilly Conferences, June 22 - 24, 2009 - San Jose, CA](http://velocityconf.com/velocity2009/public/schedule/detail/7709)

> パフォーマンスが良いと思うユーザーほどページを多く見る(つまり広告収入への影響が大きい) (最も遅く感じているユーザーでPVが多いのはなぜ？　Nicole見解：ダイアルアップ接続ユーザーでもともと遅いのに慣れているのかも)

[The Secret Weapons of the AOL Optimization Team: Velocity 2009 - O'Reilly Conferences, June 22 - 24, 2009 - San Jose, CA](http://velocityconf.com/velocity2009/public/schedule/detail/7579)

50ms, 200ms, 500ms, 1000ms で遅くする実験 左からユーザー当たりのクエリ数、クエリを変えて検索した数、ユーザー当たりの収益、ページをクリックしたかどうか、満足度、クリックするまでの時間 50msでは統計的な違いは出なかった 遅延時間が長いほど満足などの指標は減少する 遅くなれば遅くなるほど思考が止まる（自分が何をしたかったのか、いちいち思い起こす必要がある）

レンダリングの見せ方による影響について ヘッダーだけでもいいから何か見せておくことでユーザーに安心感を与える （検索を多くするユーザーほど効果的）

![](http://cdn.oreillystatic.com/radar/images/2009/06/200906221738.jpg)

パフォーマンスの悪さが続けば、UX低下に深刻なダメージを与える。 （7週間目に元に戻すが4週間立っても元のレベルに回復していない）

+ [Bing and Google Agree: Slow Pages Lose Users - O'Reilly Radar](http://radar.oreilly.com/2009/06/bing-and-google-agree-slow-pag.html)

パフォーマンスについてユーザケアする必要がある

### 開発理念　Web Dev Philosophy

フロントエンドエンジニアとデザイナーのコミュニケーションをいかに円滑にするか重要 （エンジニア、デザイナー双方が歩み寄って理解する必要がある）

### 9つのベストプラクティス

#### 1. コンポーネント化する

PSDファイルのコンポーネント化、ライブラリ化する(デザイナーが辞めても他のデザイナー対応できる)

コンポーネントはレゴに似てる コンポーネントの利点：再利用でき、ブラウザキャッシュを利用できる ページ全体からデザインするのではなく、コンポーネントからデザインしてそれを組み立てるのが良いのではないか （この考え方は海外でも新しい）

Facebookコンサルの話： Facebookは既存サイトで、最初からコンポーネントを意識して開発したわけではない 要素をカタログ化することから始めた

細かいデザインの違いによるパフォーマンス低下は極力避ける レゴ化して見比べる もし、同じページに2つの似たようなモジュールがあるのならば、ひとつにまとめる

#### 2. サイト全体で一貫性を保つ

Consistency（一貫性） ルールが多ければ多いほどデザインは崩れていく 長期スパンでパフォーマンスはゆるやかに落ちていく（危険性を感じないので厄介）

#### 3. 透過デザインモジュールを使う

利点：拡張性に対応できる、コンポーネントを組み合わせることができる 弱点：複数の背景だと使えない、それ専用のモジュールを別途作らなければならない

#### 4. 画像とCSSスプライトの最適化

Yahoo!の例：[http://a.l.yimg.com/a/i/us/sch/gr4/srp_metro_20090910.png](http://a.l.yimg.com/a/i/us/sch/gr4/srp_metro_20090910.png)

ページ内の全ての画像をスプライト化 デザインパターンが１つだけだから可能（検索画面だけ）

スプライトするためには以下の3つから2つしかとれない

ページ数、メンテナンス性、最適化 （ex：より多くのページ数を最適化したければメンテナンス性はあきらめるしかない）

拡張性を考えてスプライトする ボタンは背景画像にして中身をテキストで変更 （日本語は汚くなるから考えもの）

パフォーマンスで重要な3つのこと

+ HTTP requests
+ Size of image
+ Size of the CSS

角丸を表現するためにはHTTPリクエストが4つ必要 リクエストが2倍になれば、CSSコードも2倍に

__画像の最適化__

1. 似たような色でまとめる（スプライトの話）
2. スキマを詰める（モバイル環境を見越すと、ちょっとでもダメ）
3. CSSスプライトの画像は縦より横に並べるの方がほんのちょっとだけいい(横に読み込んでいくらしい)
4. 等倍で見たときの色を減色
5. 個々の画像を最適化してからスプライトする
6. アンチエイリアスは避ける（平行四辺形はきつい）
7. 斜めのグラデーション画像は避ける（パフォーマンス的というよりモジュールの拡張性がない）
8. アルファフィルターは避ける
9. グラデーションの色は2-3px毎に変更していく

ロゴ画像のサイズ縮小だけは慎重に（無意識下で刷り込まれているので） マクドナルドのロゴは大統領よりも有名

フィルタはやめてよ！ ブラウザがフリーズする、メモリを大量消費する どうしても使いたければアンダースコアハックでIE6分岐

Alpha Image Loaderやめただけで100ms速くなったよ by Yahoo! Search

Progressively enhanced PNG8 より良いPNG画像を作るにはPhotoshopよりもFireworksが良い

画像圧縮の流れ Step1: デザイナーが『Web用に保存』などで減色する Step2: 画像のメタ情報を取り除く（画像のクオリティはそのまま）

#### 5. ブラウザに搭載されないフォントの使用は避ける

sIFR（Scalable Inman Flash Replacement）やJSで無理やり表現すればその分HTTPリクエストが増える

#### 6. 縦で考える

コンテンツは増えていくものなので仕方がない 横に合わせるのは難しい（jQueryなどJSで制御する必要があるため）

#### 7.ギラギラなデザインは慎重に

画像などを使って目立せることでコスト（パフォーマンス低下）がかかっていることを理解する

#### 8.フレキシブルに

拡張性を考えてデザインする コンテンツは横にも縦にも伸びる 横はグリッドでコントロール（縦は仕方ない）

#### 9.グリッドは重要です

上記に同じ

## アクティビティ

各自が選んだサイトがどのように改善できるか考えるワークショップ

パフォーマンスツールの紹介

+ [IBM Page Detailer](https://www.ibm.com/developerworks/community/groups/service/html/communityview?communityUuid=61d74777-1701-4014-bfc0-96067ed50156)
+ [WebPagetest - Website Performance and Optimization Test](http://www.webpagetest.org/)
+ [サイトパフォーマンス測定・改善　概要 | Gomez](http://www.gomez.co.jp/production/performance/index.html)
+ [Firebug :: Add-ons for Firefox](https://addons.mozilla.org/ja/firefox/addon/firebug/)

今回はFirebugを使う

Firebugの弱点 キャッシュしたのは計測しない（キャッシュクリアして使う） ブラウザのイベントモデルが表示される（実際のネットワークの流れではない）

最初からツールを使うのではなく、まずぺージ全体を見て考える

Flashの良い点：ユーザーの注意を引かせる Flashの悪い点：ロードには時間がかかる ユーザーの視点から考える

ページ下部のリクエストは遅延ロードで

パフォーマンス改善に当たっての考え方

+ どれくらい改善されるのか？
+ コストはどれくらいなのか？

## ワークショップを通して

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51GQNCMJsZL._SL160_.jpg" alt="続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" name="azlinklink" target="_blank">続・ハイパフォーマンスWebサイト</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.3.12</div></div><div class="azlink-detail">Steve Souders,武舎 広幸,福地 太郎,武舎 るみ<br />オライリージャパン<br />売り上げランキング: 396868<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

パフォーマンスについての小手先の技術を覚えたというよりも、パフォーマンスに対しての考え方が身につけられた一日ではないかと思う。Nicoleはエンジニア畑の人だけれども、デザインについて物を言うエンジニアだ。そのグラフィックは本当に必要なのか？そのデザインはほかのモジュールと似ているけれども１つにまとめられないのかなど問い正してくる。実際、アクティビティの時間では自分が制作したサイトを元にどのように改善できるのか指摘してもらった。Nicoleから見ればJSファイル容量の割にはJSの効果が見えないとのこと。（ページ内リンクにスムーススクロールとか使ってた）

Nicoleが考えるに、大半のユーザーはその機能を使わないだろう（使えなくても問題ない）し、目に見えない面でコストをかける必要性があるのかと聞かれた。確かに、そのサイトの大半のページがそれほど長くないのでマウススクロールで事足りるし、ページ内リンクを押す必要性もあまり感じられない。もし、気になるのならアクセス解析ツールなど使って実際に使われているのか調査してみれば良いと言われたので調査中。（たぶん外すと思う）

結局は重要なのは自分が行ったデザインの費用対効果がどうなのかという問題だ。Webページは気軽に修正・追加されがちだけど、その１枚のバナー画像を追加することでHTTPリクエストは増えるのだから確実にパフォーマンスコストがかかっていることを理解する必要性がある。そういったコストを超えるメリットが得られるのなら追加すれば良いが、何の考えもなしにあれやこれやとページの要素を追加していくことは非常に危険だと思う。

開発方法においても、最初から細かいチューニングをするよりも、まずページ全体を見て不必要なものがないか確認する方が効果的だということも覚えておかなければならない。フロントエンドのパフォーマンスについては昨年あたりから注目され始めてきてまだ成熟していない分野だと思うので、あまり瑣末なことにリソースを割かれるのも賢明ではない。














