---
layout: post
title: Google Analyticsでページロード時間を計測する（改）
categories:
- analytics
tags:
- google
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2010/02/page-load-time-2.html
  _edit_last: '1'
  _wp_old_slug: google-analytics%e3%81%a7%e3%83%9a%e3%83%bc%e3%82%b8%e3%83%ad%e3%83%bc%e3%83%89%e6%99%82%e9%96%93%e3%82%92%e8%a8%88%e6%b8%ac%e3%81%99%e3%82%8b%ef%bc%88%e6%94%b9%ef%bc%89
  pvc_views: '4215'
---
前回紹介した、<a href="http://warikiru.blogspot.com/2010/01/page-load-time.html">ページロード時間を計測するTips</a>ですが、直帰率が0%になるのが玉に瑕でした。が、新しくプロパティIDを発行して、通常解析用のプロファイルとロード時間計測用のプロファイルと分離すればいいんじゃね？と思ったのでやってみましたよ。

<!--more-->

アカウントサマリー画面から『+ 新しいプロファイルを追加』をクリックし、『新しいドメインのプロファイルを追加』の方を選択して新しいプロパティID（UA-xxxxxxx-2）を発行します。

<img class="fig" src="http://lh3.ggpht.com/_1drnogi3vdg/S3FPqjcnksI/AAAAAAAAAzM/xf8NpxJjYP0/ga.png" alt="+ 新しいプロファイルを追加" />

BODY開始タグの直後に置くコードは前回と同じです。
<pre><span style="color: #666666;">&lt;body&gt;</span>
&lt;script type='text/javascript'&gt;
var Begin = new Date();
var Start = Begin.getTime();
&lt;/script&gt;

<span style="color: #666666;"> [ ページのコンテンツ]</span></pre>
BODY終了タグに置くコードが前回とはちょっと違います。
<pre><span style="color: #666666;"> [ ページのコンテンツ]</span> 

&lt;script type='text/javascript'&gt;try {<span style="color: #666666;">// 通常解析用</span>var pageTracker = _gat._getTracker("UA-xxxxxxx-1");pageTracker._trackPageview();

<span style="color: #666666;">// ロード時間計測用</span><span style="color: #38761d;">var timeTracker = _gat._getTracker("UA-xxxxxxx-2");timeTracker._trackPageview();</span>var End = new Date();var Stop = End.getTime();var timeElapse = Stop - Start; // stored as millsecondvar Url = location.href;timeTracker._trackEvent(  'Page Load',  'Load Time',  Url,  timeElapse); } catch(err) {}&lt;/script&gt;<span style="color: #666666;">&lt;/body&gt;</span></pre>
緑色の部分が新規に追加したコードだ。説明すると、通常解析用のプロファイル、つまり元からあるプロパティID(UA-xxxxxxx-1)は<strong>pageTracker</strong>オブジェクトに格納されているので、そこで完結している。

今回入れたロード時間計測用のプロパティID（UA-xxxxxxx-2）は新たに作成した<strong>timeTracker</strong>（名前はなんでもいい）オブジェクトに格納されているので、pageTrackerオブジェクトに影響しない。だから、_trackEvent関数もtimeTracker._trackEvent();と呼び出している。

これで、UA-xxxxxxx-1のプロファイルは直帰率に異常を起こすことなく、かつ、UA-xxxxxxx-2のプロファイルの方でロード時間を確認することが出来る。（こっちの直帰率はゼロになるけど）2週間ほど、このブログで設置して試しているが特に問題は起きていない。ただヘルプでも言われている通り、複数のトラッキングコードを実装することはサポートされていないことになっているから、あまりお薦めはしない。単純にpageTrackerとtimeTrackerの2つのオブジェクトがあることで混乱する可能性も高まるので。

なんかもっといい方法ないもんかなー・ω・
<blockquote><strong>サイトに複数のトラッキング コードが設置されています。</strong>
1 つのウェブページに複数の Google Analytics トラッキング コードを設置することはサポートされていない実装方法です。コードを 1 つだけ残して他はすべて削除し、測定したい各ページに、正しいプロファイルのコードをインストールすることをお勧めします。
<div style="text-align: right;"><span style="font-size: x-small;"><a href="http://www.google.com/support/analytics/bin/answer.py?hl=jp&amp;answer=72298">Analytics ヘルプ </a></span></div></blockquote>
