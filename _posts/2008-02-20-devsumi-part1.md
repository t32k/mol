---
layout: post
title: デブサミ2008 1日目 感想
categories:
- report
tags: []
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2008/02/2008-1.html
  _edit_last: '1'
  pvc_views: '2137'
---
<img class="alignleft" src="http://2.bp.blogspot.com/_1drnogi3vdg/R7r5dGOVAlI/AAAAAAAAADw/REvj9be_CHQ/s400/080213_0952.jpg" alt="" width="115" height="144" />
2月13-14日に行われた~Developers Summit 2008に行ってきた。 テーマが『越境しよう、コードで世界を変えよう』ということで、デザイナーの自分だけど越境してきたよ。 といっても、JavaとかRubyとかさっぱりなので、結局、受講したセッションはRIAやPMばっかしになった。 そんなわけで、一応メモっておく。

2月13日（1日目）[DevelopmentStyle(RIA)] 10:00～10:50
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=563&amp;spid=543&amp;tr=07%5FDevelopmentStyle%28RIA%29">東賢 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=563&amp;tr=07%5FDevelopmentStyle%28RIA%29">【13-D-1】　RIA開発におけるデザイナー／デベロッパー協業のワークフローについて</a>

このセッションは、自分みたいなプログラミングにも興味があるデザイナにとってはぴったりのセッションだった。 RIA(Rich Internet Application)は分かりやすく言えば、
なんらかのリッチな要素があり、インターネットも利用していて、特定の目的を果たすための機能を提供するソフトウェアと説明。またJames Wardが考えるリッチを構成する要素として
<ul>
	<li>Connected(接続している)</li>
	<li>Alive(活き活きとしている)</li>
	<li>Interactive(インタラクティブである)</li>
	<li>Responsive(反応が良い)</li>
</ul>
の4つが挙げられたが、Aliveの説明がイマイチつかめなかった。 「活き活きしている」って要は「インタラクティブで反応がよい」ってことじゃないのか？ まぁ、要するにアプリケーションをリッチにすることでそれを使うユーザーの体験（エクスペリエンス）を向上させることができる。体験というのは、例えば、コーヒーを飲むなら缶コーヒーで十分なのに、なぜその3～5倍の価格がするのに人はカフェにいくのか。休息するという点もあるが、コーヒーを飲むということ以上にそのカフェで過ごす時間（体験）に重きを置いていることを、 スターバックスの事例で説明。 つまり付加価値が重要であり、なぜソフトウェアの世界もその点を考慮しなければならないか。
既に多くのソフトウェアが機能的には成熟し、機能だけでは競争優位が保てない状態 競争優位獲得のための差別化要因としてソフトウェアのエクスペリエンスを考え直す必要がある
<span style="font-weight: bold; color: #cc0000;">DISTINCT or EXTINCT (差別するか、さもなくば絶滅か)</span>
動いて当たり前、便利で当たり前、それプラスアルファが求められている時代ということですかね。 そのあとは、エクスペリエンスをデザインするにあたってセカンドファクトリーでの手法や流れを説明。
<a href="http://3.bp.blogspot.com/_1drnogi3vdg/R7r6MWOVAmI/AAAAAAAAAD4/bvAWgOKPqec/s1600-h/team_model.png">
<img id="BLOGGER_PHOTO_ID_5168718612392116834" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer;" src="http://3.bp.blogspot.com/_1drnogi3vdg/R7r6MWOVAmI/AAAAAAAAAD4/bvAWgOKPqec/s400/team_model.png" alt="" border="0" />
</a>チームモデルとしては、上図のように、プロジェクトマネージャーを頂点に、 その下にアーキテクチャデザイナー、エクスペリエンスデザイナーさらに、実装レベルで、 システムデベロッパー(SD)、インタラクションデベロッパー(ID)、グラフィックデザイナー(GD)という構成。 また、SD、ID、GDがスムーズに業務を遂行するにはMicrosoftのWPFやAdobeのAIRなどが有用であると説明。 最後にビジネス、システム、デザインの三者が互いに密にコミュニケーションがとれるかが重要であると説明。 １発目ということもあってだいぶ緊張したが、デザイナでも理解できる分野だったので安心した。 まさしく「越境しよう」というテーマにふさわしいセッションだった。   [DevelopmentStyle(.NET)]　11:10～11:55
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=564&amp;spid=544&amp;tr=15%5FDevelopmentStyle%28%2ENET%29">八巻雄哉 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=564&amp;tr=15%5FDevelopmentStyle%28%2ENET%29">【13-D-2】　デベロッパーに贈る！業務アプリのためのユーザーエクスペリエンス向上講座</a>

