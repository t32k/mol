---
layout: post
title: デフォルトページとindex.html
categories:
- analytics
tags:
- google analytics
status: publish
type: post
published: true
meta:
  pvc_views: '2191'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2008/11/ga-indexhtml.html
  _edit_last: '1'
---
<a title="ga01 by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/3049307631/"><img src="http://farm4.static.flickr.com/3142/3049307631_82c30d6cfb.jpg" alt="ga01" width="500" height="239" /></a>

Google Analytics(以下、GA)でのプロファイル設定の『デフォルトのページ』に違和感、というかイマイチよくわかならない。

『デフォルトのページ』に関してのGoogleヘルプページ内容はこちら↓
<blockquote><span style="font-weight: bold;">デフォルトのページ</span>
[デフォルトのページ] は、ドメイン上のページが指定されていない場合に、サーバーがデフォルトで返すウェブ ページのことです。 たとえば、「www.yourdomain.co.jp」と入力すると、サーバーから index.html ページが返される場合は、index.html がデフォルトのページとなります。
Analytics の [プロファイル設定] ページには、デフォルトのページを指定する欄があります。 Google Analytics では、この情報を使用して www.yourdomain.co.jp と www.yourdomain.co.jp/index.html のヒットが実際には同じページであると判断します。デフォルトのページが指定されていない場合、これら 2 つのエントリは別のページとしてレポートに集計されます。
<div style="text-align: right;"><a href="http://www.google.co.jp/support/googleanalytics/bin/answer.py?answer=32995&amp;useful=0&amp;show_useful=1&amp;comment="><span style="font-size: 85%;">デフォルトのページ - Google Analytics ヘルプ センター</span></a></div></blockquote>
www.yourdomain.co.jp入力したらindex.html返すの当たり前じゃん、最初からそんなん指定しといてよと思った。だがそうでも、ないらしいのね。こんな記事見つけた↓
<blockquote>何故、最初からデフォールトのページを「index.html」にしてしまわないのか。それは、ウェブサーバーの設定で、デフォールトのページを変えられるから。
例えば、Apache のデフォールトは「index.html」だけど、IIS (Microsoft のウェブサーバー) のデフォールトは「Default.htm」だったり「index.htm」だったりする。「main.html」をデフォールトのページに設定してる人もいるかもしれないし、もっと変な名前をデフォールトにしてるかもしれない。若しくは、「○○/」と「○○/index.html」を同じとして数えたくない人もいるかもしれない。
<div style="text-align: right;"><span style="font-size: 85%;"><a href="http://at-aka.blogspot.com/2006/04/google-analytics.html">clmemo@aka: Google Analytics のデフォールト・ページ</a></span></div></blockquote>
なるほど、そういうことか。合点がいったよ。で、GAで『デフォルトのページ』をindex.htmlにしたわけです。そしたら、GA上では、www.example.com/などスラッシュで終わってるURLはすべてwww.example.com/index.htmlという表記でカウントされるんですね。

当たり前というか当たり前だけど。。。すべてのページをでディレクトリ作ってindex.htmlで作ったとしたら、おしりが全部index.htmlなので、見にくいじゃん。こんなふうに↓

<a title="ga02 by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/3050147092/"><img src="http://farm4.static.flickr.com/3188/3050147092_34fafc50c9.jpg" alt="ga02" width="500" height="232" /></a>

ということで、デフォルトのページは設定しないことにした。そしたらwww.example.com/とwww.example.com/index.htmlは、別々のURLで扱われるじゃないか！と思うけど。index.htmlでアクセスししてきた人は/にリダイレクトすればいいんだ。で.htaccessでこんなん見つけた↓
<blockquote>Options +FollowSymLinks
RewriteEngine on
RewriteCond %{THE_REQUEST} ^.*/index.html
RewriteRule ^(.*)index.html$ http://www.example.com/$1 [R=301,L]
<span style="font-size: 85%;">※www.example.com内のすべてのディレクトリで、「/index.html」が「/」に正規化されます。</span>
<div style="text-align: right;"><a href="http://www.suzukikenichi.com/blog/canonicalization-of-indexhtml-and-non-indexhtml/"><span style="font-size: 85%;">index.html「あり・なし」のURL正規化～301リダイレクト応用編 » 海外SEO情報ブログ・メルマガ</span></a></div></blockquote>
ようやく、自分の思い通りになったけど、GAで表示する出力を変えるだけなら、<a href="http://www.google.com/support/analytics/bin/answer.py?hl=jp&amp;answer=55461">アドバンスフィルタ</a>とか使えば良かったのかな、フィルタ系全然分からないな。もっと勉強します。。。
