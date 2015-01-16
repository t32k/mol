---
date: 2008-01-20
title: 今から始める ActionScript 3.0 - WORLD WIDE TOUR
categories: report
---
Adobe Presents コリン・ムックの「<a id="xbah" title="今から始める ActionScript 3.0 - WORLD WIDE TOUR" href="http://www.event-web.net/as3/">今から始める ActionScript 3.0 - WORLD WIDE TOUR</a> 」コリン・ムックの『コ』の字も知らない自分が、AS1,2さえも書いたことがない自分が行ってきたよ。そんな自分が今回のセミナーでクラスやオブジェクトについて理解できるわけもなく、さっぱりな印象。

とはいえ、夜行バスではるばる石川からの参戦だったので一応メモっておく。
<h2>序章</h2>
コリン・ムックは知らなかったが、WenDesigningかなにかの雑誌で日本のすごいFlasherが尊敬している人物に彼の名前を挙げていたので、記憶に残ってた。そんな折、<a id="td6e" title="セミナー情報共有カレンダー" href="http://blog.woopsdez.jp/2007/11/post_264.php">セミナー情報共有カレンダー</a>で今回のセミナーがあるのを知る。すでに定員オーバーの受付終了だったがブログレポーター枠なら残ってたので早速申し込む（07/12/12）。
さすがにノー勉ではあれなので予習をしておく。
<ul>
	<li><a id="weut" title="はじめてのActionScript3.0プログラミング" href="http://zapanet.info/blog/item/882">はじめてのActionScript3.0プログラミング</a></li>
	<li><a id="h8n1" title="3月22日の技術勉強会 - ActionScript3 / Flex / Apollo 勉強会" href="http://hatena.g.hatena.ne.jp/hatenatech/20070324/1174713674">3月22日の技術勉強会 - ActionScript3 / Flex / Apollo 勉強会</a></li>
	<li><a id="r1uv" title="8月17日の技術勉強会 - Flexレイアウト手書き勉強会" href="http://hatena.g.hatena.ne.jp/hatenatech/20070821/1187670828">8月17日の技術勉強会 - Flexレイアウト手書き勉強会</a></li>
	<li><a id="e5_b" title="ActionScript for JavaScript(er)." href="http://amachang.art-code.org/usrb.in/amachang/static/shibuyaes/">ActionScript for JavaScript(er).</a> [<a href="http://mp.i-revo.jp/user.php/hpjckqhw/attach/24">動画</a>]</li>
	<li><a id="fhbd" title="AS 3.0 勉強会資料" href="http://amachang.art-code.org/usrb.in/amachang/static/as3study20070408/">AS 3.0 勉強会資料</a></li>
	<li><a id="ppn6" title="WCAN mini vol.1 - ActionScript 3.0 + CUI" href="http://amachang.art-code.org/usrb.in/amachang/static/wcan200701/">WCAN mini vol.1 - ActionScript 3.0 + CUI</a></li>
	<li><a id="dx7s" title="ActionScript 勉強会資料 in Nagoya" href="http://amachang.art-code.org/usrb.in/amachang/static/unknown/">ActionScript 勉強会資料 in Nagoya</a></li>
</ul>
流し読み程度ですけどね。
<h2>いざ会場へ</h2>
行きの夜行バスで一睡もできず、眠たさマックスでセミナー会場である<a id="eiy8" title="ゲートシティホール" href="http://www.gatecity.jp/floor/in.html?floor=3">ゲートシティホール</a> に到着。会場の印象、で、でかい！しかも、後から申し込んだにも関わらず、ブログレポーターということで、一番前で机まで用意されてあるのはラッキーだった♪
<h2><a href="http://1.bp.blogspot.com/_1drnogi3vdg/R5NeGyF04-I/AAAAAAAAACw/bpSg18aqCQI/s1600-h/080115_0940.jpg" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img id="BLOGGER_PHOTO_ID_5157569468887786466" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; font-size: 24px;" src="http://1.bp.blogspot.com/_1drnogi3vdg/R5NeGyF04-I/AAAAAAAAACw/bpSg18aqCQI/s320/080115_0940.jpg" border="0" alt="" /></a>
コリン・ムック登場</h2>
まず、このセミナーを開いてくれた関係者の皆さんに感謝の意を表す。
年末にも東京でFlashのカンファレンスを予定しているらしい。

当日のセミナーでの講演内容はここです。
↓
<a onclick="return top.js.OpenExtLink(window,event,this)" href="http://moock.org/lectures/groundUpAS3/" target="_blank">http://moock.org/lectures/groundUpAS3/</a>

セミナーの流れとしては、たまごっちのようなプログラム
（時間が経つにつれ体力が減るペットに、エサを与えるようなプログラム）を
9時間かけて懇切丁寧に説明してくれた。

//overview
プログラムをしたことない人でも気負う必要はない。
全部分からなくてもいい、やりたいことからやればいい。
プログラムに終わりはない、1日や1年、10年続けたってダメ、大事なのは毎日続けること。
今回のセミナーはクラスを作ったことがない人が対象だよ。