続いて、2コマ目もRIA関連。 こちらのセッションはデべロッパー向けのUX(User Experience)のセッションということで、 より実践的なテクニック、お作法についての話だった。 リッチというのはただグラデーションなどを用いて見た目を綺麗にすることではなく、 様々な無駄を無くした結果の機能美でと考えたほうがよい。 人とアプリケーションが情報をやり取りする方法は入力系と参照系に分けられる。 入力系（個人情報の登録フォームなど）でできることは、入力作業の省力化であり、 自動入力、入力補助（自動遷移、ショートカット、入力モード）などや、ヒューマンエラーの軽減と そのエラー通知の方法とタイミングなどを工夫すればエクスペリエンス向上につながる。 参照系は情報を分かりやすく視覚化（見える化）すればよい話だが、曖昧さも生じてしまう問題。 人によって求められる表現は千差万別で難しい。 そういうときにWPFを使うと幾分か楽になるよという話。   [DevelopmentStyle(RIA)]　13:10～14:00
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=565&amp;spid=632&amp;tr=07%5FDevelopmentStyle%28RIA%29">小川誉久 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=565&amp;spid=633&amp;tr=07%5FDevelopmentStyle%28RIA%29">小島英揮 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=565&amp;spid=634&amp;tr=07%5FDevelopmentStyle%28RIA%29">三野凡希 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=565&amp;spid=635&amp;tr=07%5FDevelopmentStyle%28RIA%29">春日井良隆 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=565&amp;tr=07%5FDevelopmentStyle%28RIA%29">【13-D-3】　リッチクライアント最前線</a>

Adobeの小島氏、Curlの三野氏、MSの春日井氏の三者を招いて、自社のリッチクライアントについてパネルディスカッションが行われた。 各社、各技術に関しての簡単な説明と強み、またリッチとは何かついて討論していた。 まぁ、時間も時間だけに、突っ込んだ話もできず終わってしました印象。 SilverlightとAIRがほぼ同時期に出たことにより、世間では2つが対抗する技術と思われているが、 実際はSilverlightはブラウザのプラグインでAIRというよりFlashに対抗する技術であり、 AIRと対抗するのはMSで言えば、.NET(WPF)であることを勘違いしないでねと言ってた。
<a href="http://3.bp.blogspot.com/_1drnogi3vdg/R7r7KWOVAnI/AAAAAAAAAEA/QZP495UI7vo/s1600-h/ria.png">
<img id="BLOGGER_PHOTO_ID_5168719677544006258" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer;" src="http://3.bp.blogspot.com/_1drnogi3vdg/R7r7KWOVAnI/AAAAAAAAAEA/QZP495UI7vo/s400/ria.png" alt="" border="0" />
</a>参考サイト
<span class="Apple-style-span" style="color: #551a8b;">RIA／リッチクライアントの明日はどっちだ？</span>  [DevelopmentStyle(XML)]　14:20～15:05
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=559&amp;spid=653&amp;tr=11%5FDevelopmentStyle%28XML%29">加藤哲義 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=559&amp;tr=11%5FDevelopmentStyle%28XML%29">【13-C-4】　ＸＭＬデータベースというカンブリア爆発とその行方</a>

このセッションは寝ちゃった。 XMLに関してはなんとなく分かるが、DBに関してはまったくの無知なので、あまり興味がもてず。。。 とりあえず、XMLDBは柔軟なDBだよ！ってことは分かった。 以上。 追記: builderで
<a href="http://builder.japan.zdnet.com/sp/hello-xmldb/">XMLDBの連載</a>が始まったようなので、反省がてらチェックしとこ。
[DevelopmentStyle(Web)]　15:25～16:15
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=567&amp;spid=545&amp;tr=10%5FDevelopmentStyle%28Web%29">庄司嘉織 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=567&amp;tr=10%5FDevelopmentStyle%28Web%29">【13-D-5】　次世代ウェブフレームワークの幕開け～ステートフルはじめました/君が僕を望むなら僕は君を忘れない～</a>

