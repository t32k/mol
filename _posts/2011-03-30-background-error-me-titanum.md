---
layout: post
title: バックグラウンド動作と実機転送エラーと私とタイタン!!!!!
categories:
- Titanium Mobile
tags:
- Titanium
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '6063'
  _aioseop_description: "みなさんタイタンしてますか？わたし？わたしタイタン(・∀・)ｲｲ!!\r\n\r\n今日は小ネタ的な感じで徒然なるままにかきつらねてみるとかしてみるとか。"
---
<img class="fig" title="install" src="http://t32k.me/mol/file/2011/03/install.jpg" alt="" width="470" height="250" />

みなさんタイタンしてますか？わたし？わたしタイタン(・∀・)ｲｲ!!

今日は小ネタ的な感じで徒然なるままにかきつらねてみるとかしてみるとか。

<!--more-->
<h3>バックグラウンド動作させない</h3>
<blockquote>PROJECT_HOME/build/iphone/Info.plist を PROJECT_HOME/Info.plist にコピーして以下の設定を追加する
<pre>&lt;key&gt;UIApplicationExitsOnSuspend&lt;/key&gt;
&lt;true/&gt;</pre>
<a href="http://d.hatena.ne.jp/bongole/20100902/p1">Titaniumメモ - tail -f bongole.current.log</a></blockquote>
まぁ、そのまんまな内容でどうすればいいのか、ちょっと悩んだのでメモ。

例えば、あるタスクというか、そのアプリでゴールとするタスクが終わったときに、たいていのアプリって終了ボタンってないよな？ってことに気づきました。そりゃ、終わったら違うアプリ立ち上げるか、ホーム画面に戻るかして「終了」ってことになるんだろうけど、Titanium Mobileでアプリ作ってたらそのまま生きているというか、バックグラウンドで作動している。

こっちとしては、アプリを閉じたらスタート画面に戻って欲しいし、バックグラウンドで処理することもないので閉じててほしいと思ったわけです。

例えば、Twitterアプリで考えればツイートするってことも重要なタスクだろうけど、たいてはタイムラインを読むっていうループの作業だから、他のアプリ立ち上げても前回の画面などの状態は残っていてくれたほうがいいんだろうなーって思った。

何が言いたいかといいますと、Webサイトを作ってる身としてはこうゆうアプリケーション制作の感覚が新鮮というか今までとは違った頭の部分使ってる感じがしておもしろいなと思ったのでした。あ、もちろんWebサイトでも大まかなユーザーの回遊パターンとか考えてるよ。なんかアプリの場合はそれがもっとダイレクトな感じがするの。
<h3>実機転送エラー</h3>
<blockquote>ファイル名の大文字・小文字の区別は…
・iPhone実機では、 区別する。
・シミュレータでは、区別しない。

<a href="http://hidden.vis.ne.jp/blog/?p=459">hIDDEN bLOG » iPhoneシミュレータと実機でファイル名の扱いがちょっと変わる件</a></blockquote>
んで、もう一個のネタは、まさしくこれが問題でした。前回で晴れてiOS Developer Programに加入し実機転送できるようになったのですが、突然、転送エラーがでるようになってて小一時間悩みました。

で、よーくよく調べてみたら、PROJECT_HOME/build/i<strong>p</strong>honeのところが、i<strong>P</strong>honeになってました....そういえば、なんかしらよくわからないエラーになったらbuildしたファイル全削除でOK戦法してたときにあやまってi<strong>p</strong>honeディレクトリごと消したんだった。。んで、再度ディレクトリに作るときにi<strong>P</strong>honeって作成したまま、シュミレータ動かしてたのだった。

てか、ちゃんとTitanium Developerでエラーログだしてた（iPhoneフォルダは、iphoneフォルダだった、みたいな）。ちゃんと見なくてごめんなさい。Titanium側を疑ってましたすみません。ってことで、Titaniumを使わないiPhone制作ってゆうのも、ちょいちょいやっておかないとなーと思ったのでした。（基礎的な知識ね。）

では、みなさんれっつたいたい！
