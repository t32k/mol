---
layout: post
title: Googleアナリティクス v5 レポートで$インデックスを確認したい！（2ヶ月ぶり2度目）
categories:
- analytics
tags:
- google analytics
status: publish
type: post
published: true
meta:
  pvc_views: '4106'
  _edit_last: '1'
---
<a href="http://t32k.me/mol/log/index-value-ga-v5/">前回は私の勘違いで、誤った情報を流してしまい申し訳なく思ってます</a>。でもあきらめないで！（誰？

ということで、私の間違いを<a href="https://twitter.com/#!/susumukatachi">@susumukatachi</a>さんが、<a href="http://susumukatachi.jp/archives/1930">懇切丁寧にブログで教えてくださいました</a>ので今回はなんとか解決できそうです。

<!--more-->

（僕にとって）重要だったのは以下です。
<ol>
	<li>$インデックスと平均目標値は違う</li>
	<li>ベージの価値を知りたければ$インデックスを見る</li>
	<li>$インデックスは <strong>(合計目標値+Eコマースの収益) / ページ別訪問数</strong> で導き出せる</li>
</ol>
特に重要なのは3番目ですね。あー$インデックスというのはそうゆう計算式で出るのねと良いことを知りました。Googleアナリティクス上では上記のような計算はできないので、CSVかなんかでローカルにダウンロードしてEXCELで計算すれば$インデックスを出すことできますけどめんどくさいですよね。ってことで、計算してくれるユーザースクリプト作りました。Chromeで確認しています。多分Firefoxでも動くと思います。

極めて限定的な感じになって申し訳ないのですが、まずは以下のカスタムレポートを$インデックスを見たいプロファイルにコピーしてください。
<ul>
	<li><strong><a href="https://www.google.com/analytics/web/permalink?type=custom_report&amp;uid=fMTOTwpxTJisMbu_6h-Mdw">上位のコンテンツ（$インデックス含む）:カスタムレポート</a></strong></li>
</ul>
これだけだと、$インデックスは確認できないので、次のスクリプトをインストールしてください。view rawってとこクリックしたらインストールできると思います。

<script src="https://gist.github.com/1471956.js?file=calculate_index.user.js"></script>

そして先ほどのカスタムレポートにアクセスするとスクリプトが実行されてこんな感じになると思います。出力されないとか調子悪かったらリロードしてください。

<a href="http://t32k.me/mol/file/2011/12/Google-Analytics.png"><img src="http://t32k.me/mol/file/2011/12/Google-Analytics.png" alt="" title="Google-Analytics" width="500" class="fig aligncenter size-medium wp-image-3810" /></a>

個人的には満足です。<a href="https://twitter.com/#!/susumukatachi">@susumukatachi</a>さん、ありがとうございますでした。

というか、こんなスクリプトなくても新レポートで$インデックス確認できるようになるといいですね。
