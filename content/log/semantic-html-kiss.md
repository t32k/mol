---
date: 2009-07-08
title: セマンティックなマーク付けとメタデータ活用
categories: report
---
<img src="http://lh4.ggpht.com/_1drnogi3vdg/SlRSKxZU8tI/AAAAAAAAAbk/VQAdFIVgw_g/header.jpg" alt="" />

セミナーが始まる前、黙って座っているとなんだか怖い数学の先生みたいだったけど、しゃべり始めると、とても優しそうな人で安心しましたｗ
<h3>ユニバーサルWebからセマンティックWebへ</h3>
<img style="margin: 0pt 12px 12px 0pt; float: left;" src="http://lh4.ggpht.com/_1drnogi3vdg/SlRSKi3JcxI/AAAAAAAAAbg/51SIg6gRUmM/fig.jpg" alt="" width="200" height="322" />この本は2002年の段階から計画していた。初めは<a href="http://www.amazon.co.jp/gp/product/4839904545?ie=UTF8&amp;tag=warikiru-22&amp;linkCode=as2&amp;camp=247&amp;creative=7399&amp;creativeASIN=4839904545">ユニバーサルHTML/XHTML</a>の続編を書いて欲しいといった出版社からの依頼だったが、多くの方が(X)HTMLについて書かれているので、あまり必要ないと思った。それよりもセマンティックWebについて書きたい。

「セマンティックWeb」、へんちくりんで難しいと思われているものだけど、切り口を変えてみれば案外伝わるのかも（<a href="http://www.kanzaki.com/works/2006/pub/0720cssnite.html">CSS Niteなどでの講演</a>体験から）RDFaが勧告になったときチャンスだと思った。

今回の講演のタイトルがKISS：Keep It Simple, Stupidてことで、できる限り、簡単に話します！

普通の人がWeb Publishingできることが良い！Web初期はカッコいいWebにするために見た目だけのWebだった（ややこしい）

Webはもっとユニバーサルでなくてはならない、てことは前回の本で述べた。誰にでも使いやすい（人間にも使いやすい）そのおかげで情報爆発（機械の力が必要になってくる）シンプルさを維持しつつ、セマンティックにする必要がある（今回の本）人間と機械のシンプルの間を探す必要がある。
<h3>セマンティックHTML? KISS!</h3>
<strong>Slide : <a href="http://www.kanzaki.com/works/2009/pub/0704pcs.html">http://www.kanzaki.com/works/2009/pub/0704pcs.html</a></strong>

<strong>Keep It Simple, Stupid</strong>
人間が読むためのウェブ文書にはさまざまな情報が詰まっている
コンピュータ処理用のデータは別途用意する？（更新が手間）
両方まとめて、シンプルにしよう！（ワンソース・マルチユース）
だからセマンティックHTML

<strong>ウェブリソースの型と関係</strong>
文脈によらない識別（名前付け）：何が同じで何が異なるかを明確にする
(例えば、「コロンビア」と聞いてそれは地名なのかコーヒ豆のことなのか機械には分らない)
データはどんなタイプ（型）か：文書について？　あるいは文中の映画について？
（カテゴリー[普通名詞]）
データどうしの関係：この日付は映画の封切り日？　映画を観た日？

<strong>提供の仕方</strong>
共通の名前付け（共有する範囲のスコープで）
関係と型を表現するためのモデル
モデルを記述して交換可能にするための構文

<strong>意味共有のKISS：URIとRDF</strong>
URI＝グローバルな共有のための名前
（Webの「山田」さんを表現するため）
RDF＝さまざまなモデルを単純な三つ組みに分解して表現するための共通枠組み
（RDF（レゴブロックのようなもの）はモデルであって、RSSやFOAFなどボキャブラリとは違う）

<strong>RDF made easy</strong>
多くのメタデータは、暗黙の主語について「プロパティ―値ペア」
（プログラミングとかやってる人は馴染みがある）
RDFトリプルはCSSのスタイル宣言と同じ
CSSを書くときはいつでもセレクタで「主語」を明示

