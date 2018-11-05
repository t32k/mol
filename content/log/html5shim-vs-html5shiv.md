---
date: 2011-12-12
title: html5shim vs html5shiv
categories:
  - development
---

<a href="http://atnd.org/events/21980">JavaScript Advent Calendar 2011 (オレ標準コース) </a>12 日目の id:t32k です。去年も参加しましたがなんでもありと聞いて今年も懲りずに参加！

<a href="http://keycss.com/html5/html5shim-vs-html5shiv.html"><img title="Don’t lose any more time." src="/static/blog/2011/12/same.png" alt="Don’t lose any more time. html5shim and html5shiv are exactly the same thing."></a>

はじめに言っておきますが、html5shim も html5shiv どっちもまったく同じです。違いなんて無いので、こんなことに頭を悩ませる暇があったらさっさとコードでも書いてろ！以上！うんこ(・∀・)!

そんなこと言っても世の中結果じゃない、過程が大切だと思うんだ先生！ってことで今回は調べてみます。

html5shi(m|v)、めんどくさいので以下 html5.js は"HTML5 IE enabling script"の名の通り、IE8 以下で<em>article</em>などの新要素が正しく認識されずスタイル(CSS)がうまく適用されない問題を解決しそれらのブラウザでも利用可能にしてくれます。

```
document.createElement("article");
```

こんな感じに DOM で要素を生成すると、IE でも HTML5 の要素にスタイルを効くようになります。実際の html5.js はもっと複雑だけど基本的にはこんなことをやってます。詳しいことは下記スライド参照で。

- <a href="http://prog.re-d.net/demo/slide/20101218/index.html">HTML5.js の中身を見てみよう</a> by <a href="https://twitter.com/#!/kamiyam">@kamiyam</a>
  </ul>

## What's the difference?

そろそろ HTML5 でサイト作ってみっかーということでいろいろググってたら前述の問題に引っかかり、さらにググってみると同じ機能なのに名前が違う 2 つのスクリプトがあることを認識たのが今回の経緯です。

- <a href="http://code.google.com/p/html5shim/">html5shim - HTML5 IE enabling script - Google Project Hosting</a>
- <a href="http://code.google.com/p/html5shiv/">html5shiv - HTML5 IE enabling script - Google Project Hosting </a>
  </ul>
  Google Codeにホスティングされている2つのコードを見比べても全く同じです。謎です。

> **Common question:** what's the difference between the html5shim and the html5shiv?
> **Answer:** nothing, one has an m and one has a v - that's it.

と思ったら、似たような疑問を持つ人も多いのかよくある質問が用意されていました。

”違いなんて無いよ！片方は m で、片方が v なだけ。それだけ！”

```
&lt;!--[if lt IE 9]&gt;
 &lt;script src="/common/js/html5shiv.js"&gt;&lt;/script&gt;
&lt;![endif]--&gt;
```

※最近では Google Code にホスティングされているものを参照するのではなく、自鯖に落としてきて使用することが<a href="http://www.skyward-design.net/blog/archives/000134.html">推奨されています</a>。

お... また敷かれたレールを疑問も持たずに走ってればいいんだよ的な回答ですね。そんなの求めていないんだ！僕は！じゃーなぜ 2 つあるんだよ！どっち使えばいいんだよ！と遅れてきた反抗期によって僕はあきらめません。

まずは単語の意味から...

> 【名詞】【可算名詞】
> (ものを水平にしたり，すき間などに入れる)詰め木[金]
> <a href="http://ejje.weblio.jp/content/shim"> shim の意味 - 英和辞典 Weblio 辞書  </a>

> 【名詞】【可算名詞】
> 《米俗》 (ジャック)ナイフ
> <a href="http://ejje.weblio.jp/content/shiv"> shiv の意味 - 英和辞典 Weblio 辞書  </a>

ふむふむ、"shim" の方は詰め木ということで足りない機能を補完（カバー）する意味合いでも取れて、<a href="https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills">polyfill</a>みたいな感じですかね？。"shiv" はナイフ...どーゆこっちゃ＞＜

## The Story of the HTML5 Shiv

行き詰まり感たっぷりだったところに、<a href="https://t32k.me/mol/log/trackhtml5inga-with-modernizr/">Modernizr</a>  の開発者でも有名な Paul Irish さんが、<a href="http://paulirish.com/2011/the-history-of-the-html5-shiv/">The Story of the HTML5 Shiv </a>というドンピシャなタイトルの記事をあげていました。

この記事の前半部分をざっくりまとめてみると、

**2007 年くらい**
■ developers:
新要素に CSS 効かなくね？やばくねｗ？あれれｗｗ？

**2008 年**  
■ <a href="http://intertwingly.net/blog/2008/01/22/Best-Standards-Support#c1201006277"> Sjoerd Visscher</a>（初めてこのテクニックを披露した人）：
createElement したらええで〜ｗｗｗ

