---
layout: post
title: 複数のGoogle Analytics Tracker Codeを併用する
categories:
- analytics
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/06/google-analytic-tracker-code.html
  _edit_last: '1'
  pvc_views: '2516'
---
<a href="http://www.suzukikenichi.com/blog/tracking-access-by-mutiple-google-analytics-accounts/">Google Analyticsを複数のプロファイルでトラッキング | 海外SEO情報ブログ・メルマガ</a>でGAのカスタマイズってほどでもないけど、トラッキングコードのTipsが紹介されている。要は_gat._getTracker()で初期化する際に、変数を2つ用意してあげればいいってことだね。<br /><br />ちょうど<a href="http://www.sigma-dp.com/DP2/">SIGMA DP2 : Special Contents</a>で似たようなコード見つけたので、挙げておく。<br /><pre>&lt;script type="text/javascript"&gt;<br />try {<br /><br />var <span style="color: #6600cc;">pageTracker</span> = _gat._getTracker("UA-xxxxxx-1");<br />pageTracker._trackPageview();<br /><br />var <span style="color: #6600cc;">pageTracker2</span> = _gat._getTracker("UA-yyyyy-4");<br />pageTracker2._trackPageview();<br /><br />} catch(err) {}<br />&lt;/script&gt;</pre>pageTrackerとpageTracker2に格納してるんすね。違うアカウントで同じプロファイルを共有したい時ってゆう状態が、よくわからないんだけども。クライアントさんと制作者側が両方アクセス解析の情報を知りたいって時には便利なのかもしれないね。たぶん。<br /><br /><a href="http://www.vkistudios.com/">Analytics Consulting, Conversion Rate Optimization and Internet Marketing Vancouver BC</a>てところは、こんな感じだった。<br /><pre>&lt;script type="text/javascript"&gt;<br />try {<br />var <span style="color: #330099;">pageTracker</span> = _gat._getTracker("UA-5036481-1");<br />var isDev = window.location.href.search(/vkistudios.net/);<br /><br /><span style="color: #6600cc;">if (isDev &gt; -1)</span><br />pageTracker._setDomainName(".vkistudios.net");<br /><span style="color: #6600cc;">else</span><br />pageTracker._setDomainName(".vkistudios.com");<br /><br />pageTracker._setLocalRemoteServerMode();<br />pageTracker._initData();<br />pageTracker._trackPageview();<br />} catch (e) {}<br /><br /><span style="color: #666666;">//event tracking profile</span><br />try {<br />var <span style="color: #6600cc;">eventTracker</span> = _gat._getTracker("UA-5036481-4");<br /><br /><span style="color: #6600cc;">if (isDev &gt; -1)</span><br />eventTracker._setDomainName(".vkistudios.net");<br /><span style="color: #6600cc;">else</span><br />eventTracker._setDomainName(".vkistudios.com");<br />eventTracker._initData();<br />eventTracker._trackPageview();<br />} catch (e) {}<br />&lt;/script&gt;</pre>イベントトラッキングとコンテンツの情報は分けて管理してるのかな。URLを判別して、_setDomainName()の引数を変えることでマルチドメイントラッキングを可能にしてる。<br /><br />こんなふうにいろんなサイトのカスタマイズしたコード見てみたいもんです。<br />eコマーストランザクションとかどこか使ってないもんかな。
