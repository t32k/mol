---
layout: post
title: Google Analytics コードアップデート(2009年1月)
categories:
- analytics
tags:
- GA
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/01/update-google-analytics-code.html
  _edit_last: '1'
  pvc_views: '2718'
  _aioseop_description: トラッキングスニペットにtry catch文が追加された。_gatエラーのためだと思われる。
  _wp_old_slug: google-analytics-tracker-code
---
<span style="font-size: 85%;"><a style="font-weight: bold;" href="http://analytics.blogspot.com/2009/01/short-answer-is-you-dont-have-to-change.html#links">Google Analytics Blog: The short answer is.. you don't have to change your snippet</a>より</span>

最近、Google Analyticsのコードが新しくなったらしい。

[HTML]

&lt;script type="text/javascript"&gt;
var gaJsHost = (("https:" ==  document.location.protocol) ? "https://ssl." : "http://www.");
document.write(unescape("%3Cscript  src='" + gaJsHost + "google-analytics.com/ga.js'  type='text/javascript'%3E%3C/script%3E"));
&lt;/script&gt;

&lt;script type="text/javascript"&gt;
try {
var pageTracker =  _gat._getTracker("UA-XXXXX-X");
pageTracker._trackPageview();
} catch(err) {}
&lt;/script&gt;

[/HTML]

んで、また変更しきゃいけないのかと思ったらそうでもない感じ。
基本的に変えなくてもいいよーとのこと。

なぜ変更したのかと言うと、一部のブラウザでGoogle Analyticsを入れてる
ページを見るとJavaScriptエラーが出るらしくて、それを表示させないようにしたらしい。
これは極めて異例なケースだからあんまり気にしなくてもいいって。
でも、できるならアップデートしといてねと。

で、そのJavaScriptエラーがどんなもんかと<a href="http://www.google.com/support/forum/p/Google+Analytics?hl=en">Google Analytics Help</a>でググったら、
<blockquote>Q.  Error:'_gat' is undefinedって出るんだよ (´･ω･`)
A. ( ・∀・)っ 新しいコードにすればいいんだよ
<div style="text-align: right;"><span style="font-size: 85%;"><a href="http://www.google.com/support/forum/p/Google+Analytics/thread?tid=050446cd03a61132&amp;hl=en">Question: Google analytics code causes Javascript error message in Explorer</a></span></div></blockquote>
<span style="font-size: 85%;">
</span>ってことで、_gatでググったら困ってる人がいましたね。
<ul>
	<li><a href="http://www.senov.net/notes/2008/10/-gat-error.html">Google Analytics JavaScript error? - Senov</a></li>
	<li><a href="http://d.hatena.ne.jp/apple-mango/20080829">2008-08-29 - 私という名の物語*Try and error*</a></li>
</ul>
<img src="http://lh6.ggpht.com/_1drnogi3vdg/SXFUCfGH3RI/AAAAAAAAAMM/TWyTL0e7AZI/gaterror.jpg" alt="" />
<span style="color: #666666; font-size: 85%;">（Google Analytics JavaScript error? - Senovより）</span>

キャプチャしてくれてるとありがたいですね。
こーゆーのが出るのね、了解。

というわけで、_gatエラーに悩んでた人は試してみると良いと思う。
もちろん、そんなエラー知らなかった人も別にデータに影響しないので、
コード追加だけですからやっておいた方がいいでしょう。

[追記] <a href="http://analytics-ja.blogspot.com/2009/03/code-snipet.html">日本のGoogle Analyticsブログでもアナウンスされましたね。</a>