開始20分くらいは一体何に関してしゃべってるのかわからなかった。 ステートフルということは状態を持っている、てことはわかったけど、だからなんだという話だ！ フレームワークに関しても1度たりとも聞いたことのない名前ばかり、かなり冷や汗がでた。 後半、ようやくサーバサイドのJavaの話かと理解する。 当たり前だけど、まだまだ知らないことが多いってことを痛感するとともに、 RIA関連だからといってたかをくくってた自分が情けないと思う。 とはいえ、講師の
<a id="hvh2" title="Yoshiori" href="http://yoshiori.org/blog/">Yoshiori</a>さんの親身なプレゼンは好感が持てたし、熱い人だった。
<a href="http://yoshiori.org/blog/2008/02/1_3.php">デブサミ1日目！！！</a>

太田禎一 氏
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=568&amp;tr=10%5FDevelopmentStyle%28Web%29">【13-D-6】　いよいよ現実となるRIA on Desktop。　君はこの流れについてこれるか？</a>

AIRの事例を紹介。 待望のAIR1.0正式リリースは数週間以内になるとのこと。 まず英語版（ヨーロッパ言語）がリリース、そのさらに数週間後に日本語版がリリースの予定。 AIRの事例
<ul>
	<li><a id="sy4:" title="Web私書箱β" href="http://weblift.jp/">Web私書箱β</a></li>
	<li><a id="ezag" title="楽天デスクトップアプリケーション" href="http://japan.cnet.com/news/media/story/0,2000056023,20360280,00.htm">楽天デスクトップアプリケーション</a></li>
	<li><a id="gnlu" title="経営コックピットシステム" href="http://www.itmedia.co.jp/enterprise/articles/0710/30/news011_2.ht">経営コックピットシステム</a></li>
	<li><a id="o:xp" title="ASKUL DESKTOP" href="http://ascii.jp/elem/000/000/081/81885/">ASKUL DESKTOP</a></li>
</ul>
AIRはWin/Macに対応、その後Linuxにも対応予定。 今までの技術が使える（HTML,JavaScript,Ajax,Flash,Flexなど） イメージとしてはそれらのファイル全部zipにまとめてアプリケーションにするといった感じ。 開発環境としては
<ul>
	<li>Flex Builder 3</li>
	<li>Flash/Dreamweaverの機能拡張</li>
	<li>無料のAIR SDK</li>
</ul>
またAIRはバイナリ通信ができるため既存のAjaxにくらべ4倍早いということ。 Flexを使った簡単なコーディングのデモンストレーションを披露。 参考サイト
<ul>
	<li><a class="l" href="http://www.fxug.net/">Flex User Group</a></li>
	<li><a id="atmv" title="Akihiro Kamijo Blog" href="http://weblogs.macromedia.com/akamijo/">Akihiro Kamijo Blog</a></li>
</ul>
[DevelopmentStyle(Web)] 17:40～18:30
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail_speaker&amp;eid=105&amp;sid=569&amp;spid=546&amp;tr=10%5FDevelopmentStyle%28Web%29">天野仁史 氏</a>
<a href="http://www.seshop.com/event/dev/2008/timetable/Default.asp?mode=detail&amp;eid=105&amp;sid=569&amp;tr=10%5FDevelopmentStyle%28Web%29">【13-D-7】　JavaScript Tips &amp; Technique</a>

amachangさんに関してはいろいろと <a href="http://d.hatena.ne.jp/HolyGrail/20080214/1202995743">他のブログ</a>でも書いてあると思うので省略。 個人的にはあともうちょっとで、素人なりに、 『あ～、JSってそういうこと～！』って分かりそうな分からないようなもどかしい状態にはなった。 まだまだ勉強しなきゃね、JavaScript。

1日目まとめ

メモの内容を見てもらえば分かるように、後半に行くほどだらけてしまった。 とはいえ、１セッションあたり50分というのは、僕にとってはテンポがよかった（途中寝てしまったけど） また、１日でパネルディスカッションも合わせれば10人のプレゼンスタイルが見れたわけで、大変参考になった。 やはり、皆それぞれスタイルがある。 関連エントリー
