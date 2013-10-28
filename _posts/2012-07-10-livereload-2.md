---
layout: post
title: LiveReload 2入れてみた
categories:
- development
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '5037'
---
<p style="text-align: center;"><a href="http://livereload.com/"><img class="aligncenter fig" title="LiveReload 2" src="http://t32k.me/mol/file/2012/07/lr.png" alt="LiveReload 2" width="520" /></a></p>

<ul>
	<li><a href="http://livereload.com/"><strong>LiveReload (a happy land where browsers don't need a Refresh button)</strong></a></li>
</ul>
こんちわ！<a href="http://t32k.me/mol/log/sublime-text-2/">Sublime Text 2</a>の次はLiveReload 2 (Mac app)の紹介だよ。これまた感動したので。

みなさんこう考えたことはないだろうか？「もうすぐ俺も30だ。これから一体何回ブラウザリロードしていかなきゃいけないんだよ！これまで何万回リロードしてきたと思ってんだよ！！人生リロードできねーんだよ！！！」ってね。僕は考えたことないです。むしろ考えることすらせず、ただ盲目的にリロードしてきました。でも、LiveReloadを知った今では、これまでの自分が恥ずかしいです。このアプリなんて便利なんでしょう。もうちょっと早く教えてくれよ！って感じです。

<!--more-->

事の発端はですね、Sassを使うようになったわけですが、コンパイルするのに黒い画面を見るのが嫌なわけでして、なんかしらGUIのアプリないかなと思って、<a href="http://mhs.github.com/scout-app/">Scout</a>を使ってたわけです。まぁこれで十分満足してたわけですが、通りすがりの<a href="https://twitter.com/cssradar/">@cssradarさん</a>が、「LiveReloadいいよ！LiveReloadいいよ！」ってうるさく言ってきまして「あーまためんどくせーな」と思ってたわけです。しかしあまりのゴリ押し説明でこれが便利だということが理解できました。ありがとう！Radarさん！！

LiveReloadは自動リロードのほかに、CoffeeScript, SASS, LESSのコンパイルもしてくれるから薦めてきたみたい。Codekitも同じようなことできるらしいけど、Codekitより安い！画像の圧縮はないけども、フリーの<a href="http://imageoptim.com/">ImageOptim</a>と<a href="http://www.jpegmini.com/">JPEGmini</a>もあるし、開発段階ではそんなに頻繁に使うことないし、最終的にサーバー上げるときに圧縮すればいいので別にひとつのアプリとして統合してなくてもいいかなと思ってる。

簡単にデモ動画撮ってみました。基本ファイルを保存したら自動的にリロードしてくれます。素敵です。ちゃんとSassもCSSにコンパイルしてくれてます。更新のためのlivereload.js（拡張機能入れれないやつは）ってのを入れる必要があるけど、前回も紹介した<a href="https://github.com/robcowie/SublimeTODO">SublimeTODO</a>入れとけば消し忘れもないでしょう、多分、知らんけど。

<iframe src="http://www.youtube.com/embed/FiaLBYPQDOg" frameborder="0" width="500" height="375"></iframe>

個人的にはiOSシミュレーターで縦幅が長いページとかコーディングしながら確認してるとURLバーまで戻ってリロードしなきゃいけないのがたまらなくめんどくさかったんで、まさに神ツールだぜって思ったんですけど。iOSシミュレーターMobile SafariでもCmd+R的なショートカットとかあるんですかね?。だれかおせーてください、エロイ人！
