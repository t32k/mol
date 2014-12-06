---
layout: post
title: Sublime Text Icon 2014
subtitle: ちょっとヨセミティ？ちょっとSketch使ってみぃ？
categories: design
cover_image: "/2014/12-16-cover.png"
excerpt: ちょっとヨセミティ？ちょっとSketch使ってみぃ？
---

[Sketch 3 Advent Calendar 2014](http://www.adventar.org/calendars/347)の16日目です、たぶん。知らんけど。

今日はSketchを使ってYosemiteライクなアイコンを作ってみようって話です。

今年の5月に[Sketch3ハジメマシタ](/mol/log/sketch3/)って言っておきながら、それ以来まったくSketchを使ってなかったことを反省したので、最近、[SketchCasts](http://www.sketchcasts.net/)を見ながら勉強してました。余談ですが、SketchCastsは月$8でSketch.appの使い方をスクリーンキャストで学習できるサービスです。やっぱ実際に動かす・制作してるとこ見るのが一番理解が速いと思います。

そんなわけで、ひと通り使い方を学習したので何を作ろうかなと思いまして、そういえば、昔[Sublime Text](http://www.sublimetext.com/)のアイコン作ったなーと思いだしまして、それをリデザインしてみようかと思います。

![旧バージョン](http://t32k.me/static/blog/2012/12/icon2.jpg)

+ [Sublime Text 2 のアイコンをなんとかする — MOL](/mol/log/present-for-you/)

上記のアイコンですが、2年前に作った、いわゆるスキューモーフィズムっぽいやつで、しかもiOSのアイコンベースにしていたので、デスクトップアプリのアイコンとして使うにはなんだか野暮ったいです。もっと現代っぽくしたいです。もっとフラットっぽくしたいです。

+ [Inspecting Yosemite's Icons](http://martiancraft.com/blog/2014/07/inspecting-yosemite-icons/)

最新のYosemiteのアイコンの仕様に関しては上記の記事を読むと良いです。僕は読んでないですが、とりあえずはなんかガイドラインが引いてあるテンプレートみたいなものがあるのだろう、そしてそれに沿って作れば、それっぽくなるんじゃね？って思い探してみました。

+ [OS X Yosemite Icon Grid Sketch freebie - Sketch App Sources](http://www.sketchappsources.com/free-source/630-os-x-yosemite-icon-grid-sketch-freebie-resource.html)
+ [Apple OS X Yosemite Icons Sketch freebie - Sketch App Sources](http://www.sketchappsources.com/free-source/563-osx-yosemite-icons-sketch-freebie.html)

はい、ありました。Sketchのこうゆうエコシステムはほんと素敵ですね。


![新バージョン](/mol/images/2014/12-16-fig01.jpg)

あとはガイドにそって光源とか注意してあまりゴテゴテしないようにすれば、できあがりです♪

+ [t32k/sublime-text-icon - GitHub](https://github.com/t32k/sublime-text-icon)

ダウンロードは上記からどうぞ。自分でも作ってみたいって方は上記のレポジトリをフォークして作ってみるといいよ。

あとICNSファイルを作るときに、下記のオンラインツールを作ってたんだけど、どうも高解像度のアイコンが生成されなくて、Appleの標準のICNSファイル見たら10サイズあったのだけど、オンラインだと5サイズしか生成されなかったので、[Macアプリ](https://itunes.apple.com/us/app/iconvert-icons/id515197296?mt=12&ign-mpt=uo%3D4)買ったらちゃんとフルサイズ作れました。

+ [Online icon converter for png, ico, and icns - iConvertIcons](http://iconverticons.com/online/)

あとで知ったけど、`iconutil`ってコマンドで作成できるらしい。俺の500円。。

+ [iconutil(1) Mac OS X Manual Page](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/iconutil.1.html)
