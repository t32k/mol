---
layout: post
title: Coda.appでjQuery Mobileをコード補完
categories:
- markup
- mobile
tags:
- jquery mobile
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '10953'
  _aioseop_description: ごーごーれいきゅーさんのために作りました(｀･ω･´)ゞ
---
<img class="alignnone size-full wp-image-3240" title="Coda.app" src="/static/blog/2011/05/cj.png" alt="" width="470" height="120" />

どもー全国数十万のCoda.appユーザーの皆さん、t32kでございます。

MacBook AirにCSをインスコするのはちょっと気が引けたので円高もあって<strong><a href="http://www.panic.com/coda/">Coda.app</a></strong>を最近買いました。なんかいろいろ綺麗でたちまち好きになりました。どうせならこれでjQuery Mobileゴリゴリ書きたいなと思うようになりやんした。

<!--more-->

<strong><a href="http://jquerymobile.com/">jQuery Mobile</a></strong>と言いますと、最近ではアルファ版（2011/6/1現在）でもあるにも関わらずDw CS 5.5で標準装備されるなど飛ぶ鳥落とす勢いでやんす。だからってCS5.5買いたくナイヨ！

ってことで、Coda.appでコード補完色々いじくってみましたってのが今回のエントリの主旨。

Coda.appでコード補完を司っているのが、<strong>CodaCompletion.plist</strong>です。これをいじって作成しました。ファイルの在り処は以下です。Coda.appを右クリックして「パッケージの内容を表示」を選択するとディレクトリを潜れます。

[HTML]
Coda.app/Contents/Resources/Modes/HTML.mode/Contents/Resources/CodaCompletion.plist
[/HTML]

CodaCompletion.plistをDLしたものに置き換えてあげるだけです。安全のために元のファイルはどっかにバックアップしておいたほうが良いですよ。
<ul>
	<li><a href="http://d.hatena.ne.jp/pikotea/20101019/1287484040">jQuery Mobile リファレンス的なもの - へっぽこプログラマーの日記</a></li>
</ul>
このページ見て作りました。
<h2>Usage</h2>
<iframe frameborder="0" height="264" src="http://player.vimeo.com/video/24462566?title=0&amp;byline=0&amp;portrait=0" width="470"></iframe>

上記、動画を見てもらえるとだいたい分かると思います。dataなんちゃらと属性を打つといろ色出てきます。
(data-まで打つと途切れます。誰か回避方法教えてください＞＜)

個人的にはdata-iconが覚えるのには値が多すぎるので便利かなと思ってますｗ

コード補完ついでにクリップ（スニペット）的なものもちょっとだけ用意しました。<strong>jQuery Mobile.clips</strong>をダブルクリックすればインスコできます。
<ul>
	<li><strong>jqm + TAB</strong> でテンプレート挿入</li>
	<li><strong>page + TAB</strong> でdata-role="page"のコードを挿入</li>
	<li><strong>lang + TAB</strong> でローカリゼーションのコード挿入</li>
</ul>
<h2>Download</h2>
<a onclick="_gaq.push(['_trackEvent', 'DL', 'coda_jqm'])" href="https://github.com/t32k/Coda-Completion-for-jQuery-Mobile"><img class="alignnone size-full wp-image-3242" title="Download!" src="/static/blog/2011/05/zip.png" alt="" width="128" height="128" /></a>
(Coda Completion for jQuery Mobile - GitHub)

問題がありましたらご指摘下さい。
（時間あればアップデートしていきます...）
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 45px; top: 1090px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=la&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
<div id="extensionsWeblioEjBx" style="position: absolute; z-index: 2147483647; left: 226px; top: 1103px; display: none;"><iframe frameborder="0" height="205" name="weblioExtensionsFrame" scrolling="no" src="http://api.weblio.jp/act/quote/v_1_0/e/?q=v1.1&amp;type=elarge&amp;opul=chrome-extension%3A%2F%2Foingodpdjohhkelnginmkagmkbplgema%2Foptions.html" width="320"></iframe></div>