//ActionScript programming tools
ノートパッド
Flash
flex builder
(今回のセミナーでコリンは、Mac付属のテキストエディタとFlex3を使ってコードを書いてた。)

//Flash client runtime environments
Flash Player
Adobe AIR
Flash Lite

//what is an ActionScript program?
コードと.flaファイルを合わせたもの。
今回はコードだけのオブジェクト指向プログラミングについて説明する。
AS3ファイルのなかでAS1やAS2のコードも書けるのでそこんとこ勘違いしないでねと。

//building an airplane
飛行機を作ることを想像してほしい。
最初に必要なのは青写真だ。
パーツ（車輪や翼）としてつかえる汎用的な青写真

//objects
objectとはプログラムの中の「モノ」

//classes
クラスとは青写真と考えればよい
クラスとはオブジェクトの振る舞いや特徴を描写する

//create an object-oriented program
OOPとよく言われる
カスタムクラスをつくる
オブジェクトに何をすべきか伝える
（オブジェクトがプログラムの中でどのように振る舞うか決定する）

//main class
すべてのプログラムはメインクラスをもっている

//the virtual zoo
たまごっちのようなプログラムをつくりながら説明する。
細かな設定とかじゃなくロジックを主に説明する。

//packages
クラスを作るにあたりビルトインクラスとコンフリクトする可能性があるので、
packageで包む必要がある。

//classes in packages
パッケージの中のクラスはパッケージの名前とドットでつなげる。
例えば、gameと言うパッケージのなかのクラスPlayerなら
game.Playerのように

//creating a package
"define" とは定義するという意味でここではパッケージを"作る"と考えてよい

//package definition directive
definition directive　定義指令

//the zoo package
"zoo"パッケージを作る

ここらへんでなんか眠たさが極限、
あと30分でお昼休憩だからそこまでがまんしよう。あと20分。。あと10分。。。
次の瞬間、目を開いたら目の前にコリン・ムック先生が！
「このひとはたぶん疲れてるんでしょうね、そんな人にはこの無料チケットを」
みたいなことを言って、オライリーの本が1冊無料でゲットできるチケットをもらう。。。

<a href="http://3.bp.blogspot.com/_1drnogi3vdg/R5NepSF05AI/AAAAAAAAADA/hahwhraO5Og/s1600-h/080120_2334.jpg" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img id="BLOGGER_PHOTO_ID_5157570061593273346" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; font-size: 24px;" src="http://3.bp.blogspot.com/_1drnogi3vdg/R5NepSF05AI/AAAAAAAAADA/hahwhraO5Og/s320/080120_2334.jpg" border="0" alt="" /></a>
さすがに、通訳越しに言われるのはとても恥ずかしかったッス。
とはいえ、はるばる日本まで来て9時間みっちり教えてるのに、
来てみたら真ん前の席の奴が寝てるってどやねん！って
感じっすよねコリン先生からしちゃ。ほんますみませんでした。

んなかんじでお昼休憩。
休憩中はコリン先生のMacからレディオヘッドが流れてました。
<h2><a href="http://2.bp.blogspot.com/_1drnogi3vdg/R5NebCF04_I/AAAAAAAAAC4/_SsnJxCqQz8/s1600-h/080115_1217.jpg" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img id="BLOGGER_PHOTO_ID_5157569816780137458" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; font-size: 24px;" src="http://2.bp.blogspot.com/_1drnogi3vdg/R5NebCF04_I/AAAAAAAAAC4/_SsnJxCqQz8/s320/080115_1217.jpg" border="0" alt="" /></a>
後半はなされるがまま</h2>
//the public attribute   //the internal attribute
パブリック　公開できる、参照できる
インターナル　パッケージ内のクラス（デフォルトはインターナルだがちゃんと書いたほうがよい）

//constructor method
オブジェクトを使うには初期化(initialize)する

//variables and values
ローカル変数
インスタンス変数

//variable access-control modifiers
変数の4つのレベル
パブリック、インターナル、プロテクト、プライベート
どれ指定したらよいか分からなかったら、プライベートにしとけ

//assiging one variable another's value
このへんからthisとかでてきてよーわからんくなってくる＞＜

セミナー後半はただコリン先生が書くコードを見てるだけでした。
というわけで、後は印象に残ったことを箇条書き
<ul>
	<li>変数はコンテナという考えは捨てろ！変数はオブジェクトとして参照できる名前だよ。</li>
	<li>public APIは変えるな！</li>
	<li>オブジェクト指向ってのは人間のために書かれたコードだよ。</li>
	<li>オブジェクトは生き物なんだよ！</li>
	<li>MVCとかデザインパターンは便利だよ。</li>
	<li>んで、今回9時間書けてつくったプログラムだけどFlashだったら30分でできるよ。</li>
	<li>でも、コードで書く方がクライアントの急な変更にも対応できる、つまり拡張と変更が簡単なんだ。</li>
