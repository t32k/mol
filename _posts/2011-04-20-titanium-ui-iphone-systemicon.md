---
layout: post
title: Titanium.UI.iPhone.SystemIcon
categories:
- Titanium Mobile
tags:
- iphone
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '6292'
  _aioseop_description: んで、やっぱ違うわー、なんか意味違うわー。って方はこういったところでお気に入りのアイコンも探すのもありかと。
---
<p style="text-align: center;"><img class="size-full wp-image-2948 aligncenter" title="Tab Bar" src="/static/blog/2011/04/tab_bar.png" alt="TabGroup" width="390" height="181" /></p>
<a href="http://developer.appcelerator.com/blog/2011/04/titanium-mobile-1-6-2-is-released.html">Titanium Mobile 1.6.2</a> が出てましたね、皆さんいかがお過ごしでしょうか。わい？ わいタイタンやで(・∀・)ｲｲ!!てことで今回はシステムボタンではなくシステムアイコンについてキャプりました。

<!--more-->

前回のボタンはおもにtoolbarやnavbarで使うものですが、今回のはtabbar(tab group)で使うアイコンです。独自のアイコンも作るのも良いですがまずは基本です。ってことで、使い方はこんな感じ。
[javascript]
var tabGroup = Titanium.UI.createTabGroup();

var tab = Titanium.UI.createTab({
icon: Titanium.UI.iPhone.SystemIcon.FAVORITES
});

tabGroup.addTab(tab);
tabGroup.open();
[/javascript]
crateTabの中で呼び出すんですね。これだけで下のtitle部分まで指定してくれちゃいます。

Bookmarkアイコンで下の文字列を「Book」とかにしたい場合、どうしたらいいんじゃいと思ったがどうも無理臭い。やるのであれば同じようなアイコン画像を作ってそこでtitleを指定する感じですか、意味なしです。
<ul>
	<li><a href="http://developer.appcelerator.com/question/7401/tab-bar-system-icon-and-title">Appcelerator Developer Center - Tab Bar System Icon and Title</a></li>
</ul>
とはいえ、いろいろあって便利なので列挙。
<h2>Titanium.UI.iPhone.SystemIcon</h2>
<h4>BOOKMARKS</h4>
<img style="vertical-align: middle;" title="Bookmark style icon" src="/static/blog/2011/04/bookmarks.png" alt="BOOKMARKS" width="60" height="44" /> アプリケーション固有のブックマークを表示する
<h4>CONTACTS</h4>
<img style="vertical-align: middle;" title="Contacts style icon" src="/static/blog/2011/04/contacts.png" alt="CONTACTS" width="60" height="44" />「連絡先(Contacts)」を表示する
<h4>DOWNLOADS</h4>
<img style="vertical-align: middle;" title="Downloads style icon" src="/static/blog/2011/04/downloads.png" alt="DOWNLOADS" width="60" height="44" /> ダウンロードを表示する
<h4>FAVORITES</h4>
<img style="vertical-align: middle;" title="Favorites style icon" src="/static/blog/2011/04/favorites.png" alt="FAVORITES" width="60" height="44" /> ユーザ定義のよく使う項目を表示する
<h4>FEATURED</h4>
<img style="vertical-align: middle;" title="Featured style icon" src="/static/blog/2011/04/featured.png" alt="FEATURED" width="60" height="44" /> アプリケーションの推奨コンテンツを表示する
<h4>HISTORY</h4>
<img style="vertical-align: middle;" title="History style icon" src="/static/blog/2011/04/history.png" alt="HISTORY" width="60" height="44" /> ユーザアクションの履歴を表示する
<h4>MORE</h4>
<img style="vertical-align: middle;" title="More style icon" src="/static/blog/2011/04/more.png" alt="MORE" width="60" height="44" /> 追加のTab Barの項目を表示する
<h4>MOST_RECENT</h4>
<img style="vertical-align: middle;" title="Most recent style icon" src="/static/blog/2011/04/more_recent.png" alt="MOST_RECENT" width="60" height="44" /> 最新の項目を表示する
<h4>MOST_VIEWED</h4>
<img style="vertical-align: middle;" title="Most viewed style icon" src="/static/blog/2011/04/most_viewed.png" alt="MOST_VIEWED" width="60" height="44" /> すべてのユーザに最も人気のある項目を表示する
<h4>RECENTS</h4>
<img style="vertical-align: middle;" title="RECENTS" src="/static/blog/2011/04/recents.png" alt="Recents style icon" width="60" height="44" /> アプリで定義した期間内にユーザがアクセスした項目を表示する
<h4>SEARCH</h4>
<img style="vertical-align: middle;" title="Search style icon" src="/static/blog/2011/04/search.png" alt="SEARCH" width="60" height="44" /> 検索モードに入る
<h4>TOP_RATED</h4>
<img style="vertical-align: middle;" title="Top rated style icon" src="/static/blog/2011/04/top_rated.png" alt="TOP RATED" width="60" height="44" /> ユーザが決める最も高く評価された項目を表示する
<h3>参照</h3>
<ul>
	<li><a href="https://developer.appcelerator.com/apidoc/mobile/1.0/Titanium.UI.iPhone.SystemIcon">Appcelerator Developer Center - API for Titanium.UI.iPhone.SystemIcon (version 1.0)</a></li>
</ul>
んで、やっぱ違うわー、なんか意味違うわーって方はこういったところでお気に入りのアイコンも探すのもありかと。
<ul>
	<li><a href="http://www.glyphish.com/">Glyphish – Great icons for great iPhone &amp; iPad applications</a></li>
	<li><a href="http://app-bits.com/">app-bits.com | Slick user interface and icon design</a></li>
	<li><a href="http://www.iconsweets.com/">iconSweets » Free icons by Yummygum</a></li>
	<li><a href="http://www.iconsweets2.com/">iconSweets 2 » Even more free icons by Yummygum</a></li>
</ul>
