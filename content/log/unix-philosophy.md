---
date: 2015-09-28
title: UNIXという考え方
subtitle: その設計思想と哲学
categories: 
    - books
excerpt: YAPC Asiaでやたらと耳にした『一つのことをうまくやる』という言葉の出典である、『UNIXという考え方』を読んだ。
ogimage: https://t32k.me/mol/images/2015/0928-00.jpg
---

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-na.ssl-images-amazon.com/images/I/518ME653H3L._SL160_.jpg" alt="UNIXという考え方―その設計思想と哲学" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/" name="azlinklink" target="_blank" rel="nofollow">UNIXという考え方―その設計思想と哲学</a></div><div class="azlink-detail">Mike Gancarz,芳尾 桂<br />オーム社<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

YAPC::Asiaでやたらと耳にした『一つのことをうまくやる』という言葉の出どころである『[UNIXという考え方](http://www.amazon.co.jp/exec/obidos/ASIN/4274064069/warikiru-22/)』を読んだ。

UNIXは30年以上も使われているOSで、20年くらいの歴史のWebよりも長い。ちなみに調べてたら[日本UNIXユーザ会](http://www.jus.or.jp/)は、1983年6月に設立されたということで同じ誕生月、同い年ということを知った。

何はともあれ、Webのフロントエンドとというのはドッグイヤーのごとく、変化が激しい。毎年新しいJSフレームワークが出てきて正直ついていけていない。こうゆう時こそ、なにごとも歴史から学ぶ必要がある。

YAPC::Asiaにおいても、UNIXの考え方についてはWeb・フロントエンドのセッションにおいて上記の言葉をよく聞いたので、頭の良い人たちはすでに気づいているのであろう。

UNIXの考え方について、以下の9つが挙げられている。

>
+ スモール・イズ・ビューティフル
+ 一つのプログラムには一つのことをうまくやらせる
+ できるだけ早く試作を作成する
+ 効率より移植性
+ 数値データはASCIIフラットファイルに保存する
+ ソフトウェアの挺子を有効に活用する
+ シェルスクリプトを使うことで挺子の効果と移植性を高める
+ 過度の対話的インタフェースを避ける
+ すべてのプログラムをフィルタにする

なかでも、『プログラムはフィルタ』、『プログラムはデータを作らない。人間がつくる』という言葉は興味深かったし、なるほどなぁと思った。プログラムはデータの通り道と考えれば、『一つのプログラムには一つのことをうまくやらせる』だけでいい。機能が足りないのであれば、`stdin` `stdout` `stderr`の入出力があるので[パイプ](https://ja.wikipedia.org/wiki/%E3%83%91%E3%82%A4%E3%83%97_(%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF)でつなげて、必要な機能を持つ次のプログラムに渡せることができる。

結果として、プログラムは小さく保てるし、『**部分は全体の総和より大きい**』というように、プログラムの組み合わせで柔軟性も持てる。

個人的にもNode.jsのCLIツールだが、[GAER](https://github.com/t32k/gaer)で`stdin`を受けつけるようにした時、すごく感動したし、世界が広がったように感じた。こんな感じで繋げれるようになった。

```shell
stylestats -f json -n path/to/css/file.css | gaer -t UA-xxxxxxx-x -r ReportName
```
+ [t32k/stylestats](https://github.com/t32k/stylestats) - CSS解析ツール
+ [t32k/gaer](https://github.com/t32k/gaer) - GAのレポートにデータ送るツール

30年も使われているということは必ずそこには理由がある。ページ数も少なくコンパクトにまとまっているので、そのエッセンスを取り入れるためには最適な一冊だ。まさしく、エンジニアの教養としての一冊だろう。
