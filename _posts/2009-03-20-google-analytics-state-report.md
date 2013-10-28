---
layout: post
title: Google Analyticsで都道府県別セッションを調べる
categories:
- analytics
tags: []
status: publish
type: post
published: true
meta:
  pvc_views: '3227'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/03/region-custom-reporting.html
  _edit_last: '1'
---
<a href="http://www.kagua.biz/operation/custom-todoufuken.html">カスタムレポートを使って都道府県別セッションを調べる </a>より<br /><br />ほぼ受け折りで恐縮ですが、自分でもやってみたかったので。。。<br />都道府県別セッション数をカスタムレポートで作ってみようっていう主旨。<br /><br />GAの左メニューから <span style="font-weight: bold;">ユーザー</span> > <span style="font-weight: bold;">地図上のデータ表示 </span>からだと以下のように表示されます。国別になってます。。<span style="font-weight: bold;">Japan</span>をクリックすると<span style="font-weight: bold;">Shinjuku</span>や<span style="font-weight: bold;">Shibuya</span>などが表示されます。違うんだ、僕の知りたいのは都道府県別のセッションなんだ！<br /><img src="http://lh5.ggpht.com/_1drnogi3vdg/ScMD2AGpSzI/AAAAAAAAATU/s5ronVE3oHo/fig1.png" alt="" /><br /><br /><br />ということで、カスタムレポートを作成♪<br /><img src="http://lh6.ggpht.com/_1drnogi3vdg/ScMD2migFjI/AAAAAAAAATc/brn8d46EoSs/fig2.png" alt="" /><br /><br /><br /><span style="font-weight: bold;">カスタムレポートを新規作成</span>をクリックすると以下のようなページが表示されますので、まずはタイトルを「都道府県別セッション数」にでも変更しましよ。次に、<span style="font-weight: bold;">指標</span> > <span style="font-weight: bold;">利用状況</span> > <span style="font-weight: bold;">セッション数</span> を選んでドラッグアンドドロップ！<br /><img src="http://lh6.ggpht.com/_1drnogi3vdg/ScMD2tcw0PI/AAAAAAAAATk/RoTViO-plCQ/fig3.png" alt="" /><br /><br /><br />次に、ディメンションを設定しましょう。<span style="font-weight: bold;">ディメンション</span> > <span style="font-weight: bold;">ユーザー</span> > <span style="font-weight: bold;">地域</span> をまずドラッグアンドドロップ。デフォルトのはここが<span style="font-weight: bold;">国/地域</span>になってるからあかんのですね。んで、これだけではつまらないのでサブディメンションに<span style="font-weight: bold;">都市</span>も追加して<span style="font-weight: bold;">レポートを作成</span>。<br /><img src="http://lh3.ggpht.com/_1drnogi3vdg/ScMD2tgxxdI/AAAAAAAAATs/8dSzmjctLX8/fig4.png" alt="" /><br /><br /><br />そうすると以下のように、都道府県別で表示されてますね。<br />（意外と奈良県民に好評なようですね、このブログ）<br /><img src="http://lh3.ggpht.com/_1drnogi3vdg/ScMD2zeIwXI/AAAAAAAAAT0/r-DXu2yGIeI/fig5.png" alt="" /><br /><br /><br />上記で<span style="font-weight: bold;">Tokyo</span>をクリックすればドリルダウンで各都市別のセッションも確認できます。<br /><img src="http://lh5.ggpht.com/_1drnogi3vdg/ScMD8hGvHEI/AAAAAAAAAT8/8Wc_BH_Za_A/fig6.png" alt="" /><br /><br />単純なカスタムレポートですが、これにコンバージョンなども組み合わせれば有益なレポートが作成できますね。ほんとちゃんと使わないとなーと再確認しました。こんなんだと<a href="http://google.starttest.com/">Google Analytics Individual Qualification</a>合格なんて夢のまた夢。。精進します。
