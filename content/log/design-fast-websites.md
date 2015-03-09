---
date: 2008-12-24
title: Design Fast Websites
subtitle: Don’t Blame the Rounded Corners
categories: performance
excerpt:
ogimage:
---

『[Chromeはなぜ速いのか](http://www.atmarkit.co.jp/news/analysis/200812/22/chrome.html)』の記事が話題になっていて、少し内容がリンクしていたので紹介する。YSlowでおなじみのYahoo! Performance Teamのスライドだ。

<iframe src="//www.slideshare.net/slideshow/embed_code/658403" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>

パフォーマンスに関するデザインの話なので、興味があった。まず、なぜパフォーマンスを意識しなければならないのか？ということに関して3つの理由を挙げている。

+ Because fast is better
+ Because sites are bigger
+ Time is money


1つ目は、速いは正義。Webを速く表示することで誰も困らない。 2つ目は、年々Webサイトは大容量化してるそうだ。Ajaxを使ったWebアプリケーション、ディスプレイの大型化に伴うサイトのワイド化など考えられる。 3つ目、時は金なりということで、以下のようになっている。

+ +100ms Amazon : 1% drop in sales
+ +400ms Yahoo! : 5-9% drop in full-page traffic
+ +500ms Google : 20% fewer searches

Amazonで0.1秒遅くなれば、1%売り上げが落ち、Yahoo!で0.4秒遅くなれば、全ページで5~9％のトラフィックが減少し、 Googleで0.5秒遅くなれば、検索数が20%落ちるそうだ。

Web開発の理念としては：


+ デザインに敬意を払いなさい
+ デザイナーは私たちのコードを内側から見たときと同じくらいに美しく巧みなビジュアルにしてくれる
+ 元のデザインビジョンを尊重しなさい（一貫したデザインはクリーンなコードを生み、それがサイトを早くする）

などのようなことを挙げられている。

9つの実践としては、 あんまりというかほとんど聞き取れなかったので話半分に。

#### 1. スマートなオブジェクトのコンポーネントライブラリを作りなさい

これはそのままだね。レゴを作るかのようにモジュールを決めて冗長性を避けるってこと。

#### 2. セマンティックなスタイルを一貫して使用しなさい

意味に即したスタイルを指定しなさいということかな。見出しなのに、10pxなんてありえないだろみたいな。

#### 3. 透明になるように（内部で）モジュールをデザインしなさい

透過画像を使ってうまくデザイン要素を組み合わせることかな。

#### 4. 画像の最適化とCSSスプライト

この辺はsmush it!なんか使って画像を最適化しろみたいな内容。

#### 5. 非標準のブラウザのフォントを避けなさい

これはブラウザに搭載していないフォントを使いたいがために画像で書き出すことをやめろというのか、それともほんとに、font-familiyでマニアックな書体を指定するなってことかな。よく聞き取れなかった。

#### 6. 行よりも列（コラム）を使用しなさい

rows これも、CSSでは縦のラインは合わせられるけど、水平ライン（ボックスの高さ）を合わせようとしたら、JavaScriptとか使わなきゃいけないから、コラムレイアウトの方がいいよーみたいなことだと思う。

#### 7. キラキラなデザインは慎重に採用しなさい

いわゆる Web 2.0 的なグラデーションを多用すれば画像サイズも膨らむし、本当にターゲットとしたユーザーが必要としているのか考えるべき。

#### 8. フレキシブルに

#### 9. グリッドを愛することを学びなさい

グリッドレイアウトの方がコンテンツの追加・削除が容易なんだと思う。 それでコードをクリーンに保てるんだと思う。 

とまぁ、こんな感じの内容のプレゼン（適当）...

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51GQNCMJsZL._SL160_.jpg" alt="続・ハイパフォーマンスWebサイト ―ウェブ高速化のベストプラクティス" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" name="azlinklink" target="_blank">続・ハイパフォーマンスWebサイト</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.3.9</div></div><div class="azlink-detail">Steve Souders,武舎 広幸,福地 太郎,武舎 るみ<br />オライリージャパン<br />売り上げランキング: 364143<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114462/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>











