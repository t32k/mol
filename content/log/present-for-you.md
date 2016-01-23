---
date: 2012-12-25
title: Sublime Text 2 のアイコンをなんとかする
categories: 
    - design
---

<strong><a href="http://www.adventar.org/calendars/20">Sublime Text 2 Advent Calendar 2012 </a></strong>
<blockquote>とりあえず作ってみました！
Sublime Text 2に関することであれば何でもOKです。</blockquote>
ということで、Advent Calendarでは与えられたテーマから外れた内容で記事を書くことに定評のある<a href="https://twitter.com/t32k">@t32k</a>がラストを飾ってやんよ(o°3°b)b

私、恥ずかしながらSublime Textのプラグインを作ろうと思ってもPythonもかけない最下級サブライムテキスター<span style="color: #888888;">(戦闘力・たったの５か・・ゴミめ・・・)</span>でして、そんな僕でもいつかはPythonとかRubyとかSublime Textで書きたいと思うわけです。そこで今はその悔しい気持ちをアイコンにぶつけるわけです。
<p style="text-align: center;"><img class="aligncenter size-full wp-image-4619" src="/static/blog/2012/12/st2.jpg" alt="st2" width="900" height="300" /></p>
ST2のアイコンですけど、まぁそんなに、いまいち、いわんや、それほど、ましてや、はたまた、それでいて、かっこよろしくないわけですね。なんだろう色かなぁ、角度？形状？S?

そんなわけで、こう思っているのは万国共通なのか「<a href="https://www.google.co.jp/search?hl=ja&amp;safe=off&amp;tbo=d&amp;q=sublime+text+icon+replacement&amp;oq=sublime+text+icon&amp;gs_l=serp.3.2.0j0i30l4j0i8i30l3j0i5i30l2.2066.2066.0.3949.1.1.0.0.0.0.123.123.0j1.1.0...0.0...1c.1.2aW1JbqCr-s">sublime text icon replacement</a>」なんかでググりますと、いろいろ出てきます。
<ul>
	<li><a href="http://blog.jerodsanto.net/2012/01/sublime-text-2-icon-replacement-roundup/">Sublime Text 2 Icon Replacement Roundup - Jerod Santo</a></li>
</ul>
世界中のデザイナーが作品を投稿するSNSサイト「Dribbble」でも検索してみるといろいろ出てきます。
<ul>
	<li><a href="http://dribbble.com/search?q=sublime+text"><strong>Dribbble - Show and tell for designers </strong></a></li>
</ul>
既存のアイコンをブラッシュアップしたもの、「S」をモチーフにしたもの、「Lime」をモチーフにしたもの、やたらシンプルなもの、いろいろです。ここで自分のお気に入りのアイコン、DLできるアイコンが見つかれば問題ないのですが、これじゃ満足できないなんでも欲しがる子はやっぱり自分で作るしか無いわけです。
<h2>The Icon</h2>
自分でSublime Textアイコンを作る前に、アイコンの予習をば。

<a href="/static/blog/2012/12/insta1.jpg"><img class="aligncenter size-full wp-image-4632" title="insta" src="/static/blog/2012/12/insta1.jpg" alt="" width="900" height="300" /></a>

なにごとも、最初からオリジナルなものを作るのは難しいです。プログラミングでもそうでしょ？最初は良いコードを写経するもんでしょ？なので、僕も勉強がてらinstagramのアイコンとか写経してみました。いろいろ詰めが甘いですが、光の付け方とかこーすればそれっぽく見えるんだなとか一回やってみるといろいろ勉強になります。
<ul>
	<li><a href=" http://iosicongallery.com/">iOS Icon Gallery | iOS Icon Design Gallery</a></li>
	<li><a href="http://app-icons.net/">APP icons </a></li>
</ul>
上記のサイトとか見てると綺麗なアイコンがいっぱいでテンションあがります。ただ、こういったところにあがっているものを最初から作れるわけないので（<a href="http://dribbble.com/shots/200993-Boxing-Glove-App-icon">こうゆうのとか</a>どっから手を付けたらよいかわかりません＞＜）、部分的にパクるとか、Psdtuts+などでは比較的簡単な、よく使われる表現のチュートリアルがあるので、そういったものをやってみて表現できるボキャブラリーを増やしていけばよいと思います。
<ul>
	<li>
