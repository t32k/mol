---
layout: post
title: ATNDer's List Maker
categories:
- javascript
tags:
- Greasemonkey
status: publish
type: post
published: true
meta:
  pvc_views: '2964'
  _edit_last: '1'
  _aioseop_keywords: Greasemonkey
  _aioseop_description: 最近、もっぱらグリモンに夢中です。まさしくDo It Yourself精神まっしぐら、ネコまっしぐらです。
---
<a href="https://github.com/t32k/ATNDer-List-Maker/blob/master/atnder_list_maker.user.js"><img class="fig" title="atnder_list_maker.user.js" src="http://t32k.me/mol/file/2011/01/am.png" alt="" width="470" height="123" /></a>

最近、もっぱらグリモンに夢中です。まさしくDo It Yourself! 精神まっしぐら、ネコまっしぐらです。

で、こんなん作りました。
<ul>
	<li><a href="https://github.com/t32k/ATNDer-List-Maker"><strong>t32k/ATNDer-List-Maker - GitHub</strong></a></li>
</ul>
グリモン（ver 0.9+）をインストールしたFirefoxもしくは、Google Chromeで、atnder_list_maker.user.jsをクリックしてrawって書いてあるとこをクリックしたらインストールできます。

これなにかと言いますと、ATNDのユーザーページに行ってもらうと、直近１件で参加・管理しているイベントの参加者のTwitterリストが表示できます。こんな感じで。
<ul>
	<li><a href="https://github.com/t32k/ATNDer-List-Maker/wiki/Screen-shots">https://github.com/t32k/ATNDer-List-Maker/wiki/Screen-shots</a></li>
</ul>
ATNDにGoogleアカウントで入ってる人やTwitterIDを紐付けてないひとのはリンクつかないです。

こうゆうのを作ったのも最近ATNDでイベントを開催することが多くなり、参加後のレポートを書くのに参加者のリスト（Twitter）あると便利だなって思ったので作ってみました。
<h3>ツマづいた点</h3>
これを実現するにあたって、<a href="http://api.atnd.org/">ATNDのAPI</a>使えばいいんだろうなと最初考えたのですが、なにぶんAPIなんてものは使うものはこれが初めてでしばらくAPIのページをにらめっこ。なんかとりあえず、レスポンス形式を選ばなあかん、XML, ATOM, JSON..いろいろある。JSONってのよく聞くのでこれにしよう。あれ、JSONPって似たようなもんもあるぞ。どっちがいいねん？
<ul>
	<li><a href="http://d.hatena.ne.jp/jdg/20090902/1251851867">JSONとJSONPの違い - あと味</a></li>
	<li><a href="http://akiyoshi220.blogspot.com/2010/02/jsonp.html">コイケアキヨシ blog: JSONPの使い方</a></li>
</ul>
ということで、とりあえず、JSOPを使うことにした。

ごにょごにょして、ローカルのHTML ファイルで作成していたときはうまく動いていたのに、グリモン化すると動かなくなった＞＜なんで？というこで、ググッたらこんなん出てきた。
<ul>
	<li><a href="http://d.hatena.ne.jp/ku0522/20080829/1220004795">Greasemonkeyで定義した関数をJSONPで呼び出したい - ロックスターになりたい
</a></li>
</ul>
うう〜んよくわかんないけど、実行環境が違うっぽいということで、実行するスクリプトを外部ファイル化して、グリモンではその外部ファイルをページで読み込むだけにしてみたら動いた。

とまぁ、実際はこれ以外に、管理しているイベントがなかった場合とか動かなかったりして地味になやんでたりしたけど、とりあえず、ググッたらなんとかなる！

以上！

あ、あと最初userscripts.orgに登録してたけど、なんか調子悪いのでgithubにのっけてみた。GUIで操作できるTowerってapp使ったら僕でもできたよ！てか、未だに細かいこと分かってないので、求む、Git勉強会 for Webデザイナー＞＜
<ul>
	<li><a href="http://linker.in/journal/2010/12/gitguitower.php">GUIでGitを使える「Tower」をさらっと触ってみた｜linker journal</a></li>
	<li><a href="http://linker.in/journal/2010/12/towergithub.php">TowerでGitHubをつかってみる｜linker journal</a></li>
</ul>
あ、でもちょっとしたUserScriptだったら、<a href="https://gist.github.com/">Gist</a>に登録したほうが便利かも。
<ul>
	<li><a href="http://d.hatena.ne.jp/secondlife/20080724/1216860029">gist.github.com で GreaseMonkey Script を管理しよう - 川o・-・）＜2nd life </a></li>
</ul>
