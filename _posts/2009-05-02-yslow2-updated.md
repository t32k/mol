---
layout: post
title: YSlow 2.0 アップデート
categories:
- performance
tags: []
status: publish
type: post
published: true
meta:
  pvc_views: '2258'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/05/yslow-20-release.html
  _edit_last: '1'
---
<img src="http://lh5.ggpht.com/_1drnogi3vdg/SfwFSF4A4lI/AAAAAAAAAXE/Kw2nQ22a5OY/8.png" alt="Yslow2.0" />
先日、<a href="http://developer.yahoo.net/blog/archives/2009/04/yslow_update.html">YSlowがアップデート</a>されましたね。主な変更点と言えば、
<ul>
	<li>新たに9つの指標を追加</li>
	<li>独自のルールセットが設定可能</li>
	<li>Smushi.itツールの追加</li>
	<li>UIデザインの変更</li>
</ul>
ですかね。
<h5>新たに9つの指標を追加</h5>
<img src="http://lh4.ggpht.com/_1drnogi3vdg/SfwEwosBxtI/AAAAAAAAAWM/M0tm-XhgdzY/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-1.png" alt="" />
上のキャプチャはこのブログを測定したものです。前のバージョンでは13の指標でしたが、今回は9つ追加されて合計で22となります。以下、追加された９つです。
<ul>
	<li>Make AJAX cacheable<span style="color: #999999;"> (content)</span></li>
	<li>Use GET for AJAX requests<span style="color: #999999;"> (server)</span></li>
	<li>Reduce the number of DOM elements<span style="color: #999999;"> (content)</span></li>
	<li>Avoid HTTP 404 (Not Found) error <span style="color: #999999;"> (content)</span></li>
	<li>Reduce cookie size<span style="color: #999999;"> (cookie)</span></li>
	<li>Use cookie-free domains<span style="color: #999999;"> (cookie)</span></li>
	<li>Avoid AlphaImageLoader filter<span style="color: #999999;"> (css)</span></li>
	<li>Do not scale images in HTML<span style="color: #999999;"> (images)</span></li>
	<li>Make favicon small and cacheable<span style="color: #999999;"> (images)</span></li>
</ul>
<h5>独自のルールセットが設定可能</h5>
<img src="http://lh4.ggpht.com/_1drnogi3vdg/SfwFRw7wXzI/AAAAAAAAAW0/ibqvyqNsfwo/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-6.png" alt="" />
小規模のサイトやブログなどでCDNを利用しなさいってのはコスト的に現実的ではないですよね。またサーバーの設定がいじれないということもありえます。そういった時にこれらの指標は検証しないという設定ができるようになりました。自分で22の指標から測定したい指標だけをチェックして独自のルールセットが作れます。またYslow1.0の13指標だけチェックする<span style="font-weight: bold;">classic(v1) </span>や小規模サイトのための<span style="font-weight: bold;">Small Site or Blog</span>のルールがあらかじめセットされています。<span style="font-weight: bold;">Small Site or Blog</span>でもう一度このブログを測定したら<span style="font-weight: bold;">D</span>から<span style="font-weight: bold;">Ｃ</span>に評価が上がりました。
<img src="http://lh5.ggpht.com/_1drnogi3vdg/SfwFSOToFNI/AAAAAAAAAW8/kwULw6F7fMU/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-7.png" alt="" />
<h5>Smushi.itツールの追加</h5>
<img src="http://lh3.ggpht.com/_1drnogi3vdg/SfwEw9HTeXI/AAAAAAAAAWk/dhnYiN0LOw4/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-4.png" alt="" />
<img src="http://lh6.ggpht.com/_1drnogi3vdg/SfwEwwaivfI/AAAAAAAAAWs/dDigLDCqliM/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-5.png" alt="" />
Yahoo! Performance Teamの人らが作った画像最適化ツールもYSlowから利用できるようになりました。タブの<span style="font-weight: bold;">Tools</span>から<span style="font-weight: bold;">All Smush.it™</span> をクリックすれば、表示されている画像を最適化してくれます。
<h5>UIデザインの変更</h5>
<img src="http://lh6.ggpht.com/_1drnogi3vdg/SfwEwotXkqI/AAAAAAAAAWU/eagkoT4Yguc/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-2.png" alt="" />
<span style="font-weight: bold;">Components</span>は種類ごとにグルーピングされて見やすくなりましたね。

<img src="http://lh4.ggpht.com/_1drnogi3vdg/SfwEwvRdgBI/AAAAAAAAAWc/OnoI1nbad14/%E3%83%94%E3%82%AF%E3%83%81%E3%83%A3-3.png" alt="" />
<span style="font-weight: bold;">Statistics</span>はYahoo!カラーの紫系でまとめたんでしょうか、おしゃれですが区別しにくくなったのではと個人的には思います。。。

みなさんも新しいYSlow試してみてはどうでしょうか。
<ul>
	<li><a href="https://addons.mozilla.org/en-US/firefox/addon/5369">YSlow :: Firefox Add-ons</a></li>
</ul>
