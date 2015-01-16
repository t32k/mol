---
date: 2014-08-04
title: 修正しやすいCSSとは
subtitle: 『CSS設計の教科書』はモダンCSSを探る最適なマップ
categories: books
cover_image: "/2014/08-04-cover.jpg"
excerpt: "Web制作者のためのCSS設計の教科書 モダンWeb開発に欠かせない「修正しやすいCSS」の設計手法"
---

[@hiloki](https://twitter.com/hiloki)という男がいる。この男と初めて出会ったのは7年前だろうか、当時細々と石川でブログを書きながらWebデザイナーをしていた僕に初めて勉強会で声をかけてくれた人物である。

それ以来、当時彼が住んでいた大阪の勉強会と石川の勉強会で互いに参加しあったりして親交を深めていった。ついには2年という短い間ではあったが、某緑の会社で同僚として働けたことは本当かけがえのないものと感じている。

そんな彼が最近2冊目の単著を出した。1冊目の『[HTML5＋CSS3で作る 魅せるiPhoneサイト](http://www.amazon.co.jp/HTML5%EF%BC%8BCSS3%E3%81%A7%E4%BD%9C%E3%82%8B-%E9%AD%85%E3%81%9B%E3%82%8BiPhone%E3%82%B5%E3%82%A4%E3%83%88-iPhone-iPad-touch%E5%AF%BE%E5%BF%9C/dp/4899772750%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4899772750)』はもちろん購入して読書済だが、本当に丁寧に書いてあり分かりやすかった印象がある。そんな彼の出す本だから間違いないのは当たり前だが、特筆すべきは扱っているテーマだろう。

最近のCSSのWeb参考書というと、CSS3でこんなことができちゃいます〜、だとかアニメーションでこんなことがっ！？とか、こんなグラフィカルな表現がCSSだけで！！みたいなものが多い。たぶん、JavaScriptがバックエンドのエンジニアが片手間にやるような言語と思われているように、CSSもまたWebデザイナーの片手間言語だと思われているからだろう。

しかし、WebサイトにしてもWebアプリにしても公開して終わり！ってことほとんどないだろう。植物に毎日水を与えるように、Webサイト/アプリもまたメンテ・機能追加・リニューアルなどしていかなければならない。

そうゆうわけで、いかにメンテしやすい、変更に対応しやすくするか、『設計』という概念が必要になってくる。本書ではそれをテーマにしている。CSS自体は適当にHTMLにclass属性を与えてそれに対してスタイリングしていく、極めてシンプルなものだ。シンプルがゆえに誰でも扱うことが出来るし、シンプルがゆえに何もできない。だからなんにも考えなしに書いていったらすぐに破綻する。

こういった問題に真摯に対峙している人は少ない。なぜならデザイン的なものを表現するのにエンジニア的マインドも必要になってくるからだ。GitHub社にCSSエンジニアと呼ばれる肩書の人が数十人もいて、その中には情報処理の博士号を取った人なんかがCSSを書いているらしいが、普通そういった人たちの知見は一部の海外エンジニアのブログでしか拝めない。

![カラーで見やすい！](/mol/images/2014/08-04-fig01.jpg)

本書で扱っている、[BEM](http://bem.info/)や[CSSO](http://css.github.io/csso/)、[CSScomb](http://csscomb.com/)とかはロシアのYandex社の人が中心に開発してたり、毎回イケてるCSS記事を書いてくれる[CSS Wizardry](http://csswizardry.com/)はイギリスだったり、[SMACSS](https://smacss.com/ja)の[Jonathan Snook](http://snook.ca/)はカナダだし、[Kite](https://github.com/hiloki/kitecss)や[FLOCSS](https://github.com/hiloki/flocss)（by @hiloki）、[Maple](https://github.com/t32k/maple)や[StyleStats](https://github.com/t32k/stylestats)（by @t32k）はもちろん日本から発信してるものだったりして、このチョイスで一冊の本にまとめられるのは世界中でも@hilokiしかいないだろう。

余談だけど、本書の『はじめに』で[@cssradar](https://twitter.com/cssradar)に感謝を述べているが、僕からも感謝の意を述べたい。@cssradarのSMACSS翻訳プロジェクトに参加したのをキッカケに、CSSってこんなに奥深いものなのかと知り、僕らは互いに切磋琢磨してCSSに関する技術を向上させることができた。しかも、それを実践する環境は当時の緑の会社にあって、本当に良い環境だったと今は思う。

本書はそういったCSS設計を中心にモダンなCSS開発に関してのノウハウが体系的に、果てはWeb Componentsまで古今東西を通じてまとめらていながら、書籍版が __2,376円__ 、Kindle版なら __28%OFFの1,710円__ の破格の安さで購入することが出来る！！

決して、これを読んだからといてすぐに理想的なCSSを書けるわけではないが、すくなくとも混沌としたCSSの開発現場をサバイバルするための最適なマップとして活用できることだろう。


<table  border="0" cellpadding="5"><tr><td valign="top"><a href="http://www.amazon.co.jp/Web%E5%88%B6%E4%BD%9C%E8%80%85%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AECSS%E8%A8%AD%E8%A8%88%E3%81%AE%E6%95%99%E7%A7%91%E6%9B%B8-%E3%83%A2%E3%83%80%E3%83%B3Web%E9%96%8B%E7%99%BA%E3%81%AB%E6%AC%A0%E3%81%8B%E3%81%9B%E3%81%AA%E3%81%84%E3%80%8C%E4%BF%AE%E6%AD%A3%E3%81%97%E3%82%84%E3%81%99%E3%81%84CSS%E3%80%8D%E3%81%AE%E8%A8%AD%E8%A8%88%E6%89%8B%E6%B3%95-%E8%B0%B7-%E6%8B%93%E6%A8%B9/dp/4844336355%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4844336355" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51rsbQOrZ0L._SL160_.jpg" border="0" alt="Web制作者のためのCSS設計の教科書 モダンWeb開発に欠かせない「修正しやすいCSS」の設計手法" /></a></td><td valign="top"><font size="-1"><a href="http://www.amazon.co.jp/Web%E5%88%B6%E4%BD%9C%E8%80%85%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AECSS%E8%A8%AD%E8%A8%88%E3%81%AE%E6%95%99%E7%A7%91%E6%9B%B8-%E3%83%A2%E3%83%80%E3%83%B3Web%E9%96%8B%E7%99%BA%E3%81%AB%E6%AC%A0%E3%81%8B%E3%81%9B%E3%81%AA%E3%81%84%E3%80%8C%E4%BF%AE%E6%AD%A3%E3%81%97%E3%82%84%E3%81%99%E3%81%84CSS%E3%80%8D%E3%81%AE%E8%A8%AD%E8%A8%88%E6%89%8B%E6%B3%95-%E8%B0%B7-%E6%8B%93%E6%A8%B9/dp/4844336355%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4844336355" target="_blank">Web制作者のためのCSS設計の教科書<br>モダンWeb開発に欠かせない「修正しやすいCSS」の設計手法</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&l=ur2&o=9" width="1" height="1" style="border: none;" alt="" /><br />谷 拓樹 <br /><br />インプレスジャパン  2014-07-24<br /><a href="http://www.amazon.co.jp/Web%E5%88%B6%E4%BD%9C%E8%80%85%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AECSS%E8%A8%AD%E8%A8%88%E3%81%AE%E6%95%99%E7%A7%91%E6%9B%B8-%E3%83%A2%E3%83%80%E3%83%B3Web%E9%96%8B%E7%99%BA%E3%81%AB%E6%AC%A0%E3%81%8B%E3%81%9B%E3%81%AA%E3%81%84%E3%80%8C%E4%BF%AE%E6%AD%A3%E3%81%97%E3%82%84%E3%81%99%E3%81%84CSS%E3%80%8D%E3%81%AE%E8%A8%AD%E8%A8%88%E6%89%8B%E6%B3%95-%E8%B0%B7-%E6%8B%93%E6%A8%B9/dp/4844336355%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4844336355" target="_blank">Amazonで詳しく見る</a></font><font size="-2"> by <a href="http://www.goodpic.com/mt/aws/index.html" >G-Tools</a></font></td></tr></table>

