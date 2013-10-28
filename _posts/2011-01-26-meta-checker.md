---
layout: post
title: Meta Checker
categories:
- javascript
tags:
- Greasemonkey
status: publish
type: post
published: true
meta:
  pvc_views: '3950'
  _edit_last: '1'
  _aioseop_description: "最近、もっぱらグリモンに夢中です。まさしくDo It Yourself! 精神まっしぐら、ネコまっしぐらです。\r\n\r\nで、こんなん作りました。"
  _wp_old_slug: ''
  _aioseop_keywords: javascript, dom, Greasemonkey
---
最近、もっぱらグリモンに夢中です。まさしくDo It Yourself! 精神まっしぐら、ネコまっしぐらです。

で、こんなん作りました。
<ul>
	<li><strong><a href="https://github.com/t32k/Meta-Checker">t32k/Meta-Checker - GitHub</a></strong></li>
	<li><a href="http://userscripts.org/scripts/show/94060">Meta Checker for Greasemonkey</a></li>
</ul>
<a href="https://addons.mozilla.org/ja/firefox/addon/greasemonkey/">Greasemonkey（ver 0.9+</a>）をインストールしたFirefoxで、meta_checker.user.js をクリックしてrawって書いてあるとこをクリックしたらインストールできます。すんませんが、今のところFirefoxでしか動きません。

右下のボタン押したら、TITLE要素やMETA要素を表示してくれます。またボタンを押したら非表示になります。あと、TITLEとDescriptionは文字数を、Keywordsはキーワード数をカウントしてくれます、こんな感じで。
<ul>
	<li><a href="https://github.com/t32k/Meta-Checker/wiki/Screen-shots">https://github.com/t32k/Meta-Checker/wiki/Screen-shots</a></li>
</ul>
事の始まりは、隣の人がSEOツールが欲しいとのことで作ってみたのです。
<ul>
	<li><a href="https://addons.mozilla.org/ja/firefox/addon/meta-description-title-on-top/">Meta Description &amp; Title on Top :: Add-ons for Firefox</a></li>
</ul>
初めはこれを使っていたのですが、UIが気に食わないとのことで、俺好みのものを作れという依頼でした。作ってみて思ったのは、やっぱり、人の為に何かを作るのはやりがいのあることだと思う（それがヒゲメガネのおっさんのためでも）。それもすぐにフィードバックがくる。嬉しい！また頑張る！って好循環になったかと思います。

<!--more-->

んで、なんかつまづいたことメモ。
<h2>ツマぶきな点</h2>
母性本能をくすぐる笑顔ですかね。実はこれが初めてのグリモンでしてかなり手間取りました。
<h3>基本的なグリモンのお作法</h3>
まぁ、ここ見れば基本的な流れが分かるかと思います。
<ul>
	<li><a href="http://gihyo.jp/dev/feature/01/greasemonkey">特集：Greasemonkeyによるアプリケーション開発｜gihyo.jp … 技術評論社</a></li>
</ul>
<pre><code> // ==UserScript==
 // @name         スクリプトの名前
 // @namespace    名前空間
 // @description  スクリプトの内容
 // @author       スクリプト作成者
 // @version      バージョンナンバー
 // @include      実行するURL
 // @exclude      実行しないURL
 // @require      外部スクリプト
 // @resource     リソースの名前 リソースのパス
 // @icon         管理画面で表示するアイコンのパス
 // ==/UserScript==</code></pre>
<a href="Metadata Block - GreaseSpot">Metadata Block - GreaseSpot</a>

最初の最初は、まずメタデータを書きます。スクリプトの名前と名前空間（自分のWebサイトのURLとか）あとは実行するURLさえかけば、とりあえずは動きます。@requireを使えばjQueryを読みこめるので、結構楽になるのじゃないでしょうか（@requireはGoogle Chromeのほうでは作動しません（その場合、jQueryのコードを直に貼っつけるのも手ですｗ））。

んで、メタデータの下に実行するコードを書いていくんですけど、他の環境のことも考えて無名関数で囲っておいたほうがベター。
<pre><code>(function(){
    // 処理内容
})();</code></pre>
<a href="http://efcl.info/adiary/Greasemonkey%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%88%E5%85%A8%E4%BD%93%E3%82%92%E7%84%A1%E5%90%8D%E9%96%A2%E6%95%B0%E3%81%A7%E5%9B%B2%E3%81%86%E6%84%8F%E5%91%B3">Greasemonkeyスクリプト全体を無名関数で囲う意味 - prog*sig</a>
<h3>querySelector</h3>
はい、じゃ、コード作ります。やりたいことは、非表示になっているTITLEやMETAを取ってきて表示させるってことですから、まず、TITLEやMETA要素を取ってきましょう。

ってことで、グリモンがなぜおもしろいのかというと、IEのことを考えなくていいんでよね。FirefoxもしくはChromeのような頭の良い子のことだけを考えればいいわけで、当然新しい技術が使い放題です。

querySelectorはIE8以上の対応ですが、Fxでも普通に使えます。これが使えるとなにが楽かってゆうと、jQueryみたいにCSSセレクタ形式でDOMを取ってこれるわけです。はいこれで、jQuery使わなくてもイケルかもって思ってきました。
<blockquote>便利なものはたいていコストが高いです!  By os0xせんせ

