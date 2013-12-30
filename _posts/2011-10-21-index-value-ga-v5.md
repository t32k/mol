---
layout: post
title: GA Version5 のレポートでインデックス値みたいなものを確認したい！
categories:
- analytics
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '2565'
---
<a href="http://www.flickr.com/photos/treevillage/5296353933/"><img class="fig" title="Mikan five" src="/static/blog/2011/10/ga_v5.jpg" alt="" width="500" height="250" /></a>
<p style="text-align: right;"><span style="font-size: x-small;"><a href="http://www.flickr.com/photos/treevillage/5296353933/">Mikan five | Flickr - Photo Sharing! </a></span></p>
みなさんGoogle Analyticsしてますかー？わい？わいアナリティックしてるしてる。ということで表題どおりの内容のエントリです。巷じゃぁ、GAのレポート画面が刷新されてオサレな感じになってますが、やはり長年使ってた旧バージョンのレポートも恋しいです。しかし新しい恋人とこれからの新生活を始めようと最近では意識して使ってます。

<!--more-->

話は2ヶ月ほど前、第2回<a href="http://gatracker.org/">_gaTrackerミーティング</a>での<a href="http://www.slideshare.net/susumukatachi/20110824-gatrackerfinal">飯田進さんのセッション</a>でインデックス値が無くなったのは不便だという話をされていました。このときはまだ旧レポートを使ってたのでそーなんだーとしか思ってませんでしたけど、ときは経て、新バージョン使うようになってからは、やはりインデックス値を知りたい。てかなんでわからんの？って感じでいろいろ調べてみました。<del>どうやらインデックス値は<strong>平均目標値</strong>という名前に変わったようです。</del> (そうでないようです。両者の違いは下記から）
<ul>
	<li><a href="http://gaforum.jp/basic/term/984">Google アナリティクスの「平均目標値」とは | GA フォーラム </a></li>
	<li><a href="http://gaforum.jp/basic/term/957">Google アナリティクスの「$インデックス」とは | GA フォーラム </a></li>
</ul>
<p style="text-align: center;"><a href="/static/blog/2011/10/v4.png"><img class="aligncenter size-medium wp-image-3649 fig" title="v4" src="/static/blog/2011/10/v4.png" alt="" width="500" height="380" /></a></p>
<p style="text-align: center;"><span style="font-size: x-small;">v4 レポート：上位のコンテンツ</span></p>
ということでこのインデックス値の代用になるかと思い、平均目標値を確認できるレポートを作ってみました。ついでに、旧バージョンでよく使ってた<em><strong>コンテンツ &gt; 上位のコンテンツ</strong></em>っぽいカスタムレポートにしてみました。GAアカウントにログインした状態で下記リンクを踏んでもらうとカスタムレポートをインストールできます。
<ul>
	<li><strong><a href="https://www.google.com/analytics/web/permalink?type=custom_report&amp;uid=T2VS0LQ_R5GoaJKBiFGRVw">上位のコンテンツ：カスタムレポート</a></strong></li>
</ul>
<p style="text-align: center;"><a href="/static/blog/2011/10/v5.png"><img class="aligncenter size-medium wp-image-3650 fig" title="v5" src="/static/blog/2011/10/v5.png" alt="" width="500" height="421" /></a></p>
<p style="text-align: center;"><span style="font-size: x-small;">v5 レポート：カスタムレポート（上位のコンテンツ）</span></p>
これでインデックス値のように、ページの貢献度が分かるのかは微妙ですね。どうゆう計算でしてるのかまだ理解していないので引き続き調べてみます。

間違いを指摘してくださった衣袋さんありがとうございます。
<p style="text-align: center;"><a href="/static/blog/2011/10/edit.png"><img class="aligncenter size-medium wp-image-3648 fig" title="edit" src="/static/blog/2011/10/edit.png" alt="" width="500" height="309" /></a></p>
<p style="text-align: center;"><span style="font-size: x-small;">v5 カスタムレポート設定</span></p>
ほかにこんなパネェカスタムレポート使ってるよって方がいましたらシェアしましょ♪
