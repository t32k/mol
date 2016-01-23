---
date: 2011-06-28
title: jQuery MobileでGoogle Analyticsを使うために気をつけなければいけないこと
subtitle: Using Google Analytics with jQuery Mobile
categories: 
    - analytics
excerpt: jQuery MobileでAjax遷移してると、普通にGoogle Analytics置いてても作動しないから気をつけてねって話です。
ogimage: http://i.imgur.com/wtaftdU.png
---

<iframe src="//www.slideshare.net/slideshow/embed_code/key/B85ZvFNIIylyud" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen></iframe>

とあるとこで、とある話をしたので、とあるスライド置いときますよ。 要点を言うと、jQuery MobileでAjax遷移してると、普通にGoogle Analytics置いてても作動しないから気をつけてねって話です。

## GATC for jQuery Mobile

僕はこうゆう感じでとりあえず対応しています。作動させるタイミングとフラグメント識別子を記録させるのがポイントです。あとはご自身のサイトに合わせてカスタマイズしていただければと思います。

```javascript
//Account Setting
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
```

### jQuery Mobile XSS Problem

ちなみに上記と関係ないですけど、jQuery Mobileのアルファ版使ってる人は直ちに最新版にアップデートしときましょうってお知らせ。

+ [jQueryMobileのXSSに関する調査メモ at HouseTect, JavaScriptな情報をあなたに](http://hisasann.com/housetect/2011/06/jquerymobilexss.html)

最後になりましたが、主催者の@makitaniさん、呼んでくださってありがとうございます。並びに素晴らしいユーザーMTGありがとうございます。