<img src="http://lh5.ggpht.com/_1drnogi3vdg/SlRXKDwYXJI/AAAAAAAAAbs/L26P1SXKbsU/three.png" alt="" />

<strong>RDFをシンプルに表現するためには</strong>
トリプルをシンプルに表現する方法
<ul>
	<li>既存のrel、rev、href、content、srcを（拡張して）利用</li>
	<li>新しい属性property、resource、about、typeof、datatypeを導入</li>
</ul>
<strong>名前（URI）をシンプルに表現する方法</strong>
<ul>
	<li>CURIEはURI文字列を2分割し前半を接頭辞（prefix）にマップする（後半は参照と呼ぶ）
（長いままだと不便なので）</li>
	<li>XHTMLではxmlns属性を借用して接頭辞を宣言する
HTMLでもxmlns属性を借用できる（代替方法も検討中）</li>
</ul>
セマンティックHTMLといえば…

<img src="http://lh5.ggpht.com/_1drnogi3vdg/SlRXJ_VhJDI/AAAAAAAAAbo/sOh6I5u3FMI/tabnle.png" alt="" />
※ μFはMicroformats

RDFaでの記述
<ul>
	<li> link、meta要素のメタデータ記述をそのまま利用。ただしname属性は他の要素型では異なる意味を持つので、property属性を導入</li>
	<li>プロパティはCURIEを用いて記述する。このとき、XHTML定義済みのrel属性値は接頭辞無し（従来と同じ）で使える
（下記、copyrightは定義済みなのでCURIEはいらない）</li>
</ul>
<pre>&lt;link rel="copyright" href="rights.html" /&gt;&lt;meta name="author" property="ex:creator" content="神崎正英" /&gt;</pre>
<ul>
	<li>rel属性、property属性はどんな要素にも記述可能</li>
	<li>rel属性で示したプロパティの目的語がハイパーリンク可能ならhref属性で、そうでなければresource属性
（href属性値にはCURIEはかけないので）</li>
</ul>
<strong>接頭辞宣言が面倒？</strong>
オール・イン・ワンの語彙を使って、接頭辞宣言を最小限にする
たとえばGoogle語彙はよく使いそうなプロパティを一通りそろえている

<strong>文書内に含まれるデータ</strong>
<ul>
	<li>about属性で対象のURIを示す</li>
	<li>typeof属性でデータの型を示す</li>
</ul>
<strong>文脈を利用した記述</strong>
<ul>
	<li>タグの入れ子を利用してグラフを連鎖させる</li>
	<li>入れ子による空白ノードの生成</li>
</ul>
<strong>文書のURIと実世界のモノのURI</strong>
「http://ja.wikipedia.org/wiki/東京タワー」は文書のURI、＜東京タワー＞はその文書の主トピック
「http://www.kanzaki.com/」は文書のURI、＜神崎正英＞はその文書をホームページとする人物
この区別が明確でないと、分散データを集約するとき話が食い違う

:isPrimaryTopicOf（逆関数プロパティ）
実世界のモノにURIがないときは、文書URIを使って間接的に識別できる。

RDFaを応用してみる
既存文書をセマンティック化
<ul>
	<li>W3CのホームページのニュースをRSS化する</li>
	<li>ウェブログなどの自己紹介ページ（セクション）をFOAFで記述する</li>
	<li>製品情報ページをGoogle語彙で記述する</li>
</ul>
<strong>補足1：Google語彙</strong>
検索のためのオール・イン・ワン語彙
検索対象として用いられそうな語彙を一つの名前空間にまとめる
概ねマイクロフォーマットの語彙を再利用
同じプロパティでも用例によって値がURIだったりリテラルだったりと、現時点では不安定

<strong>人、製品、レビュー</strong>
人：FOAFとhcardの混成語彙。v:Person、v:name、v:affiliation、v:role、v:addressなど。
組織：これもFOAFとhcardの中間。v:Organization、v:name、v:url、v:addressなど
製品：hproductを流用。v:Product、v:name、v:brand、v:category、v:price
レビュー：hreviewを流用。v:Review、v:itemreviewed、v:reviewer、v:rating