</ul>
ここからはコリン先生ネタw
<ul>
	<li>音楽聞きながらプログラミングできないよー。</li>
	<li>女の子プログラマーがもっと増えればいいなーとおもってる。</li>
	<li>コーラが好きだ。</li>
	<li>Flexのコード編集コマンドがギガ/メガお気に入りです。</li>
	<li>MacもWinも制作環境としてはどちらも嫌い</li>
	<li>でも、Winにはボイスデクテーション?という音声文字入力アプリがあるからwin使ってる。</li>
	<li>タイプしたくない！</li>
</ul>
コリン先生のマック
MacBook Black
OS X 10.5 Leopard
text editor : <a id="xzyj" title="Smultron" href="http://smultron.sourceforge.net/">Smultron</a>
music player : <a id="d4d8" title="Cog" href="http://cogx.org/">Cog</a>
launcher : QuickSilver
あとは確認できたのは
Flash CS3 Flex3とかで、あんましメインでは使ってない感じ。

そんな感じで、なんかもっと勉強してくれば、もっとタメになったんだろうなと思いました。

帰りも夜行バスで帰りました。
朝6時に金沢駅に着いたので、そのまま家に帰るのもあれだなと思い、
近くの<a id="nx0u" title="アパホテルの温泉" href="http://www.apahotel.com/hotel/hokuriku/06_kanazawa-ekimae/facilities.html#spa">アパホテルの温泉</a> でくつろいでそのまま会社に出社しました。

だもんで、金沢に夜行バスで観光に来る人は朝方着いて何もお店開いてないから、
温泉入りながら時間つぶせばいいと思うよ。3時間1000円だよ。
金沢駅周辺にはマンガ喫茶とかないから時間が潰せないんだよ。
とローカルネタも今後書いていこうと思ったりして。

&nbsp;

最後にコリン先生居眠りしてごめんなさい。
もらった無料チケットでEssential ActionScript 3.0は買わず、JavaScript 第5版を買わせていただきます。Essentialは翻訳版が春か夏ごろ出るとおっしゃっていたので、それまでJS勉強して、もう一度ASに再挑戦したいと思います。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td colspan="2"><a href="http://www.amazon.co.jp/JavaScript-%E7%AC%AC5%E7%89%88-David-Flanagan/dp/4873113296%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113296" target="_blank">JavaScript 第5版</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" border="0" alt="" width="1" height="1" /></td>
</tr>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/JavaScript-%E7%AC%AC5%E7%89%88-David-Flanagan/dp/4873113296%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113296" target="_blank"><img class="fig" style="border: 0px initial initial;" src="http://ecx.images-amazon.com/images/I/413amOWGgvL._SL160_.jpg" border="0" alt="JavaScript 第5版" width="123" height="160" /></a></td>
<td valign="top">村上 列&nbsp;

<strong>おすすめ平均</strong> <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-5.gif" alt="" />
<img src="http://g-images.amazon.com/images/G/01/detail/stars-5-0.gif" alt="stars" />買って良かった
<img src="http://g-images.amazon.com/images/G/01/detail/stars-4-0.gif" alt="stars" />多少冗長な感じがします
<img src="http://g-images.amazon.com/images/G/01/detail/stars-5-0.gif" alt="stars" />翻訳が上手です
<img src="http://g-images.amazon.com/images/G/01/detail/stars-4-0.gif" alt="stars" />文書が多くサンプルコードが少ない本です

<a href="http://www.amazon.co.jp/JavaScript-%E7%AC%AC5%E7%89%88-David-Flanagan/dp/4873113296%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113296" target="_blank">Amazonで詳しく見る</a> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></td>
</tr>
</tbody>
</table>
<table border="0" cellpadding="5">
<tbody>
<tr>
<td colspan="2"><a href="http://www.amazon.co.jp/%E8%A9%B3%E8%AA%AC-ActionScript-3-0-Colin-Moock/dp/4873113873%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113873" target="_blank">詳説 ActionScript 3.0</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" border="0" alt="" width="1" height="1" /></td>
</tr>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/%E8%A9%B3%E8%AA%AC-ActionScript-3-0-Colin-Moock/dp/4873113873%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113873" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/514SnR1V4yL._SL160_.jpg" border="0" alt="詳説 ActionScript 3.0" width="125" height="160" /></a></td>
<td valign="top">永井 勝則&nbsp;

オライリージャパン  2008-11-22
売り上げランキング : 17072

<strong>おすすめ平均 </strong><img src="http://g-images.amazon.com/images/G/01/detail/stars-5-0.gif" alt="star" />
<img src="http://g-images.amazon.com/images/G/01/detail/stars-5-0.gif" alt="star" />ActionScript3.0言語仕様の解説書です

<a href="http://www.amazon.co.jp/%E8%A9%B3%E8%AA%AC-ActionScript-3-0-Colin-Moock/dp/4873113873%3FSubscriptionId%3D0G91FPYVW6ZGWBH4Y9G2%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873113873" target="_blank">Amazonで詳しく見る</a> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></td>
</tr>
</tbody>
</table>