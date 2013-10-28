---
layout: post
title: Chrome DevTools.next from yoshikawa_t
categories:
- development
- javascript
- performance
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '1958'
  _wp_old_slug: '4556'
---
<p style="text-align: center;"><img class=" wp-image-4570 aligncenter" alt="" src="http://t32k.me/mol/file/2012/12/chrome.jpg" /></p>
昨日は、弊社の社内勉強会に、Google API Expertや「<a href="http://www.amazon.co.jp/dp/484433266X">jQuery Mobileパーフェクトガイド</a>」の著者で有名な<a href="http://d.hatena.ne.jp/pikotea/">吉川さん</a>が登壇してくれました。『なんか喋ってよ』とアバウトな私の要望に完璧に、いやパーペキすぎに応えてくれました吉川さんにマジ感謝リスペクトでございます。

そんな吉川さんのスライドが上がっておりますので、みなさまもご覧になってはどうでしょうか。

<iframe style="border: 1px solid #CCC; border-width: 1px 1px 0; margin-bottom: 5px;" src="http://www.slideshare.net/slideshow/embed_code/15725086" height="486" width="597" allowfullscreen="" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>
<div style="margin-bottom: 5px;"><strong> <a title="Chrome DevTools.next" href="http://www.slideshare.net/yoshikawa_t/chrome-devtoolsnext" target="_blank">Chrome DevTools.next</a> </strong> from <strong><a href="http://www.slideshare.net/yoshikawa_t" target="_blank">yoshikawa_t</a></strong></div>
以前にもこの社内勉強会では<a href="https://speakerdeck.com/t32k/mobile-front-end-optimization-standard-2012">私もChrome DevTools(PageSpeed)に関して</a>、ざっと概要を説明していたのですが、JavaScriptやレンダリングの最適化等に関しては説明していなかった（できなかった）ので、吉川さんにお願いしました。

やっぱりデモをしながらだとすごくわかりやすくて、特にTimelineパネルの説明などは英語などの記事はよく見かけるのですが、今回、日本語で説明してくれて本当助かりました。このへんちょっとよく分かんなかったので、テンションだだあがりでした。

もはやHTTPリクエスト削減などは当たり前にやるべきことで、競合他社とパフォーマンスに関して差別化しようと思うのであれば、このレベルでの最適化が必要になってくると感じているので、まさしくNextの段階に進むための素晴らしい講義でした。
<h3>参考</h3>
<ul>
	<li>
<p style="display: inline !important;"><a href="http://www.jankfree.com/jank-busters-io/index.html#1">Jank Busters - Google IO 2012</a></p>
</li>
	<li><a href="https://gist.github.com/4338551">gist:4338551</a></li>
	<li><a href="http://paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/">Why moving elements with translate() is better than pos:abs top/left « Paul Irish</a></li>
	<li><a href="http://www.youtube.com/watch?v=WpqZ0LjNU5A">The Breakpoint Ep. 4 —The Tour De Timeline - YouTube</a></li>
	<li><a href="http://addyosmani.com/blog/performance-optimisation-with-timeline-profiles/">Improving Web App Performance With the Chrome DevTools Timeline and Profiles </a></li>
	<li><a href="http://ariya.ofilabs.com/2012/12/javascript-performance-analysis-sampling-tracing-and-timing.html">JavaScript Performance Analysis: Sampling, Tracing, and Timing don't code today what you can't debug tomorrow </a></li>
	<li><a href="http://www.html5rocks.com/en/tutorials/speed/rendering/">Jank Busting for Better Rendering Performance - HTML5 Rocks</a></li>
	<li><a href="http://www.html5rocks.com/en/tutorials/games/abouttracing/">Profiling your WebGL Game with the about:tracing flag - HTML5 Rocks </a></li>
	<li><a href="https://docs.google.com/presentation/d/1b7rdeXYdmL3lmT24GAaC14eOSkq5qt6FM-yLSeFykQk/edit?pli=1#slide=id.g5087401_1_0">Velocity 2012 - Rendering Slow - Google Drive </a></li>
</ul>
あと、吉川さんはChromeのGoogle API Expertということで、DevToolsへの要望・改善を本国のエンジニアに伝えることが可能らしく、DevToolsの不満は吉川さんにぶつけてみようｗ僕からは、スマホサイトとPCサイトをデバッグしてるときすごくめんどくさいのですが、Dock to rightとDock to Bottomをワンクリック（ショートカット）で切り替え出来るようにしてほしい！と投げときました。

最後に、Paul Irishさんに(o・∀・)oｸﾞｯｼﾞｮﾌﾞ!って言われてる吉川さんすげー！！今回はほんとうにありがとうございました！
<blockquote class="twitter-tweet tw-align-center" data-in-reply-to="282104729696362497">@<a href="https://twitter.com/yoshikawa_t">yoshikawa_t</a> fantastic deck. nice work!

— Paul Irish (@paul_irish) <a href="https://twitter.com/paul_irish/status/282214323294711808" data-datetime="2012-12-21T20:01:52+00:00">December 21, 2012</a></blockquote>
&nbsp;
