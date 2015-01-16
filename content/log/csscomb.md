---
date: 2012-10-17
title: CSScomb
categories: css
---

<p style="text-align: center;"><a href="http://csscomb.com/"><img class="aligncenter size-full fig" title="csscomb" src="/static/blog/2012/10/csscomb.jpg" alt="" width="520" height="260" /></a></p>
うららかに晴れた秋の日、みなさんいかがお過ごしか？こんちわ @t32k だ。

今日は<strong><a href="http://csscomb.com/">CSScomb</a></strong>ってツールの紹介だよ。タネマキであった<a href="https://twitter.com/cipher">こもりさん</a>のSublime Text2勉強会のときに知ったんだけど、 まぁ、CSSプロパティを綺麗にソートしてくれるって代物だ。大まかな機能はこんな感じ。
<ul>
	<li>CSSプロパティのソート</li>
	<li>ソート順は設定可能</li>
	<li>&lt;style&gt;タグ、style属性もパースできる</li>
	<li>スタイルシートのフォーマットは変更しない(ホワイトスペースの除去とかしない)</li>
	<li>CSS2,3,4も完全にサポートしてる</li>
</ul>
<a href="http://csscomb.com/online/">オンライン</a>でも使えるし、Sublime Textだけじゃなくてメジャーなテキストエディタだったら、たいてい<a href="https://github.com/miripiruni/CSScomb/downloads/">プラグインが用意</a>されてるんだ。

<!--more-->

へー便利なものがあるなーと思ったけども、<a href="https://twitter.com/t32k/statuses/224069764396498944">Sassファイルでこのツールを実行するとそんときはバグってて</a>、単純にプロパティ順を綺麗にさせるためだけなのに、そんな致命的なバグの危険性（CSSが壊れる）とかマジ勘弁！などと思ったけど、あれから3ヶ月、俺もCSScombも成長したんだ。その話を聞いてくれ。
<h2>SassとCSScomb</h2>
まずは、Sass文法をうまく理解していなかった点。<a href="http://csscomb.com/tests/">Tests</a> を見てくれ。見てごらん綺麗な緑色してんだろ。これテストに合格してるんだぜ...ってことで、Sass関連のテストも今じゃパスしてる様子。@includeが消えたりするバグも僕の方でも確認できていない。YOSHI 合格だ。

ちょっとReal Filesでwarningがあるみたいだけど、Sassのパーシャルファイルとか見通しのよいファイル単位でCSScombしてあげれば問題があってもすぐ気づけるからまぁそこまでも気にしなくてもいいかなと思ってる。働いたら負けかなと思ってる。
<h2>gzipとCSScomb</h2>
次に、CSSプロパティのソートは自己満足か？ってこと。基本コードは綺麗なほうがいいに決まってるけどそれがユーザーに対してなんかしらのメリットがないと、どーも後押しが弱いなって感じです。順番ぐらいそこまでひどくない限り、特に問題になることもないと思う（よっぽど書き散らかしたときは別だけど）。そう思ってた時代も僕にはありました。
<ul>
	<li><strong><a href="http://t32k.github.com/speed/articles/gzip.html">gzip圧縮のしくみ | LPWS </a></strong></li>
</ul>
まずは↑こちらをご覧いただきたい。gzipってテキストファイルとかを圧縮する技術なんですが、これサーバー側の設定をちょいちょいとするだけの割りにはなかなかナイスーな効果を発揮してくれるパフォーマンス対策のひとつでもあります。これの仕組みなんですけど、要は同じような文字列を探してひとまとめとして考えるみたいなんですね。参照リンクの例ではそれぞれ別のhnタグと全部同じのdivタグの場合だと未圧縮の状態ではhnタグのほうが少ないバイト数ですが、gzip圧縮するとdivタグのほうが少ないバイト数になるんですね。divのまとまりがひとつとしてみなされてるみたいな感じですかね。

これはHTMLの例ですが、CSSの場合も同じような文字列がでてきますよね。たいていどのセレクタもmarginとかpaddingとかwidthとか含んでいます。こーいったプロパティの順番がセレクタごとにバラバラだったら同じような文字列としてカウントされないのでgzip圧縮効率も悪いんじゃねーの？って話です。

試しに、Apple Storeのbase.cssで実験してみましょう。別にApple StoreのCSSが汚いって言ってるわけじゃなくてある程度分量があったから良いサンプルかなと思ったのです。
<ul>
	<li><a href="http://store.storeimages.cdn-apple.com/6487/store.apple.com/rs/rel/base.css">http://store.storeimages.cdn-apple.com/6487/store.apple.com/rs/rel/base.css</a></li>
</ul>
<p style="text-align: center;"><a href="/static/blog/2012/10/b4.png"><img class="aligncenter  wp-image-4376" title="b4" src="/static/blog/2012/10/b4.png" alt="" width="520" /></a></p>
んで、素のbase.cssとCSScombをかけた奴。もともとminifyされてるから綺麗になったかどうかわかんないけど多分ソートされたのでしょう。なぜかCombしたほうがファイルサイズが大きくなってますが、重要なのはgzipされた状態でのサイズです。
<p style="text-align: center;"><a href="/static/blog/2012/10/a5.png"><img class="aligncenter  wp-image-4377" title="a5" src="/static/blog/2012/10/a5.png" alt="" width="500" /></a></p>
はい、これをgzipコマンドにかけてみるとどーでしょう！わお、400バイトほど軽くなってるじゃないですか！うそーまじー！！

はい。

gzip圧縮を想定してない場合意味ないとか、たった400バイトとか...そういった意見もあるかもしれないけど、ボタン1発でできるのならやったほうがいいよねと僕は思います。別に毎回やる必要もないし、ほんとデプロイの時に最後のひと手間かけてやるだけなんでみなさんもどーですかね。まさしくお出かけ前のCombですね！！