■ <a href="http://ln.hixie.ch/?start=1201080691&amp;count=1"> Ian Hickson</a>（HTML5 のエライ人）：
これマジパネェｗｗｗこれ使ったら IE7 の互換 shim 簡単に作れるわーｗｗｗｗ

■ <a href="http://ejohn.org/blog/html5-shiv/">John Resig</a>（jQuery 作った人）：
CSS 効かせる方法、HTML5 Shiv って名前つけたわーｗｗ（shim だけど）

**2009 年**
■ <a href="http://remysharp.com/2009/01/07/html5-enabling-script/"> Remy Sharp</a>（初めて html5.js をディストリビュートした人）：
HTML5 Shiv のやつ Google Code にホスティングしといたわーｗｗ

**2010 年**
■ <a href="http://code.google.com/p/html5shim/source/detail?r=2">Remy Sharp</a>：
html5shim でミラー作っておいたわーｗｗｗ

だいたいこんな感じですな。

## Shiv?

ここで問題なのは、なんで Remy Sharp さんあとから html5shim のミラーを 公開したのか？ということですね。

"shiv" って単語がコンピューター用語で言う互換性のため回避策といった意味が一般認識されていなかったのではないかという仮説が僕の中で湧いてきました。

試しに<a href="https://github.com/">GitHub</a>で <a href="https://github.com/search?q=shiv&amp;type=Everything&amp;repo=&amp;langOverride=&amp;start_value=1">"shiv" で レポジトリ検索</a>をしてみると 17 件、<a href="https://github.com/search?type=Everything&amp;language=&amp;q=shim&amp;repo=&amp;langOverride=&amp;x=0&amp;y=0&amp;start_value=1">"shim"で検索</a>すると 93 件ヒットしました。"shiv"  に関しては html5shiv に関しての内容ばかりで、他のものも新しいライブラリです。

<a href="http://ejohn.org/blog/html5-shiv/#comment-296934">2008 年の John Resig 氏のエントリのコメント</a>においても、「shim じゃなくて shiv?」といった内容が見受けられます。

しかし、Wikipedia の<a href="http://en.wikipedia.org/wiki/Shim_(computing)">Shim (computing)</a>の項目には、"a shim (from shim) or **shiv** is a small library which..."とまぁなんか互換性のため回避策の意味として記述されています...

え、そうなの？なんでじゃ！ということで、例によって反抗期の僕には<a href="http://en.wikipedia.org/w/index.php?title=Shim_(computing)&amp;action=history">wiki の変更履歴</a>を見てみるとありました。21:20, 16 November 2011‎ までは  Shim (computing)の項目に  "shiv"  って単語はなかった。なんだ最近、追記されてんじゃん！

まぁ少なくとも 2008 年の John Resig が書いたエントリの時点では "shiv" に「互換性のため回避策」といった意味がなかったのではないかと推測できます。

## Conclusion

で結局、**ここからは妄想**になるんだけど、

**2008 年**
■ <a href="http://ejohn.org/blog/html5-shiv/">John Resig</a>（jQuery 作った人）：
CSS 効かせる方法、HTML5 Shiv って名前つけたわーｗｗ
やってることは shim だけど、shiv の方が武器っぽくって強そうじゃんｗｗｗドヤｗｗ

■ developers1:
shiv じゃなくて shim だろｗｗワロスｗｗｗ

■ developers2:
html5shiv いいねｗｗｗｗｗイカスｗｗｗｗｗ

**2010 年**
■ <a href="http://code.google.com/p/html5shim/source/detail?r=2">Remy Sharp</a>：
html5shiv でホスティングしたったーけどｗｗｗｗ
html5shim の方が意味的に分かりやすいし一応こっちも作っとくかーｗｗ

そんな経緯ですかね...**”なぜ”**そうしたのかって部分が言及されて（見つから）なかったので、あくまで上記は僕の**妄想**ですからあしからず。知ってる人いたら教えてください。

てか、<a href="http://www.modernizr.com/download/">Modernizr にバンドリングされてる</a>し、そっち使ったらいいんじゃないっすかねー（by <a href="https://twitter.com/#!/5509">@5509</a>）

## 参考

- <a href="http://en.wikipedia.org/wiki/HTML5_Shiv">HTML5 Shiv - Wikipedia, the free encyclopedia </a>
- <a href="http://ejohn.org/blog/html5-shiv/">John Resig - HTML5 Shiv </a>
- <a href="http://remysharp.com/2009/01/07/html5-enabling-script/">HTML5 enabling script | remy sharp's b:log</a>
- <a href="http://paulirish.com/2011/the-history-of-the-html5-shiv/">The Story of the HTML5 Shiv « Paul Irish </a>
- <a href="http://en.wikipedia.org/wiki/Shim_(computing)">Shim (computing) - Wikipedia, the free encyclopedia </a>
