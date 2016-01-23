---
date: 2009-06-22
title: 複数のGoogle Analytics Tracker Codeを併用する
categories: 
    - analytics
---

『[Google Analyticsを複数のプロファイルでトラッキング | 海外SEO情報ブログ](https://www.suzukikenichi.com/blog/tracking-access-by-mutiple-google-analytics-accounts/)』でGAのカスタマイズってほどでもないけど、トラッキングコードのTipsが紹介されている。要は`_gat._getTracker()`で初期化する際に、変数を2つ用意してあげればいいってこと。

ちょうど、『SIGMA DP2 : Special Contents』のサイトで似たようなコード見つけたので、挙げておく。

```html
<script type=“text/javascript”>
<script>
try {
	var pageTracker = _gat._getTracker(“UA-xxxxxx-1”);
	pageTracker._trackPageview();

	var pageTracker2 = _gat._getTracker(“UA-yyyyy-4”);
	pageTracker2._trackPageview();

} catch(err) {}
</script>
```

`pageTracker`と`pageTracker2`に格納してるんすね。違うアカウントで同じプロファイルを共有したい時ってゆう状態が、よくわからないんだけども。クライアントさんと制作者側が両方アクセス解析の情報を知りたいって時には便利なのかもしれないね。たぶん。

+ [Digital Intelligence Solutions to Empower Data Driven, Confident Decision Making | Cardinal Path](http://www.cardinalpath.com/)

上記にサイトはこんな感じのコードだった。

```html
<script>
try {
	var pageTracker = _gat._getTracker("UA-xxxxx-1");
	var isDev = window.location.href.search(/vkistudios.net/);

	if (isDev > -1)
	pageTracker._setDomainName(".vkistudios.net");
	else
	pageTracker._setDomainName(".vkistudios.com");

	pageTracker._setLocalRemoteServerMode();
	pageTracker._initData();
	pageTracker._trackPageview();
} catch (e) {}

//event tracking profile
try {
	var eventTracker = _gat._getTracker("UA-xxxxx-4");

	if (isDev > -1)
	eventTracker._setDomainName(".vkistudios.net");
	else
	eventTracker._setDomainName(".vkistudios.com");
	eventTracker._initData();
	eventTracker._trackPageview();
} catch (e) {}
</script>
```

イベントトラッキングとコンテンツの情報は分けて管理してるのかな。URLを判別して、`_setDomainName()`の引数を変えることでマルチドメイントラッキングを可能にしてる。

こんなふうにいろんなサイトのカスタマイズしたコード見てみたいもんだ。eコマーストランザクションとかどこか使ってないもんかな。