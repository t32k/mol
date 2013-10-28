---
layout: post
title: 続・おんなじラベル何回も作るのめんどくさい
categories:
- javascript
- Titanium Mobile
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '2595'
---
前回の記事書いてからそう言えば、JSSってのがあったんだと思いだしたので書いてみる。

JSSはTitanium Mobile環境でCSSみたいな感じの役割をしてくれます。でも前回試した時残念な出来だったのであんまり↓だったので忘れてた。<!--more-->
<script src="https://gist.github.com/1180786.js"> </script>

font: {fontSize: 50}みたいにオブジェクトで書くケースの時ってJSSではどーやって書かなきゃいけないだろうと思ったり、ちゃんと書いてるのにCleanしてやらないと動作しなかったり、やっぱ不安な感じです。あと動的に値を設定したい時ってこれじゃ無理だよね？

デザイナーさんと分業するならこれ以上無い選択なんだろうけどまだはやいかな。。。あとは、
<ul>
	<li><a href="http://higelog.brassworks.jp/?p=1144">TitaniumのロジックとUIのプロパティ定義を分離する | ひげろぐ </a></li>
</ul>
ひげろぐさんみたいに、単純にプロパティ部分を分ける方法もあった。こっちが一番トーシローの僕的には分かりやすい気がする。

<script src="https://gist.github.com/1180830.js"> </script>

<blockquote>すなわちTi.includeよりrequireがいいらしいということです。
<a href="http://higelog.brassworks.jp/?p=1741"> CommonJSスタイルがいいらしい | ひげろぐ </a></blockquote>
とのことなのでrequireでやってみた。
