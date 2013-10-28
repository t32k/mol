---
layout: post
title: TextMateで日本語入力を可能にする
categories:
- processing
tags:
- textmate
status: publish
type: post
published: true
meta:
  pvc_views: '8057'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/08/japanese-input-in-textmate.html
  _edit_last: '1'
---
<img src="http://lh6.ggpht.com/_1drnogi3vdg/SoleMR6bqcI/AAAAAAAAAiM/mOGlTd02pt4/head.png" alt="" />

<a href="http://warikiru.blogspot.com/2009/08/textmate-meets-processing.html">前回のエントリでProcessingのBundleも入れて</a>満足な僕ですが、考えてみればTextMateは日本語入力を受けつけてないという現実にぶち当たりました。
<h3>日本語入力を可能にする</h3>
なぁに、解決方法はプラグインを入れるだけさ ~ﾍ(´ー｀*) ｶﾓｰﾝ
以下のサイトからCJKInput20061110.zipをダウンロードして、
<ul>
	<li><a href="http://hetima.com/textmate/index.html">TextMate stuff - hetima.com</a></li>
</ul>
解凍したファイルの中にあるCJK-Input.tmpluginを ~/Library/Application Support/TextMate/PlugIns/ に放り込むだけで日本語入力が可能になる。
<span style="color: #666666; font-size: 85%;">（ /Applications/TextMate.app/Contents/PlugIns/ 以下に放り込む方法もあるようだけど、個人的には自分でインストールしたプラグインなりバンドルが全て ~/Library/Application Support/TextMate/ 以下にあるのはわかりやすいかなと思った。なんかおかしくなったらここのディレクトリ消せばいいんだし。）</span>
<h3>日本語をわりとまともに表示する</h3>
で、このままだと文字が重なって見にくいのでTextMate専用のフォントをインストールする。先ほどのサイトの下部にForMateKonaVe.ttfという項目があるので、そこからForMateKonaVe2006-11-02.zipをダウンロード！解凍して ForMateKonaVe.ttfをダブルクリックしてフォントをインストール！
TextMateを起動させて TextMate &gt; Preference &gt; Fonts &amp; Color の設定画面の下部にあるFont:にForMateKonaVe-Regularを選択して完了。これでOK！

<img src="http://lh5.ggpht.com/_1drnogi3vdg/SoleMuNl00I/AAAAAAAAAiQ/IQMvomehCzY/ss.png" alt="" />

なんとかいけるもんですねｗ
<h3>参考サイト</h3>
<ul>
	<li><span style="font-size: 85%;"><a href="http://d.hatena.ne.jp/hetima/20061110/1163085746">TextMate の日本語入力 - d.hetima</a></span></li>
	<li><a href="http://d.hatena.ne.jp/hetima/20061102/1162435711"><span style="font-size: 85%;">TextMate で日本語をわりとまともに表示する - d.hetima</span>
</a></li>
</ul>
