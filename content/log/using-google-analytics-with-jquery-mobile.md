---
date: 2011-06-28
title: jQuery MobileでGoogle Analyticsを使うために気をつけなければいけないこと
categories:
- analytics
---
<div id="__ss_8433078" style="width: 425px;"><strong style="display: block; margin: 12px 0 4px;"><a title="Using Google Analytics with jQuery Mobile" href="http://www.slideshare.net/t32k/using-google-analytics-with-jquery-mobile">Using Google Analytics with jQuery Mobile</a></strong> <iframe frameborder="0" height="355" marginheight="0" marginwidth="0" scrolling="no" src="http://www.slideshare.net/slideshow/embed_code/8433078" width="425"></iframe> View more <a href="http://www.slideshare.net/">presentations</a> from <a href="http://www.slideshare.net/t32k">Koji Ishimoto</a></div>
<a href="http://gatracker.org/">とあるとこ</a>で、とある話をしたので、とあるスライド置いときますよ。

要点を言うと、jQuery MobileでAjax遷移してると、普通にGoogle Analytics置いてても作動しないから気をつけてねって話です。

<!--more-->
<h2>GATC for jQuery Mobile</h2>
僕はこうゆう感じでとりあえず対応しています。作動させるタイミングとフラグメント識別子を記録させるのがポイントです。あとはご自身のサイトに合わせてカスタマイズしていただければと思います。

<pre><code>//Account Setting
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-xxxxxxx-x']);

//Async Snippet
(function () {
    var ga = document.createElement('script');
    ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(ga, s);
})();

//Execute
$('[data-role="page"]').live('pageshow', function () {
    var u = location.hash.replace('#', '');
    u ? _gaq.push(['_trackPageview', u]) : _gaq.push(['_trackPageview']);
});
</code></pre>

<h2>jQuery Mobile XSS Problem</h2>
ちなみに上記と関係ないですけど、jQuery Mobileのアルファ版使ってる人は直ちに最新版にアップデートしときましょうってお知らせ。

[blackbirdpie url="https://twitter.com/#!/bulkneets/status/83174006110437377"]
<ul>
	<li><a href="http://hisasann.com/housetect/2011/06/jquerymobilexss.html">jQueryMobileのXSSに関する調査メモ at HouseTect, JavaScriptな情報をあなたに </a></li>
</ul>
最後になりましたが、主催者の<a href="https://twitter.com/#!/makitani">@makitani</a>さん、呼んでくださってありがとうございます。並びに素晴らしいユーザーMTGありがとうございます。
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 15px; top: 516px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=Tracking%20Snippet%0A&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 153px; top: 508px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=Tracking%20Snippet%0A&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 14px; top: 532px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=Tracking%20Snippet&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 102px; top: 513px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=Google%20A&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 34px; top: 511px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=oogle%20&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 259px; top: 514px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=GATG%20for%20jQuery%20Mobile&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