<strong>HTML5のマイクロデータ</strong>
HTMLとして定義するセマンティック・マーク付け
HTML5編集者草案の第5章で示されているセマンティック・マーク付け
対象コンテンツを「アイテム」としてとらえ、アイテムがプロパティの集合によって表現される
RDFaやマイクロフォーマットと同様に、属性を利用してアイテムを記述する
属性値は、通常の単語（カスタムプロパティ）のほか、URI、Java風の逆順ドメイン名などを用いる。定義済み名もある

<strong>マイクロデータの基本表現</strong>
アイテムは要素にitem属性を設定して示す。item属性に値があるときはアイテムの型を表す
アイテムの子孫要素にitemprop属性を与えてプロパティ名を示す
プロパティの値は、リンク要素や埋め込み要素ならhref／src属性のURI、それ以外は要素内容テキスト（meta、time要素のように属性値が使えることもある）
<pre>&lt;p item&gt;&lt;cite itemprop="title"&gt;セマンティックHTML/XHTML&lt;/cite&gt;は…&lt;/p&gt;</pre>
<h3>神崎先生への質問コーナー</h3>
<h4>1. マークアップの今後に関する質問</h4>
<strong>Q1-1</strong>
RSSやAtomのように高い認知度を得られそうなフォーマットはどれだと思いますか？

Yahoo!がリストアップしているものがある。
（これかなリストアップってのは? <a href="http://developer.yahoo.net/blog/archives/2008/12/monkey_finds_microformats_and_rdf.html">Monkey Finds Microformats and RDF (Yahoo! Developer Network Blog)</a>）

W3Cの方でFOAFとVCARDを整理している。

<strong>Q1-2</strong>
XHTML 2やHTML 5などが登場すると、ウェブはなにがどのように変わると思いますか？

＞XHTML2のの策定を打ち切りをうけて
XHTML1.2とか仕様が進んでいたものもクローズになって残念。
HTML5はWeb Applicationとしての側面が強い。Web PublishingとしてはHTML4にちょっと手を加えた程度。まぁ仕様と実装の足並みが揃うことは良いことではないか。

<strong>Q1-3</strong>
機械が自然言語を人間並みに理解・解析できるしくみができればすべては解決するのでしょうか?

文書内での理解ならできてくると思うが、人間は文書を理解するときその文書以外に知識バックグラウンドも使って理解しているのでそこまでいくと人工知能の分野になってくる。すべて解決というのは難しい。。
<h4>2. メタデータ活用の実務的な質問</h4>
<strong>Q2-1</strong>
今後、メタデータが付与されたリソースは特にどのようなコンテンツで増えていくとお考えですか?

人・製品（GoogleのVocabulary）、時間と場所、評価（レビュー）などに対してメタデータは有効。
時間的制約を受けるもの（短時間で情報を見つけなければならない場合）、情報が膨大なもの（レシピとか番組情報）に関してメタデータは有効活用されると思う。

<strong>Q2-2</strong>
セマンティックなHTML/XHTMLをいっそう普及させる方法として、一般の方も利用できるサービスを構築するのがよいと思っています。TV番組表のカスタマイズ、グルメマップ、晩ご飯のレシピ、お店のクーポン、書店でのおすすめ書籍の紹介などが考えられますが、神崎さんが欲しい「身近なサービス」はありますか？

無数にあるネットラジオのサービス。（登録する必要のない）演奏会情報。

<strong>Q2-3</strong>
マイクロフォーマット、RDFaなど何を実装するにしてもコストが上がってしまいます。どんなことを強調して提案していけば企業担当者にも納得してもらいやすいと思いますか？

<strong>Q2-4</strong>
企業のウェブサイト運用やデータ管理において、セマンティックなHTML/XHTMLに取り組むにあたり比較的導入が可能でわかりやすい具体的なメリット（データ管理の簡略化、利益の向上など）があれば、お聞かせください。

