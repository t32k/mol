---
date: 2015-03-31
title: gFaceeeに最新コミット日時を強調する機能追加した
subtitle: A Chrome Extension for displaying avatar on GitHub
categories: development
excerpt: Webフロントエンド技術に関して非常に多くの技術情報を日々捌いているLayzieさん曰く、『記事の日付は必ず確認』しなければならない。
ogimage: http:t32k.me/mol/images/2015/0331-00.png
---

[Webフロントエンド技術に関して非常に多くの技術情報を日々捌いているLayzieさん](http://layzie.hatenablog.com/entry/20141104/1415076724)曰く、『__記事の日付は必ず確認__』しなければならない。つい先日、2年前くらいのはてブ記事をドヤ顔でSlackグループに投げて言われた言葉だ。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4844334220/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51whkjxFOAL._SL160_.jpg" alt="開発者のためのChromeガイドブック (Google Expert Series)" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4844334220/warikiru-22/" name="azlinklink" target="_blank">開発者のためのChromeガイドブック</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.3.30</div></div><div class="azlink-detail">吉川 徹,あんどうやすし,田中 洋一郎,小松 健作<br />インプレスジャパン<br /></div><div class="azlink-review" style="margin-top:10px;margin-bottom:10px"></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4844334220/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

情報の鮮度は非常に重要だということを改めて理解しつつ、二度とこのような失態を犯さないためにどうすればよいか考えた結果、いったん、はてブは置いといて、GitHubの最新コミット日時を強調するChrome拡張機能を作った。

ご存知の通り、GitHubの時間表記は相対的な3 minutes agoと 3 hours agoとか、May 14, 2012とか、なんか直感的に新しいのか古いのか分かりにくい（というか読み取るのが面倒くさい）。あと最近流行りのReact.jsではなく、今さらBackbone.jsを勉強してるけど、関連リポジトリの更新が普通に2年前で止まってるとかあったので、ちょっと注意しないとと思った次第。

![](/mol/images/2015/0331-00.png)

+ 1週間未満: Bright Green
+ 1ヶ月未満: Green
+ 6ヶ月未満: Yellow
+ 1年未満: Orange
+ 1年以上: Red

というわけで、上記のような基準で各リポジトリトップのlatest commitの日時を色付けするようにした。さりげない感じで強調してくれるので個人的に気に入っている。とりあえず、赤色（1年以上コミット無し）なら注意してみてみようなど色で判断できるようにした。

もちろん、コミットが止まっているのは枯れていて安定しているって意味かもしれないので、必ずしも悪いことじゃない。しかし、変化の激しいフロントエンド界隈で生きているので、やっぱ定期的にメンテなりしてあるほうがいいかなと思っている。

![](/mol/images/2015/0331-01.png)

+ __[gFaceee - Chrome ウェブストア](https://chrome.google.com/webstore/detail/gfaceee/fgkdbhnipaaeokfjgdmpejglfepclgbk)__

GitHubのニュースフィード上でアイコンを表示させるgFaceeeの追加機能としてリリースしましたのでよければ使ってくださいませ。
