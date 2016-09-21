---
date: 2014-08-04
title: 修正しやすいCSSとは
subtitle: CSS設計の教科書はモダンCSSを探る最適なマップ
categories: 
    - books
cover_image: "/2014/08-04-cover.jpg"
excerpt: "Web制作者のためのCSS設計の教科書 モダンWeb開発に欠かせない「修正しやすいCSS」の設計手法"
---

[@hiloki](https://twitter.com/hiloki)という男がいる。この男と初めて出会ったのは7年前だろうか、当時細々と石川でブログを書きながらWebデザイナーをしていた僕に初めて勉強会で声をかけてくれた人物である。

それ以来、当時彼が住んでいた大阪の勉強会と石川の勉強会で互いに参加しあったりして親交を深めていった。ついには2年という短い間ではあったが、某緑の会社で同僚として働けたことは本当かけがえのないものと感じている。

そんな彼が最近2冊目の単著を出した。1冊目の『[HTML5＋CSS3で作る 魅せるiPhoneサイト](https://www.amazon.co.jp/dp/4899772750/?tag=warikiru-22)』はもちろん購入して読書済だが、本当に丁寧に書いてあり分かりやすかった印象がある。そんな彼の出す本だから間違いないのは当たり前だが、特筆すべきは扱っているテーマだろう。

最近のCSSのWeb参考書というと、CSS3でこんなことができちゃいます〜、だとかアニメーションでこんなことがっ！？とか、こんなグラフィカルな表現がCSSだけで！！みたいなものが多い。たぶん、JavaScriptがバックエンドのエンジニアが片手間にやるような言語と思われているように、CSSもまたWebデザイナーの片手間言語だと思われているからだろう。

しかし、WebサイトにしてもWebアプリにしても公開して終わりってことほとんどないだろう。植物に毎日水を与えるように、Webサイト/アプリもまたメンテ・機能追加・リニューアルなどしていかなければならない。

そうゆうわけで、いかにメンテしやすい、変更に対応しやすくするか、『設計』という概念が必要になってくる。本書ではそれをテーマにしている。CSS自体は適当にHTMLにclass属性を与えてそれに対してスタイリングしていく、極めてシンプルなものだ。シンプルがゆえに誰でも扱うことが出来るし、シンプルがゆえに何もできない。だからなんにも考えなしに書いていったらすぐに破綻する。

こういった問題に真摯に対峙している人は少ない。なぜならデザイン的なものを表現するのにエンジニア的マインドも必要になってくるからだ。GitHub社にCSSエンジニアと呼ばれる肩書の人が数十人もいて、その中には情報処理の博士号を取った人なんかがCSSを書いているらしいが、普通そういった人たちの知見は一部の海外エンジニアのブログでしか拝めない。

![カラーで見やすい！](/mol/images/2014/08-04-fig01.jpg)

本書で扱っている、[BEM](http://bem.info/)や[CSSO](http://css.github.io/csso/)、[CSScomb](http://csscomb.com/)とかはロシアのYandex社の人が中心に開発してたり、毎回イケてるCSS記事を書いてくれる[CSS Wizardry](http://csswizardry.com/)はイギリスだったり、[SMACSS](https://smacss.com/ja)の[Jonathan Snook](http://snook.ca/)はカナダだし、[Kite](https://github.com/hiloki/kitecss)や[FLOCSS](https://github.com/hiloki/flocss)（by @hiloki）、[Maple](https://github.com/t32k/maple)や[StyleStats](https://github.com/t32k/stylestats)（by @t32k）はもちろん日本から発信してるものだったりして、このチョイスで一冊の本にまとめられるのは世界中でも@hilokiしかいないだろう。

余談だけど、本書の『はじめに』で[@cssradar](https://twitter.com/cssradar)に感謝を述べているが、僕からも感謝の意を述べたい。@cssradarのSMACSS翻訳プロジェクトに参加したのをキッカケに、CSSってこんなに奥深いものなのかと知り、僕らは互いに切磋琢磨してCSSに関する技術を向上させることができた。しかも、それを実践する環境は当時の緑の会社にあって、本当に良い環境だったと今は思う。

決して、これを読んだからといてすぐに理想的なCSSを書けるわけではないが、すくなくとも混沌としたCSSの開発現場をサバイバルするための最適なマップとして活用できることだろう。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00M0ESXUI/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-na.ssl-images-amazon.com/images/I/51nSEOKWSrL._SL160_.jpg" alt="Web制作者のためのCSS設計の教科書 モダンWeb開発に欠かせない「修正しやすいCSS」の設計手法" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00M0ESXUI/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">Web制作者のためのCSS設計の教科書 モダンWeb開発に欠かせない「修正しやすいCSS」の設計手法</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2016.7.18</div></div><div class="azlink-detail">谷 拓樹<br />インプレス<br />売り上げランキング: 7548<br /></div><div class="azlink-review" style="margin-top:10px;margin-bottom:10px"></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00M0ESXUI/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>
