---
layout: post
title: Google Analyticsの(other)とはなんぞや？
categories:
- analytics
tags:
- google analytics
status: publish
type: post
published: true
meta:
  pvc_views: '3624'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/11/google-analytics-other-entry.html
  _edit_last: '1'
---
アクセス解析してたら、どうもデータの取れていないページがある事に気づいた。確かに該当のページは他のページと比べてあまり見られてなさそうなページなので、もしかして、はしょられているの？なんて思いながらGoogle Analyticsのそこらへんの仕様について調べてみた。<br /><br />というのも、データが取れていないのなら取れていないでいいんだけど、こっちとしてはなぜ取れていないのか説明できないとアクセス解析ツールを使う他部署の皆さんが不信感を抱いてしまう。｢こんなうさんくさいツール信用できっかよ｣なんて事になったら困りものだ。<br /><br />そうゆことで、最初に目をつけたのが<b>トラッキングコードがおかしくないか</b>。うん、基本ですね。目視でちゃんと正しいトラッキングコードになっていることを確認。てか、テンプレートページに入れてあるので、該当のページだけおかしくなるというのは考えられない。<br /><br />続いて、HTTPヘッダーでGIFリクエストされていることも確認。<b>GAサーバーに情報は送られているのは確か</b>なようだ。<br /><br />つまり、情報が送られて表示するまでの間が問題かと思い、次にフィルタに着目。フィルタはほんとうに怖いね。試しに何にもフィルタをかけていないプロファイルを新しく作成し、該当のページにアクセスしてみた。一日後、うん記録されてないね。<b>フィルタが原因ではなかった</b>。<br /><br />困った。だいぶ困った。そしたらこんなヘルプ記事見つけた。<br /><br /><blockquote><span style="font-size: 85%;"><span style="font-weight: bold;">一日で50,000ページ（または仮想ページ）以上をトラッキングしていませんか？</span></span><span style="font-size: 85%;"><br />Google AnalyticsはWebサイトの全ての情報を収集し、一日つき50,000ページまでページビューで分類されたレポートを表示します。残りのページはレポート上では (other) という名前のエントリに集約されます。トラフィックの少ないページの詳細なレポートを見るためには、トラフィックの多いページを除くフィルタをかけた新しいプロファイルを作成する必要があります。こうすることで、効果的に残ったページを50,000URLs内に含めておけます。<br /></span><br /><div style="text-align: right;"><span style="font-size: 85%;"><a href="http://code.google.com/intl/en/apis/analytics/docs/tracking/gaTrackingTroubleshooting.html">Troubleshooting the Tracking Code - Google Analytics - Google Code</a></span><br /></div></blockquote><br />そんなん知らないよ〜＞＜<br />試しに1日分のデータ見たら確かに49,999ページ分しかなかった。<br /><br /><img alt="" class="fig" src="http://lh4.ggpht.com/_1drnogi3vdg/SwaejT6swYI/AAAAAAAAAsk/jFQRXDaLHlI/other.png" /><br /><br /><span style="font-weight: bold;">(other)</span>は前々から気になってたけど、こんなところで理解するとは思わなかった。つまり、今回の現象はPV数が少ないページが記録される前に、他のPVの多いページが50,000ページ記録されて、それ以降は<span style="font-weight: bold;">(other)</span>にまとめられちゃったから、｢上位のコンテンツ｣から該当のURLで検索してもひっかからなかったってことね。<br /><br />ということは、50,000ページ記録される前に該当のページにアクセスすれば記録されるんじゃねと思ったので、日付が変わる12時過ぎにアクセスしたけど、記録されなかった。たぶん、50,000ページのリセットのタイミングが日付と違うのか、それともPV数の多いページから優先的に処理されるのかもね。<br /><br />ともかく、PV数の少ないページのレポートを見るためにフィルタで細分化されたプロファイルから確認しないといけないって他部署の人には説明すれば良いと言うわけだ、てかその前にそんなトラフィックあるんなら有償ツール使えってことですね。。。はい、SiteCatalyst使いたいです＞＜<br /><br /><span style="font-size: 85%;">関連リソース<br /></span><br /><ul><li><a href="http://d.hatena.ne.jp/kahze/20090318/1237350495"><span style="font-size: 85%;">PV制限なしでGoogle Analyticsを使っているのに"(other)"が出てくる件 - ジブログ2</span></a></li></ul>
