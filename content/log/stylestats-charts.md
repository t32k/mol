---
date: 2015-08-09
title: StyleStatsにタイムラインチャートを追加した
subtitle: Added timeline charts!
categories: 
    - development
excerpt: 待望の期間グラフをStyleStats Web版に追加した。StyleStatsはCSSを解析ツールで、一回だけ使って、へぇー私の・僕の書いたCSSはこんな感じなんだぁーと理解してもらうのも結構だが、やはり継続的に解析してもらって、どのくらい改善したのか理解して欲しいと思っている。
ogimage: http://t32k.me/mol/images/2015/0810-00.png
---

[![](/mol/images/2015/0810-00.png)](http://www.stylestats.org/dashboard?q=https://www.facebook.com)

待望の期間グラフを[StyleStats Web版](http://www.stylestats.org/)に追加した。StyleStatsはCSSを解析ツールで、一回だけ使って、へぇー私の・僕の書いたCSSはこんな感じなんだぁーと理解してもらうのも結構だが、やはり継続的に解析してもらって、どのくらい改善したのか理解して欲しいと思っている。

<script async class="speakerdeck-embed" data-slide="125" data-id="50ae30301fb9013041ed22000a9d04af" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

+ [GitHub's CSS Performance // Speaker Deck](https://speakerdeck.com/jonrohan/githubs-css-performance)

こう思うようになったのもJon Rohan氏のGitHub's CSS Performanceのスライドを見てからだ。CSSだからといって、彼らは手を抜くこともなく最高のエンジニアリングを持って問題を解決しようとしていた。さすがGitHub!おれたちにできない事を平然とやってのけるッ！そこにシビれる!あこがれるゥ!と思って、そうゆうことを僕もしたくてここまで頑張ってきた。

そんな感じで感傷に浸っているが、実装自体は[HIGHCHARTS](http://www.highcharts.com/)を使っていて、難なくできている。[D3.js](http://d3js.org/)も考えたが、あれはビジュアリゼーションツールであって、グラフツールではない。[C3.js](http://c3js.org/)を使えば、グラフ機能を簡単に使えるが、D3.js + C3.js、2つのスクリプト読み込むのダルいと思って、HIGHCHARTSにした。そのほうが軽いしね。商用利用するとお金がかかるが、まぁしないし、いいかと思った。

![](/mol/images/2015/0810-01.png)


そうゆうわけで、みなさん定期的に使ってみてください。当然、1回しかテストが実行されてないと、ただの点のグラフになるで、とりあえず2回以上テストお願いします。あとは、Web UIからじゃなくて、リモートから実行できたらいいなぁと思いつつ、おいおい頑張っていこうと思う。

## WEB+DB PRESS総集編

そういえば、WEB+DB PRESS総集編に記事を寄稿しましたので、皆さんよければ買ってください。買ってください！

>WEB+DB PRESS総集編第5弾です。Vol.1~84まで14年分のバックナンバーと、過去4回の総集編の書き下ろし記事をDVDに一挙収録します。もちろん、特別書き下ろしとして豪華執筆陣による「Web技術の過去と現在、そしてこれから」も掲載。DVD収録データを含めた本誌電子版のダウンロード用パスコードも付録しているため、DVDが読めない環境の方も安心です!

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4774175382/warikiru-22/ref=nosim/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/512VlPFhc%2BL._SL160_.jpg" alt="WEB+DB PRESS総集編[Vol.1~84]" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4774175382/warikiru-22/ref=nosim/" name="azlinklink" target="_blank">WEB+DB PRESS総集編[Vol.1~84]</a></div><div class="azlink-detail">WEB+DB PRESS編集部<br />技術評論社 (2015-08-11)<br />売り上げランキング: 2370<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4774175382/warikiru-22/ref=nosim/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>