ワンソースマルチユースの前提
データベースとWebを管理できてれば別に導入する必要はない
プレスリリース（文書）などセマンティックにすると良いかも。
マークアップについて分からない人でも指示できるように（FOAFは○で印のつけてあるところ、VCARDは△など）簡単なルールなど社内で決めておくことが良い。

<strong>Q2-5</strong>
現在、セマンティックなHTML/XHTMLを活用している企業事例がありましたら教えてください。

イギリスの政府系が活発に動いている。DiggやSlideshareも。
Google VocabularyなんかはDBを構築していない中小企業の商品情報を検索エンジンがデータベース化してくれるかも。

<strong>Q2-6</strong>
実装を行う際にマイクロフォーマット、RDFa、ダブリンコアなどいくつかの方法が用意されていますが、「こんな場合はコレで」といった、基準になるようなものはありますか？

今すぐ導入したい！→マイクロフォーマットが手っ取り早い
ただマイクロフォーマットには分散しているリソースを統合して利用できないのでRDFaを利用すると良いだろう。でもRDFaはマイクロフォーマットにくらべて面倒なので、要はバランス。

<strong>Q2-7</strong>
(X)HTMLにおいてメタデータを付与するにはRDF、microdata、マイクロフォーマットなどさまざまな実現方法がありますが、これは最終的には淘汰されるのでしょうか。もしされるとしたらなにが残ると予測されますか?

HTML5の勢いが凄いものがあるので実装されたらマイクロデータの影響力は大きそう。
マイクロデータはマイクロフォーマットとRDFaの中間っといったイメージ。
RDFaはもうちょっと整理された方がよい。
マイクロデータでマイクロフォーマットは利用できるかもしない(class属性をitemprop属性に変更すればよいので)
まぁ、混沌としてます。。。

<strong>Q2-8</strong>
今後、さらに洗練されたメタデータの実装方法が出現する可能性はありますか?その場合、どのようなものになると予測されますか?

RDFモデルである主語・述語・目的語の３つだけでなくn個のことを表現したいという人もいるけど、たぶん変わらないだろう。
<h4>3. トレンドに関する質問</h4>
<strong>Q3-1</strong>
「日本のWebは残念だ」という話が少し盛り上がっていますが、神崎さんの目にはどのように映っていますか？

話題が出ているというメタデータは知っているが、実体は知らないｗ
Webに外国も日本も区別ないので残念ではない。
<h4>4. 書籍に直接関係する質問</h4>
<strong>Q4-1</strong>
pp.238-239、例10.9とその説明について、説明を読んでも頭の中がこんがらがってしまい、どうも理解できずに困ってしまうことが多いです。いざ実装となるともっと頭がこんがらがってしまいそうです。複雑な関係を考える際のコツなどはありますか？

セマンティック化することは文書構造とデータ構造が多重化することなので、文書とデータでツリーが逆になる状態はできる限り避けた方がよい。ただ、こんなんできるよってことを紹介しておいた。

<strong>Q4-2</strong>
p.234、例 10.6の＜span property="rvw:minRaiting" content="1"＞＜/span＞ の部分ですが、span要素の中が空になっています。空の要素は意味を持たないものだと思います。いままで属性で意味を与えるということがそれほどなかったので、RDFaのために空要素を記述することに抵抗があります。レビュー以外でも出てくることがあると思います。空要素以外での対応方法などありましたら教えていただければ幸いです。
人間とコンピュータが必ずしも同じ情報を必要としているとは限らない。コンピュータにはメタデータが必要。
見えるデータとして表示しておくのもひとつ。誤解が生じるようであれば空にしておく。
ちなみにHTML5だとBODY要素にMETA要素が書けるかもしれない。

