---
layout: post
title: pageTracker._initData();もいらない？
categories:
- analytics
tags:
- GA
status: publish
type: post
published: true
meta:
  pvc_views: '2732'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/05/pagetracker-initdata.html
  _edit_last: '1'
---
数ヶ月前の記事（<a href="http://warikiru.blogspot.com/2009/01/update-google-analytics-code.html">Google Analytics コードアップデート</a>）でGAのコードにtry {} catch(err) {}文が挿入されたってことを書いた。でも、よくよく見たら<span style="font-weight: bold;">pageTracker._initData();</span>の関数もなくなっていない？ってことに気づいた！

[javascript]
var pageTracker = _gat._getTracker("UA-xxxxxxx-x");
pageTracker._initData();
pageTracker._trackPageview();
[/javascript]

少し前のga.jsのコードはこんな感じだったともう。

[javascript]
try{
var pageTracker = _gat._getTracker("UA-xxxxxxx-x");
pageTracker._trackPageview();
} catch(err) { }
[/javascript]

今はこんな感じ。

_initData()ってゆうくらいだから初期化する関数なのかと思い<a href="http://www.google.com/support/googleanalytics/bin/answer.py?hl=jp&amp;answer=76305#init">Google Analytics トラッキング コード移行ガイド</a>で初期化部分探したけど、載ってない。。。
んで、悔しいから<a href="http://code.google.com/intl/ja/apis/analytics/docs/gaJS/gaJSApi.html#_gat.GA_Tracker_._initData">Google Analytics Tracking API</a>探したら書いてあった！
<blockquote><strong><span style="font-size: small;">_initData()</span></strong><span style="font-size: small;">
_initData()</span><span style="font-weight: bold;"><span style="font-size: small;">Deprecated</span></span><span style="font-size: small;">. initData() now executes automatically in the ga.js tracking code.
</span><span style="color: #999999;"><span style="font-size: small;">Initializes or re-initializes the GATC (Google Analytics Tracker Code) object.</span></span>
[javascript]
var pageTracker = _gat._getTracker("UA-12345-1");
pageTracker._initData();
pageTracker._trackPageview();
[/javascript]
</blockquote>

Deprecatedってことは廃止予定ってことか。なんかga.js内で自動的に実行しているらしい。
あーすっきり！しかしまぁ、もうちょっとアナウンスしてくれてもいいんだと思うんだけどな。。。
