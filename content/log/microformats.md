---
date: 2009-02-12
title: マイクロフォーマット
subtitle: Webページをより便利にするマークアップテクニック
categories: 
    - books
excerpt: マイクロフォーマット(microformats)とは、既存の(X)HTMLを用いつつ、ウェブページの情報により豊かな意味を与え、構造化する仕組みです。ウェブページをマイクロフォーマットに対応させることで、ウェブページ上の情報を、コンピュータでも処理しやすくなります。
ogimage: http://ecx.images-amazon.com/images/I/41vZZo0080L.jpg
---

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4839925445/warikiru-22/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/41vZZo0080L._SL160_.jpg" alt="マイクロフォーマット ~Webページをより便利にする最新マークアップテクニック~ (Web Designing BOOKS)" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4839925445/warikiru-22/" name="azlinklink" target="_blank">マイクロフォーマット</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.3.4</div></div><div class="azlink-detail">John Allsopp<br />毎日コミュニケーションズ<br />売り上げランキング: 1046859<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4839925445/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

HTML5に関して言えば、意味的な要素が追加され、セマンティックな色合いが強まっているがまだまだ足りない。なぜなら「店名」をマークアップするときはどの要素を使うべきか？「名前」をマークアップするときは？「地名」は？などのようにだ。

だからといって、`shop`や`name`みたいに新しい要素がどんどん作られたらそれはそれで困るだろう。そうゆうわけで、マイクロフォーマットの出番だ。簡単に言えば、新しく要素なんて作らずにclass属性やrel属性を使って意味的な部分を補っていこうって考え。

紹介する本はリファレンス形式かなと思いきやステップアップ式のガイド本だったのが残念だった（一応、巻末に仕様リファレンスはある）。例えば、hreviewの仕様について知りたかったら、まず、hreviewの章の部分読んで、事例研究の章を読んで、仕様リファレンス部分を読まなければならず、飛び飛びですごく面倒くさい。CSSのスタイル指定とかあんまり必要ないのではと感じた。

とはいえ、Microformats Wikiを除けば、日本語でこれだけマイクロフォーマットについて書かれてるドキュメントはこれしかないし、実際に使われているマイクロフォーマットの事例など紹介して丁寧に解説されてあるので、分かりやすかった。

特にYahoo!の事例なんかは、中の人のマイクロフォーマットに対する考え紹介されていて興味深い。

> なぜマイクロフォーマットを採用したのかって？　何よりまず、Yahoo!ではどのスタッフもただウェブに夢中だからだ。ウェブがどんどん繁栄するのを見たいのさ。マイクロフォーマットはウェブを活気づけるのに役立ちそうだし、最終的にはユーザのためにもなるだろうと感じた。ウェブサイトでも組織でも、大規模になるほど制約が出てくることがあるのは確かだけど、裏を返せばその規模の大きさが有利になることもある。マイクロフォーマットのような例では、Yahoo!クラスの規模があれば、その技術が一定のハードルを超えて広まる可能性がある。僕らは光栄にもその役目を果たしたわけで、マイクロフォーマットをの力でウェブが一段とユーザの役に立つようになるのを楽しみにしているんだ。

いいですね、米Yahoo!はオープンな感じがして、とても好きです。実際にSearchMonekyではhAtom、hCalendar、hCard、hReview、XFNをインデックスしているみたいだ。

> ウェブをもっと良い世界にしてくれるものなら、何でも利用した方がいいと思う。それがマイクロフォーマットほど技術的な影響が小さいものなら、使わない手はない。もちろん、状況次第で臨機応変に判断する必要があるけれど、マイクロフォーマットに対応するのは楽勝モノだと思うよ。おまけに、自分たちの努力がウェブ全体の進化にとってプラスとなるかもしれないというボーナスまで付くことになる

事実、マイクロフォーマットは最小限の工数で対応しようと思えば、class属性いじるだけで良いからだ。それによってCSSを変更しなければならないとかないし（名前かぶったらしなきゃいけないけど）、古い環境に影響せずにそれに対応するUAにはそれ相応の価値を提供できる。素敵だ。