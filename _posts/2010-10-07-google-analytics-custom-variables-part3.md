---
layout: post
title: Google Analytics カスタム変数、パート3：スロットぜよ！
categories:
- analytics
- translate
tags:
- google analytics
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '4534'
---
<cite>原文：<a href="http://www.lunametrics.com/blog/2010/07/23/custom-variables-part-iii-slots/">Custom Variables, Part III: Slots</a>
投稿日：2010-7-23 by Jonathan</cite>

これがカスタム変数シリーズ3番目の記事だ（ようやくだね）。僕らはすでに、<a href="http://t32k.me/mol/2010/10/google-analytics-custom-variables-part1/">なぜカスタム変数を使うのか</a>、<a href="http://t32k.me/mol/2010/10/google-analytics-custom-variables-part2/">どのようにコードが動作するのか</a>見てきた。カスタム変数のスロットと呼ばれるものがどのように動作するのか説明する、これが最後のパートだ。
<h3>スロットとスコープ</h3>
<a href="http://t32k.me/mol/file/2010/10/slot.jpg"><img class="alignright size-full wp-image-1764" title="slot" src="http://t32k.me/mol/file/2010/10/slot.jpg" alt="" width="200" height="245" /></a>

<a href="http://t32k.me/mol/2010/10/google-analytics-custom-variables-part2/">パート2</a>でスロットもしくはインデックスは、_setCustomVar関数の第1引数だと覚えているだろうし、僕らもその時はもっともらしく説明していた。なぜなら、本気で説明しようとなると記事丸々使うことになっちゃうからね。

スロットをGAからの小さな郵便箱だと考えることができると思うよ。君は名前と値のペアを紙に書いて投函することができて、GA配達員がそれを引き出し、値を書き込んでいく。そこには1から5とナンバリングされている5つのスロットがある。各スロットには1枚の紙しか入れておけないんだ。

”それで... ”と、君は言うだろう。 ”ということは、僕らは5つのカスタム変数を持てるってことだよね？"

<!--more-->

うん、まぁちょっと違うんだ。なぜなら、思い出してほしい。各変数はビジター、セッション、ページレベルといった<strong>スコープ</strong>を持ってたよね。これらの動作の仕方は微妙に違うんだ！

ページレベル変数において、Google Analytics の郵便配達員はすべてのページで、ボックスの中の紙を取り出す。そしてボックスは空になり次のページで新しい紙を入れることができるんだ。

セッションレベル変数において、Google Analytics の郵便配達員はセッションの終りに、ボックスの紙を取り出す。君は新しい紙を投函することができるが、まずは古い紙を捨ててからだ。

ビジターレベル変数において、Google Analytics の郵便配達員は紙を取り出し、値を書き込む。そして紙を戻す。（__utmvクッキーが存在する限り）また、新しい紙を入れることが出来るがこれも古い紙を捨ててからだ。

どのスロットにおいても、<strong>最後に記録された値が勝つ</strong>ってこと。
<h3>OK、いい話だったよ、つべこべ言わず要旨を教えてくれ。</h3>
それで、結論はここかい？
<ul>
	<li>ページレベル変数では異なるページでスロットを再利用出来る。</li>
	<li>もしセッションレベルとページレベル、いずれの変数において再利用するならば、最後の値が勝つので、スロットを再利用する場合は本当にそれが上書きされたのか確認すべきだろう。時にこれは理にかなっている（誰かがステータスを“member=gold” から“member=platinum”に変えた時など）。たいていは、セッションレベルもしくはビジターレベルの変数が他の影響を受けないためにも、君はスロットを取っておきたいはずだ。</li>
	<li>常に同じスロットで同じキーを変数として使うべきだ。君は“member=gold”を異なる2つのスロットで使ってはいけないし、さらに悪いことに“member=gold”をスロット1で使って“member=platinum” をスロット2に使うなんて言語道断だ。</li>
	<li>最も重要な教訓は<strong>カスタム変数の管理方法はあなた次第</strong>ということ。もし、多くのカスタム変数を抱えるような複雑な状況ならば、スロットとスコープの表を作って管理するといいだろう。</li>
</ul>
<h3>スロットを知る</h3>
カスタム変数の案件を隣の部署のエンジニアに任せたいし、彼らはそれをうまく解決してくれそうだけれども、すでにスロットは重要であることは気づいただろう。スロットが重要である理由はカスタム変数を詳細セグメント(またはクロスセグメントのレポート、カスタムレポート）でも使えるからだ。以下のような感じでスロットを利用できる。

<a href="http://t32k.me/mol/file/2010/10/dimension.png"><img class="alignnone size-full wp-image-1761" title="dimension" src="http://t32k.me/mol/file/2010/10/dimension.png" alt="" width="200" height="260" /></a>
<h3>もっと知りたい</h3>
Google Code のサイトになかなかよい<a href="http://t32k.me/mol/2010/10/gatrackingcustomvariables/">カスタム変数についてのドキュメント</a>があるよ。でも、この<a href="http://www.youtube.com/watch?v=UmQTfqmoSyk">ウェビナー</a>を見るのが一番いいね。Google Analytics のプロダクトマネージャーであるPhil Mui がカスタム変数がどのように動くのか丁寧に教えてくれるよ。最後に、Phi から君に良い言葉がある。” Google Analytics がどのように動くのか知りたいと思った時ほど成長するチャンスはない”
