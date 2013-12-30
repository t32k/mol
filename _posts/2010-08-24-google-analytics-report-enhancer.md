---
layout: post
title: Google Analytics を強化するユーザースクリプト
categories:
- analytics
tags:
- google analytics
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '5703'
  _topsy_long_url: http://t32k.me/mol/2010/08/google-analytics-report-enhancer/
  topsy_short_url: http://bit.ly/afOadO
---
<img class="alignnone size-full wp-image-1562" title="roirevoluyion" src="/static/blog/2010/08/roirevoluyion.png" alt="" width="470" height="90" />

今回のやりたいことはですね、自分のブログについて言及されているページをいかに早く確認するかということです。

<!--more-->

<a href="/static/blog/2010/08/gare01.png"><img class="fig" title="トラフィック　＞　参照元サイト" src="/static/blog/2010/08/gare01-300x238.png" alt="" width="300" height="238" /></a>

Google Analytics では、プロファイルの左メニューの <em>トラフィック &gt; 参照元サイト</em> から自分のブログの参照元が分かりますね。しかし、これだと最初の段階でドメインレベルでしかわかりません。ページ（記事）レベルで知りたいと思うと、ドメインのリンクをクリックしていちいちドリルダウンしなきゃなりません。非常にめんどくさいです。ほかのドメインのページを調べたいと思うと、１回ドメインレベルまで上がってまた下がるといったフローをとらなければなりません。もう１回言いますが非常にめ・ん・ど・く・さ・いです！

ということで、フィルタで最初からドメイン/記事URLみたいな感じで書き出せばいいんじゃね？俺天才じゃね？と思ったのですが、そんなことはだれでも考えることで3年前くらいに同じ目的の記事がありました...
<ul>
	<li><a href="http://d.hatena.ne.jp/sotarok/20070627/1182959279">Google Analyticsで参照元の完全なURLを記録する - 肉とご飯と甘いもの @ sotarok</a></li>
</ul>
この方法を簡単に説明しますと、カスタムフィルタのフィールド値の「参照」ってのがですね、ドメイン/パスの情報を持ってまして、それを <em>ユーザー &gt; ユーザー定義</em> のメニューに書き出しているわけです。

なんか美しくないですねー。確かに自分も同じような考え方をしたのですが、参照元なので<em> ユーザー</em> ではなく <em>トラフィック</em> のカテゴリにあってほしいわけですよ、僕的に！とはいえ、Google Analytics では、左メニューに新たな項目を追加できないので、どこかしらの項目に上書きするしかないんですよね。。。んで、ユーザー定義がそのお役目をカスタム変数に引き渡したので、一番無難にカスタムした情報を書き出しやすいってことになってます。

う〜ん、困ったなぁーもっとエクセレントな方法ないかなと思ってたのですが
<ul>
	<li><a href="http://susumukatachi.jp/archives/1525?utm_source=blogfeed&amp;utm_medium=rss">標準の「セカンダリディメンション」にはない項目で深堀したい｜ススムカタチ</a></li>
</ul>
この記事の中で、あっさり解決方法が書いてありました。

ユーザースクリプト(<a href="https://addons.mozilla.org/ja/firefox/addon/748/">Greasemonkey</a>)でやっちゃう方法ですね。まず、グリモンをインスコしてもらって、今回のエントリの本題である<strong><a href="http://www.roirevolution.com/blog/2010/08/gare_updated_google_analytics_dimensions_drop-down.html">GARE(Google Analytics Report Enhancer)</a></strong>というのをインスコします（<strong><a onclick="javascript:pageTracker._trackPageview('/blog/downloads/GARE_refresh');" href="http://roirevolution.com/script/GAREnhancer.user.js">Get  the GARE</a></strong>をクリック）。これは文字通りGoogle Analyticsのレポートを強化してくれるユーザースクリプトなんですね。僕も前からインストールしていたのですが、メニューがほとんど英語なのであんまり使い方わかってなかったです...（最新バージョンだとある程度日本語に対応していますね）具体的にこれをインストールしたらどうなるかというと、<a href="http://www.google.com/support/analytics/bin/answer.py?hl=jp&amp;answer=142827">セカンダリディメンション</a>が以下のように増えます。

<a href="/static/blog/2010/08/gare02.png"><img class="fig" title="セカンダリディメンション前" src="/static/blog/2010/08/gare02-300x146.png" alt="" width="300" height="146" /></a>
<span style="color: #888888;">GAREインストール前のセカンダリディメンション</span>

<a href="/static/blog/2010/08/gare03.png"><img class="fig" title="GAREインストール後" src="/static/blog/2010/08/gare03-300x245.png" alt="" width="300" height="245" /></a>
<span style="color: #888888;">GAREインストール後のセカンダリディメンション</span>

なんということでしょう。わっさー項目が増えましたねヽ(´ー｀)ノﾜｰｲ！

ということで、今回したかったことはドメイン/パスのように表示させることだったので、GAREをインストール後、<em>トラフィック &gt; 参照元サイト </em>を表示させ、セカンダリディメンションからGAREによって追加された<em> 参照URL</em> を選択してください。

<a href="/static/blog/2010/08/gare041.png"><img class="fig" title="GARE 参照元ドメイン/パス" src="/static/blog/2010/08/gare041-300x259.png" alt="" width="300" height="259" /></a>

すると、上記のような形で表示されますのでドメインごとではなく記事URL単位で比較することができます（記事単位でソートとかできるのでハッピー♪）。

はい、これでフィルタでメニュー項目を汚すことなくやりたいことが実現できました。まぁこのGAREを使うと、参照元サイト以外でもいろんなセカンダリディメンションが適用できるのでおもしろい発見があると思います。みなさんも試してみてはどうでしょうか。

ちなみに、Google ChromeはネィティブでGreasemonkeyに対応していますので、Chromeでも<a onclick="javascript:pageTracker._trackPageview('/blog/downloads/GARE_refresh');" href="http://roirevolution.com/script/GAREnhancer.user.js">Get  the  GARE</a>をクリックするだけで即インストールでき、Firefox同様に使用できます。

もっと、詳しく知りたい方は<a href="http://susumukatachi.jp/category/blog">ススムカタチ×コトバ×しくみ</a>の<a href="http://twitter.com/susumukatachi">@susumukatachi</a>さんが素敵な記事を連発しているのでチェックすればOKかと思います。

susumukatachi++