<a href="http://t32k.me/mol/2011/01/live-or-static/#div-comment-1155">http://t32k.me/mol/2011/01/live-or-static/#div-comment-1155</a></blockquote>
ってことで、パフォーマンスも気をつけましょう。
<h3>GM_addStyleとE4X</h3>
んで、要素が取れたらページ上に表示用の要素を作って入れ込めばいいわけです。ここで、私デザイナーなのでちょっと見た目にはこだわりたいんですよ。表示してはい終わりじゃ嫌なんですよ。元々のクライアントの要望もUIを変えてくれってことでしたので、CSSをバリバリ当て込んでいきたいわけですけど、グリモン上でCSSってどうやって書くの？ってことなんですが、
<ul>
	<li><a href="http://wiki.greasespot.net/GM_addStyle">GM_addStyle - GreaseSpot</a></li>
</ul>
はい、グリモンさんクールです。GM_addStyle関数なるもんがあります。この引数にスタイル書いていけばいいわけです。だけども、これ改行できないんですか？
<ul>
	<li><a href="http://wiki.greasespot.net/Multi_Line_Strings">Multi Line Strings - GreaseSpot</a></li>
</ul>
できますよーってことで、今回僕は一番使い勝手がよさそうなECMAScript for XML (E4X) で改行を試みました。（chromeはE4X対応してないので動かなくなります。）

これで、デザイナーの力量発揮ですね。CSS3でグラデーションとか透明とか指定しちゃいましょう。IE のことは考えなくていいのです。はい、楽しくなってきました＞＜

でも、試しに動かしてみると、実行するページのCSSとバッティングしたりしてうまく表示できないことがありました。あたい干渉されたくない！ってことでググッたらこんなんでてきました。
<ul>
	<li><a href="http://efcl.info/2010/0328/res1636/">Greasemonkeyでサイト既存CSSの影響を受けないポップアップパネルを作る方法 | Web scratch</a></li>
</ul>
表示する要素をiframe内に入れることで、影響を受けないようにしてくれます。COOL! これを拝借しました。ありがとうございます。
<h3>GM_*ValueとlocalStorage</h3>
はい、次は表示/非表示の設定の永続化にチャレンジしました。最初の段階では、メタ要素は表示しっぱなしで非表示にしてもページ遷移すれば、また表示しっぱなしに戻ってしまいます。これクールじゃない。やっぱりちょっと距離を置きたいことも人間あるそういう時期もある。ということで、設定の情報をクッキーとかに持たせればいいんでしょうけど、やっぱりFirefoxでやっているわけですからlocalStorageとかゆうナウでヤングなもの使ってみましょう。いや使いたい。

localStorage自体は簡単な記述で書けるんですけど、あれなんか動かない？ちゃんとやってるよ！？と思ったら、こうゆう情報が
<blockquote>Greasemonkey上で動いている場合、localStorage.keyで値をとることができません

<span style="font-size: x-small;"><a href="http://d.hatena.ne.jp/h13i32maru/20100606/1275816792">Google Chromeでも動くユーザスクリプトを書くためのメモ - maru source</a></span></blockquote>
！

！！

！！！

3時間くらい悩んだのでこれくらいの驚きでした。グリモン嬢をなびかせるにはlocalStorage.keyではなく、localStorage.getItem(key)ってちょっとめんどくさいアプローチをしなければならないんですね。そんなん知りませんよヽ(｀Д´#)ﾉ ﾑｷｰ!!

てことで、ようやく動いたのですが、今度は期待した動きをしてくれない。
<blockquote>ただ、注意しなければならないのはWebStorageは同じオリジン(<a href="http://d.hatena.ne.jp/keyword/%A5%D7%A5%ED%A5%C8%A5%B3%A5%EB">プロトコル</a>、ドメイン、ポート)ごとにデータを保存するということです。オリジンを超えてデータを共有したりするのは無理ということです。その点GM_*Value系はスクリプトごとにデータを保存するので少し使い勝手が落ちてしまいますが、まあ良しとしましょう。

<span style="font-size: x-small;"><a href="http://d.hatena.ne.jp/h13i32maru/20100606/1275816792">Google Chromeでも動くユーザスクリプトを書くためのメモ - maru source</a></span></blockquote>
！なんと、まぁこれは予想できたのですが。つまり、非表示にしていてもほかのドメインのサイト行ったらまた表示の設定に戻っちゃうわけなんですね。ってことで、やっぱりグリモンのGM_*Value関数を使って設定の永続化を実装しました。
<h2>まとめ</h2>
ということで、あーだーこーだー言ってきましたが、初めてのグリモンでしたがなんとなくそれっぽいもんができました！完成品だけを見れば、お！こいつすげーんじゃね？ってJavaScriptをやらないWebデザイナーさんは思ったりするのかもしれないけど、実際はなんもできなくて、何百回と失敗してようやくたどり着いたってところがあります。結局、やる気とガッツと少しのググる力があればなんとかなるもんです。んで、ちょっとづつ成長していけばいいんじゃないかな。なによりも自分の作ったもので人の役に立つのは素晴らしいことだと思う。
