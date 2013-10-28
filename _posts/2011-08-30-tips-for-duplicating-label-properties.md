---
layout: post
title: おんなじラベル何回も作るのめんどくさい
categories:
- javascript
- Titanium Mobile
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '3616'
  _wp_old_slug: '%e3%81%8a%e3%82%93%e3%81%aa%e3%81%98%e3%83%a9%e3%83%99%e3%83%ab%e4%bd%95%e5%9b%9e%e3%82%82%e4%bd%9c%e3%82%8b%e3%81%ae%e3%82%81%e3%82%93%e3%81%a9%e3%81%8f%e3%81%95%e3%81%84'
---
あいかわらず、TItanium Mobileでもごもごしてる@t32kでございます。

アプリ作っていると、同じスタイルのLabelだけど、文言だけ違ってその度に、Titanium.UI.createLabelして同じプロパティ毎回書き連ねることが何回かあって、これめんどくさいなと。以下のように。
<!--more-->
<script src="https://gist.github.com/1180418.js?file=gistfile1.js"></script>

最初は根性やで！と書いていたのですが6回くらい続いて、ようやくなんか違うって思いました@t32k

そこで向かいの向かいの人に聞いたら、関数でまとめればいんじゃね？って言われました。こんな具合に。

<script src="https://gist.github.com/1180421.js?file=gistfile1.js"></script>

素敵！抱いて！！ってなるほどーって思ったのですが、
<ul>
	<li><a href="http://developer.appcelerator.com/question/18731/tips-for-duplicating-label-properties">Tips for Duplicating Label Properties » Community Q&amp;A » Appcelerator Developer Center </a></li>
</ul>
上記のQ&amp;Aにも似たような感じのことが書いてありましたが、なんか違う方法のようです。

<script src="https://gist.github.com/1180423.js?file=gistfile1.txt"></script>

なるほど、in演算子使って、あらかじめ指定したプロパティに後から書いたプロパティを追加して、そのオブジェクトを返してるんすかね。こっちのほうが汎用性高いですな。

ちなみに、Object.extendに代入してある関数はprototype.jsから拝借してるっぽい。

とまぁ、さも分かったようなこと書いてあるのですが、ぜんぶpocotanせんせに教えてもらいました。ありがとございました。