<strong>Q4-3</strong>
紀元前の情報からRFCやTEIなど、メインの内容以外にも数多くの情報を網羅していないと書けない内容だと思いました。膨大な情報をどのように整理されているのでしょうか？日々のインプットからアウトプットまでの流れや情報整理のコツなどがありましたら教えてください。
適当にやってますｗ　全部テキストにするのがつぶしがきく。
アウトライプロセッサを使用した。
<h4>5. The Web KANZAKIや神崎さんに関する質問</h4>
<strong>Q5-1</strong>
普段はどのようなお仕事をされているのでしょうか？

フリーター！？　ウェブに関係することやっています。

<strong>Q5-2</strong>
The Web KANZAKIにはかなりのページ数があると思うのですが、すべて静的に管理しているのでしょうか？また、現時点でおおよそ何ページくらいで構成されているのでしょうか?

16000リソースにアクセスがあった。そのうち7,8割は動的に生成なので静的は2000~3000くらいかな。よくわからないです。
<strong>Q5-3</strong>
神崎さんはTwitterを使われていますか？また、TwitterでセマンティックなHTML/XHTMLを活用する方法としてどのようなことができますでしょうか。アイデアがありましたら、教えてください。
Twitter : <a href="http://twitter.com/_masaka">@_masaka</a> FriendFeed : <a href="http://friendfeed.com/mkanzaki">http://friendfeed.com/mkanzaki</a>
アカウント名にmasakaが使えないとやる気がなくなる。でもフォローされるようになって今は英語でつぶやいている。Twitterはハッシュタグを使ったサービスがあると面白いかも。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/483993195X/warikiru-22/ref=nosim/" target="_blank"><img class="fig" style="border: 0pt none;" src="http://ecx.images-amazon.com/images/I/51oaN2iq9xL._SL160_.jpg" border="0" alt="セマンティック HTML/XHTML" width="124" height="160" /></a></td>
<td valign="top"><a href="http://www.amazon.co.jp/%E3%82%BB%E3%83%9E%E3%83%B3%E3%83%86%E3%82%A3%E3%83%83%E3%82%AF-HTML-XHTML-%E7%A5%9E%E5%B4%8E-%E6%AD%A3%E8%8B%B1/dp/483993195X%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D483993195X" target="_blank">セマンティック HTML/XHTML</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" border="0" alt="" width="1" height="1" />
神崎 正英&nbsp;

毎日コミュニケーションズ  2009-05-28
売り上げランキング : 15357
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-5-0.gif" alt="" />

<a href="http://www.amazon.co.jp/%E3%82%BB%E3%83%9E%E3%83%B3%E3%83%86%E3%82%A3%E3%83%83%E3%82%AF-HTML-XHTML-%E7%A5%9E%E5%B4%8E-%E6%AD%A3%E8%8B%B1/dp/483993195X%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D483993195X" target="_blank">Amazonで詳しく見る</a>

by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></td>
</tr>
</tbody>
</table>
<h3>参加してみて</h3>
本を読む限り、かなり小難しくて全然理解できてませんでした。たぶんセミナーも高度な内容で俺置いてけぼりになるんだろうなと思ってました。（全部読んでなかったし）でも、やはりそういう人のことは神崎さんも気にしていて、セミナーはゆっくり・丁寧、繰り返しで、できる限り分かりやすく説明していました。そのおかげでRDFaのことが何となく掴めたというか、もちろん全部わかるようになったわけではないけど、少なくともこの本をもう一度理解するキッカケになったと思います。なので、セマンティックHTML読んで理解できなかった人は、まず今回のセミナーのスライドを理解してから読めばいいとい思うよ。

まぁ、RDFa, Microformats, microdata, GRDDLに加え、各ボキャブラリーと勉強しなければならないことはまだまだ多いなと。。。

参考サイト
<ul>
	<li><a href="http://www.yomotsu.net/wp/?p=538">セマンティックなマーク付けとメタデータ活用 | ヨモツネット</a></li>
	<li><a href="http://www.yasuhisa.com/could/diary/cybergarden-semanticweb/">「セマンティックなマーク付けとメタデータの活用」に参加してきました : could</a></li>
</ul>