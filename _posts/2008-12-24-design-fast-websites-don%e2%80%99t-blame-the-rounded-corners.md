---
layout: post
title: Design Fast Websites (Don’t Blame the Rounded Corners)
categories:
- performance
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2008/12/design-fast-websites-dont-blame-rounded.html
  pvc_views: '2450'
  _edit_last: '1'
---
<a href="http://www.atmarkit.co.jp/news/analysis/200812/22/chrome.html">Chromeはなぜ速いのか － ＠IT</a>の記事が話題になってて、少し内容がリンクしていたので、紹介。<a href="http://journal.mycom.co.jp/articles/2008/01/29/yslow/">YSlow</a>でおなじみのYahoo! Performance Teamのスライドです。

<iframe style="border: 1px solid #CCC; border-width: 1px 1px 0; margin-bottom: 5px;" src="http://www.slideshare.net/slideshow/embed_code/658403" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" width="427" height="356"></iframe>
<div style="margin-bottom: 5px;"><strong> <a title="Design Fast Websites" href="http://www.slideshare.net/stubbornella/designing-fast-websites-presentation" target="_blank">Design Fast Websites</a> </strong> from <strong><a href="http://www.slideshare.net/stubbornella" target="_blank">Nicole Sullivan</a></strong></div>
<a href="http://yuiblog.com/blog/2008/12/23/video-sullivan/">YUI Theater — Nicole Sullivan: "Design Fast Websites (Don’t Blame the Rounded Corners)"</a>より

パフォーマンスに関するデザインの話っぽいので、食いつきましたw
まず、なぜパフォーマンスを意識しなければならないのか？
ということに関して3つの理由を挙げています。
<ul>
	<li>Because fast is better</li>
	<li>Because sites are bigger</li>
	<li>Time is money</li>
</ul>
1つ目は、速いは正義ですね。ウェブを速く表示することで誰も困らないですしね。
2つ目は、年々ウェブサイトは大容量化してるそうです。Ajaxを使ったウェブアプリケーション、ディスプレイの大型化に伴うサイトのワイド化など考えられます。
3つ目、時は金なりということで、以下のようになってます。
<ul>
	<li>+100ms Amazon : 1% drop in sales</li>
	<li>+400ms Yahoo! : 5-9% drop in full-page traffic</li>
	<li>+500ms Google : 20% fewer searches</li>
</ul>
アマゾンで0.1秒遅くなれば、1%売り上げが落ち、
ヤフーで0.4秒遅くなれば、全ページで5~9％のトラフィックが減少し、
グーグルで0.5秒遅くなれば、検索数が20%落ちるそうです。

ウェブ開発の理念としては、
<ul>
	<li>デザインに敬意を払って作業をしなさい。
Work out of respect for the design.</li>
	<li>デザイナーは私たちのコードを内側から見たとき同じくらいに美しく巧みなビジュアルにしてくれる。
Designers make our code as beautiful and clever on the outside as it is on the inside.</li>
	<li>元のデザインのビジョンを尊重しなさい。
（一貫したデザインはクリーンなコードを生み、それがサイトを早くする）
Respect the original design vision. consistent design = clean code = fast site.</li>
</ul>
などのようなことを挙げられています。
嬉しい反面デザイナーとして責任重大です＞＜

9つの実践としては、
あんまりというかほとんど聞き取れなかったので、話半分に。

<strong>1. スマートなオブジェクトのコンポーネントライブラリを作りなさい。</strong>
Create a component library of smart objects
これは、そのままですね。レゴを作るかのようにモジュールを決めて、
冗長性を避けることですね。

<strong>2. セマンティックなスタイルを一貫して使用しなさい</strong>
Use consistent semantic style
意味に即したスタイルを指定しなさいということかな。
見出しなのに、10pxなんてありえないだろみたいな。

<strong>3. 透明になるように（内部で）モジュールをデザインしなさい。</strong>
Design modules to be transparent on the inside
透過画像を使ってうまくデザイン要素を組み合わせることですかね。

<strong>4. 画像の最適化と(CSS)スプライト</strong>
Optimize images and sprites
この辺は<a href="http://smushit.com/">smush it!</a>なんか使って画像を最適化しろみたいな内容です。

<strong>5. 非標準のブラウザのフォントを避けなさい</strong>
Avoid non-standard browser fonts
これはブラウザに搭載していないフォントを使いたいがために画像で書き出すことをやめろというのか、それともほんとに、font-familiyでマニアックな書体を指定するなってことかな。よく聞き取れませんでした。

<strong>6. 行よりも列（コラム）を使用しなさい</strong>
Use columns rather than rows
これも、CSSでは縦のラインは合わせられるけど、水平ライン（ボックスの高さ）を合わせようとしたら、JavaScriptとか使わなきゃいけないから、コラムレイアウトの方がいいよーみたいなことだと思う。

<strong>7. キラキラなデザインは慎重に採用しなさい</strong>
Choose your bing carefully
いわゆる Web 2.0 的なグラデーションを多用すれば画像サイズも膨らむし、本当にターゲットとしたユーザーが必要としているのか考えるべき。

<strong>8. フレキシブルに＜</strong>
Be flexible.
フレキシブルに＞

<strong>9. グリッドを愛することを学びなさい。</strong>
Learn to love grids
グリッドレイアウトの方が、コンテンツの追加・削除が容易なんだと思う。
それで、コードをクリーンに保てるんだと思う。
とまぁ、こんな感じの内容のプレゼンです。
興味のある人、英語のできる人は詳しい内容教えてくだされ～
