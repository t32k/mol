---
date: 2013-04-08
title: CSSプロパティの継承：inherit
categories: css
---

<p style="text-align: center;"><img class="aligncenter size-full wp-image-4776" title="listviews" src="/static/blog/2013/04/link.png" alt="" width="860" height="450" /></p>
最近のスマホサイトとかコーディングしてるとこーゆうリストビューのコンポーネントをよくマークアップする。リストのひとつの項目全体がタップエリアで遷移したりなんかアクションしたりする。

こーゆのコーディングするとなると、ul &gt; li &gt; aでaをblock要素にしたりする。そんとき、上記の普通のテキスト文もリンクテキストになってしまって、いわゆる青色の下線テキストリンクのようなスタイルになってしまう。
<pre><code> body { color: black; } a { color: blue; } </code></pre>
下線付きとは言わなくてもまぁたいていリセットの段階で基本的なリンク色を設定してると思う。
<pre><code> ul li { color: gray; } </code></pre>
それじゃいけないってもんだから、ul &gt; liにグレーの文字色を定義したりする。『あれ？青色のままじゃん？あ、そうだaのcolorは継承しないんだったー』ってことが疲れてるとよくある。
<pre><code> ul li, ul li a { color: gray; } </code></pre>
だもんで、めんどくさいけど、こんなことしてた（aで包まない時にも文字色を維持するため）。なんかこれは単純な例だけど、もうちょっと複雑になると、詳細度の兼ね合いとかめんどくさくなってくる。しかしまぁよくよく考えたら、継承させればいいんだよねってことで、ここでinheritさんの登場だ。
<pre><code> a { color: inherit; } ul li { color: gray; } </code></pre>
こうしとけば、 ul &gt; li &gt; aは、グレーの文字色を継承する。inheritなんて初めて使っただよ。（<a href="http://jigokuno.com/?eid=943">やっべー、CSS3ばっか使ってinherit使ってこなかったわー。ほら俺ってCSS3ばっか使っちゃうからー</a>）

スマホサイトはタップエリアを大きくするためにblock化して、aに多くの内容物が放り込まれるきらいがある。だもんで、aも通常のspanとかdiv感覚に扱うようになってきから、継承させたほうがなにかと都合が良い気がする。そのほうが素直な気がする。

とおもったの(´・ω・`)
<ul>
	<li><strong><a href="http://snook.ca/archives/html_and_css/inheriting_link">Inheriting Link Colour - Snook.ca </a></strong></li>
</ul>