<p style="display: inline !important;"><a href="http://psd.tutsplus.com/tutorials/icon-design/mobile-app-icon/">Create a Mobile App Icon in Photoshop | Psdtuts+</a></p>
</li>
	<li><a href="http://psd.tutsplus.com/tutorials/icon-design/create-a-camera-lens-icon-in-photoshop-screencast/">Create a Camera Lens Icon in Photoshop – Screencast | Psdtuts+</a></li>
</ul>
<h2>Sublime Text Icon</h2>
<ul>
	<li><a href="https://github.com/dmatarazzo/Sublime-Text-2-Icon"><strong>dmatarazzo/Sublime-Text-2-Icon · GitHub </strong></a></li>
</ul>
さて、Sublime Textのアイコンを作っていきますか。幸いにもひな形というか、Sublime Textで必要となるフォーマットは上記のGitHubからフォークすることできます。なるほどデザインデータもGitHubで管理する時代ですかなるほど(・ω&lt;) ご丁寧にもPSDデータまであるので、見てみますと512pxサイズで作っておけばあと問題ない感じですかね。

個人的にはテキストエディタのアイコンなので、テキストブック...ブック....本( ・∀・)!!みたいなアイコンにしたいと思いました。

<a href="https://github.com/t32k/Sublime-Text-2-Icon"><img class="aligncenter size-full wp-image-4622" src="/static/blog/2012/12/icon1.jpg" alt="icon1" width="900" height="300" /></a>
<ul>
	<li><a href="https://github.com/t32k/Sublime-Text-2-Icon">https://github.com/t32k/Sublime-Text-2-Icon</a></li>
</ul>
最初に作ったのこれ。縫い目の表現をしたかったので個人的に満足したのですけれどもロゴマーク的（S）なものがしっくりきてないのと、iOSアイコンのテンプレートで作ってるのMac Appアイコンとして見てると少し平べったい印象です。

なんかもうちょっとモッコリしてみたいなと思ったのと、本の「地」みせた感じのあの表現やってみたいなと思ってぐぐってみるてると、見つけました。
<p style="text-align: center;"><a href="http://dmonzon.com/freebies/book-icon-template/"><img class="aligncenter size-full wp-image-4630" title="book" src="/static/blog/2012/12/book.jpg" alt="" width="900" height="300" /></a></p>

<ul>
	<li>
<p style="display: inline !important;"><a href="http://dmonzon.com/freebies/book-icon-template/ ">Book Icon Template</a></p>
</li>
</ul>
おお！アレアレ！ということですが、これをそのまま使うのは芸がないので変えてみましょう。なんかいいのないかなと思ったら手元に<a href="http://www.moleskine.co.jp/">某有名なメモ帳</a>があったのでこれを真似てみましょう。

なんでこんなにテカってる本なのでしようね、テクスチャを落ち着いたレザーに変えたいものです。
<ul>
	<li>
<p style="display: inline !important;"><a href="http://subtlepatterns.com/">Subtle Patterns | Free textures for your next web project</a></p>
</li>
</ul>
ということで、いつもテクスチャ系でお世話になってるのが上記のサイトでSubtleというだけあって主張し過ぎない、ギラつかない、いい感じのテクスチャがいっぱいあります。

<a href="https://github.com/t32k/Sublime-Text-2-Icon/tree/moreskine"><img class="aligncenter size-full wp-image-4623" src="/static/blog/2012/12/icon2.jpg" alt="icon2" width="900" height="300" /></a>
<ul>
	<li>
<p style="display: inline !important;"><a href="https://github.com/t32k/Sublime-Text-2-Icon/tree/moreskine">https://github.com/t32k/Sublime-Text-2-Icon/tree/moreskine</a></p>
</li>
</ul>
で、ちょいちいといじりますとこんな感じに出来上がりました。

あとは、出来上がったPNG形式の画像を下記サイトでicoやicnsに出力します。
<ul>
	<li>
<p style="display: inline !important;"><a href="http://iconverticons.com/online/  ">iConvert: ico、icns、pngアイコンをオンラインでWindows用、Mac OS X用、Linux用へと変換する</a></p>
</li>
</ul>
いかがでしたでしょうか？デザインってのそんなに難しくないですよね？いや難しいか... いや僕も絵とか書けないんですけど、最近のプログラミングみたいに便利なオープンソースフレームワークを使ってちゃちゃっとWebアプリケーションを作るような感じで、アイコンとかも便利な素材やチュートリアルがたくさん出回っているので、うまく活用してお気に入りのアイコンを作ってみたらいいんじゃないかと思います。
