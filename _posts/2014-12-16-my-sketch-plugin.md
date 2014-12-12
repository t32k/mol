---
layout: post
title: Material Design Color Paletteプラグインつくった
subtitle: Sketch 3 Advent Calendar 2014
categories: blog
cover_image: "/2014/12-16-1-cover.png"
excerpt: Sketch app plugin for displaying Google material design color palette.
---

[Sketch 3 Advent Calendar 2014 - Adventar](http://www.adventar.org/calendars/347) 16日目です。

表題の通りなんですけど、Sketch.appのプラグインとか作ってみたいなーて思ってて作ったわけです。

<iframe src="//player.vimeo.com/video/114320997?title=0&amp;byline=0&amp;portrait=0" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

+ __[t32k/material-design-color-palette-sketch-plugin](https://github.com/t32k/material-design-color-palette-sketch-plugin)__

GoogleのMaterial Designってありますよね？あれの色見本的なものを生成してくれるやつです。公式サイトみたらIllustrator/Photoshop用のSwatchesファイルがあったんですけど、Sketch用のなかったわけですよ！（そもそもそんなファイルSketchにはないのか？）よくわかりませんが、なかったら自分で作りなはれ精神で作りました。

+ [Color - Style - Google design guidelines](http://www.google.com/design/spec/style/color.html)

個人的に明度ごとに各色のパレット作り出すやつが欲しかったやつなのでお気に入りです。

なんか不具合とかあったら[@t32k](https://twitter.com/t32k)まで、ご連絡くださいませ。

## Sketch Pluginの作り方

+ [Bohemian Coding - Sketch Developer](http://bohemiancoding.com/sketch/support/developer/)

上記の公式リファレンスを見れば作れる。。。。なんてことはない。CocoaScriptという、JavaScriptの文法でCocoaフレームワークにアクセスできる代物。てか、Cocoaフレームワークが分からんし。。なんかカッコ多くてよくわからんし、リファレンス不親切だしって感じで、作りたいものに似たプラグインを探して真似するのが最善の策かと思われる。

みんなCocoaに精通しているのか、それともググりながらがんばってるのか、いずれにせよ、Sketchプラグインのエコシステムはデベロッパーの皆様の多大なる努力の賜物であることを身にしみた。

## Sketch Pluginを作ったら…

[Sketch Toolbox](http://sketchtoolbox.com/)という、Sketchプラグインを管理するアプリがあるのですけど、せっかくなのでここに登録したいと思いまして、どうしたら登録できるのだろうと探していたら、どうやら[sketchplugins/plugin-directory](https://github.com/sketchplugins/plugin-directory)ここにプルリクを送ればいいっぽい。

なんとまぁアナログな！Bohemian Codingさんはプラグインサーバー立てて、そこにアップロードできるようにすればいいのになー（儲かってないのかなー）。

あとは、Sketchのリソース関連で有名なSketch App Sourcesに載せるため[Submit free resources](http://www.sketchappsources.com/submit-free-resource.html)に申請しておきましょう。

とまぁ作ってみたけど、もっと環境がよかったらなーもっと作ってみたいと思うけど、満足したので、もうプラグイン作るのはお休み(´･ωゞ)。

