---
layout: post
title: コメントアウト
categories:
- memo
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2007/08/blog-post.html
  pvc_views: '2085'
  _edit_last: '1'
---
<p>自分の中でコメントアウトがごちゃごちゃしてきたのでメモ！</p><span style="font-weight: bold;">HTML</span><br />&lt;!-- コメントアウト --&gt;<p><br /></p><p><span style="font-weight: bold;">CSS</span><br />/*コメントアウト */</p><p><br /></p><span style="font-weight: bold;">JavaScript</span><br />//一行のときコメントアウト<br /><br />/*<br />複数行のとき<br /><p>コメントアウト<br />*/</p><br /><p style="font-weight: bold;">XHTMLでページ内にJavaScriptを記述するとき<br /><span style="font-weight: normal;">&lt;script type="text/javascript"&gt;</span><br /></p><p><br />//&lt;![CDATA[<br /><br />　スクリプト・・・<br /><br />//]]&gt;<br /><br />&lt;/script&gt;</p>なんでかってゆうとXHTMLではスクリプト内の"< "もタグの開始だとみなされちゃうから<p>らしい。<p>CDATA(Character Data)・・・文字データ</p>
