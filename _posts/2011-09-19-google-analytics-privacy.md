---
layout: post
title: Titanium Google Analytics
categories:
- analytics
- Titanium Mobile
tags:
- TDm03
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '3332'
---
9/17（土）に、はてな株式会社さんで開かれた<a href="http://tidevs.me/">Ti.Developers.meeting Vol 0.3 in Kyoto</a>に行ってきました。すっごい楽しかったです（そう主催者が言えって言ってました）。いや嘘です、いや本気で。

で、ちょっとセッションで気になったコト調べてみた。
<div id="__ss_9291306" style="width: 425px;">

<strong style="display: block; margin: 12px 0 4px;"><a title="Ti.Developer.Meeting #03 Hatena::Counting" href="http://www.slideshare.net/chris4403/tidevelopermeeting-03-hatenacounting" target="_blank">Ti.Developer.Meeting #03 Hatena::Counting</a></strong> <iframe frameborder="0" height="355" marginheight="0" marginwidth="0" scrolling="no" src="http://www.slideshare.net/slideshow/embed_code/9291306" width="425"></iframe>
<div style="padding: 5px 0 12px;">View more <a href="http://www.slideshare.net/" target="_blank">presentations</a> from <a href="http://www.slideshare.net/chris4403" target="_blank">Yoshiomi Kurisu</a></div>
</div>
<a href="https://twitter.com/chris4403/">@chris4403</a>さんの「<a href=" http://d.hatena.ne.jp/chris4403+tech/20110917">はてなカウンティングアプリの裏側</a>」のセッションで出てきた、Titanium MobileとGoogle Analytics（以下、GA）について。

アプリがどのように使われているのか、GAを使って計測しているというものです。Webアプリなら普通に、GAのトラッキングコードを貼り付けるだけなのですが、iOSのネイティブアプリでGAを使いたい場合、<a href="http://code.google.com/intl/ja/mobile/analytics/docs/iphone/">Google Analytics SDK for iOS</a>を使わなければなりません。はい、Objective-Cなんて分からないですよね、分からないからTitanium使ってるんです（少なくとも僕の場合）。ということで、Titanium MobileでもWebみたいにGAを使いたいって方に、オススメするのが以下のライブラリです。
<ul>
	<li><a href=" https://github.com/rogchap/Titanium-Google-Analytics">rogchap/Titanium-Google-Analytics - GitHub</a></li>
</ul>
詳しい使い方については、<a href="https://twitter.com/chris4403/">@chris4403</a>さんの<a href="http://d.hatena.ne.jp/chris4403+tech/20110128/1296189155">解説記事</a>を見れば、分かると思います。設定の部分の記述がややめんどいですが、それさえ済めばあとはTitanium.App.Analytics.trackPageviewで仮想ページビューを設定していくだけです。うん簡単。

僕のネコミミカメラアプリ<a href="http://itunes.apple.com/jp/app/nyars/id433610083?mt=8">Nyars</a>でも実装していて、どの色のネコミミが人気なのかとか計測しています。黒、白、茶トラの色がありますが、黒色が皆さん好きなようです。

ネコミミの色が分かったからどーだって話ですが、ちゃんと使えばどの機能が使われているかとか、どのビューが見られていないとか、エラーがどれだけ起こっているかとか分かりますので、アプリ改善に大いに役立てられるかと思います。

<!--more-->
<h2>プライバシー的にどーなんよ？</h2>
はい、で、これってプライバシー的にどーなんよ？って質問がされてました。これが今回のエントリの本題です。個人的にもプライバシーとか個人情報とかよくわかってなかったので、調べてみます。
<h3>個人情報の保護に関する法律</h3>
まぁ、プライバシーなんちゃらて言われるようになったのもこの法律が2005年から施行されたからでしょう。
<blockquote><strong>法律の概要</strong>

個人情報保護法および同施行令により、5000件以上の個人情報を個人情報データベース等として所持し事業に用いている事業者は個人情報取扱事業者とされ、個人情報取扱事業者が主務大臣への報告やそれに伴う改善措置に従わない等の適切な対処を行わなかった場合は、事業者に対して刑事罰が科される。

<span style="font-size: x-small;"><a href="http://ja.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E6%83%85%E5%A0%B1%E3%81%AE%E4%BF%9D%E8%AD%B7%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E6%B3%95%E5%BE%8B ">個人情報の保護に関する法律 - Wikipedia</a></span></blockquote>
ふむふむ。で、「個人情報」って何よ？
<blockquote><strong>個人情報</strong>

個人情報とは、生存する個人の情報であって、特定の個人を識別できる情報（氏名、生年月日等）を指す。これには、他の情報と容易に照合することができることによって特定の個人を識別することができる情報（学生名簿等と照合することで個人を特定できるような学籍番号等）も含まれる。

<span style="font-size: x-small;"><a href="http://ja.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E6%83%85%E5%A0%B1%E3%81%AE%E4%BF%9D%E8%AD%B7%E3%81%AB%E9%96%A2%E3%81%99%E3%82%8B%E6%B3%95%E5%BE%8B ">個人情報の保護に関する法律 - Wikipedia</a> </span></blockquote>
ふむふむ。もうちょっと具体的に。
<blockquote>個人情報には
<ul>
	<li>氏名</li>
	<li>性別</li>
	<li>生年月日</li>
	<li>住所</li>
	<li>住民票コード</li>
	<li>携帯電話の番号</li>
	<li>勤務場所</li>
	<li>職業</li>
	<li>年収</li>
	<li>家族構成</li>
	<li>写真</li>
	<li>指紋などの生体情報</li>
	<li>コンピュータのIPアドレス・リモートホスト</li>
</ul>
などの情報でかつ個人を特定できる場合に該当する。逆にいずれかに該当しても、個人を特定することができなければ、個人情報には該当しない。例えば、年収と職業の2情報から、個人を特定することはできない。なお、生体情報については、技術の高度化に伴ってその個人特定性が徐々に強まる傾向があり、個人情報該当性の判断が難しい場合が見られる

<span style="font-size: x-small;"><a href=" http://ja.wikipedia.org/wiki/%E5%80%8B%E4%BA%BA%E6%83%85%E5%A0%B1">個人情報 - Wikipedia</a></span></blockquote>
え、職業とかもダメなの！？って思ったけど、他の情報も合わせると個人が特定できる可能性のあるものもってことですね。あ、でも職業が総理大臣なら個人が特定できるか。まぁなににせよ、個人情報＝氏名など単純に考えてたら痛い目に合いそうです。

で、この法律が適用される「個人情報取扱事業者」って何よ？
<blockquote>個人情報取扱事業者の対象
個人情報等データベースを事業の用に供する者で、国、地方公共団体、独立行政法人等、地方独立行政法人（行政機関個人情報保護法等の適用を受ける）や、取扱う個人情報（市販の電話帳やカーナビの住所情報等は除く）が過去6か月以内のいずれの時点においても5000人を超えない事業者を除く者を指す（2条3項、施行令2条）。

したがって、事業者には営利法人のみならず非営利法人も該当するが、一般の個人については原則として対象とならない（ただし、個人事業主等でこの定義に当てはまる者は当然、本法の対象となる）。</blockquote>
ふむふむ。あ、 法人・個人関係無く5,000人のデータでこの「個人情報取扱事業者」って判断されるのね。個人の趣味でやる分にはそうそう適用されることはないですね。

で、もし「個人情報取扱事業者」の場合、以下の義務を果たさなければなりません。
<blockquote><strong>個人情報保護法により発生する７つの義務</strong>
<ol>
	<li>個人情報の利用目的の特定</li>
	<li>個人情報の適正な取得、利用目的の通知</li>
	<li>正確性の確保</li>
	<li>安全管理措置</li>
	<li>第三者提供の制限</li>
	<li>開示、訂正、利用停止</li>
	<li>苦情の処理</li>
</ol>
<span style="font-size: x-small;"><a href="http://www.kj-law.com/kj-gimu.htm">個人情報保護法により発生する義務は？ ～ 個人情報保護法対策プロジェクト</a></span></blockquote>
これを守らないで勧告されて無視してると懲役と罰金が科せられます。
<blockquote>この命令に違反すると、６月以下の懲役又は３０万円以下の罰金が科されます。
<span style="font-size: x-small;"><a href="http://www.kj-law.com/kj-ihan.htm"> 個人情報保護法に違反するとどうなる？ ～ 個人情報保護法対策プロジェクト</a></span></blockquote>
怖いです。
<h2>Google Analyticsとプライバシー</h2>
で、肝心のGoogle Analyticsを使用するにあたってはどんな感じなんでしょうか。
<blockquote><strong>Google Analytics の概要</strong>

Google Analytics はウェブサイトでのユーザーの行動を分析するのに役立つウェブ解析ツールです。ウェブサイトでのユーザーの行動に関するさまざまなレポートが提供され、ウェブサイトの改善に役立てることができます。Google Analytics は情報を匿名で収集し、個々のユーザーを特定することなくウェブサイトの動向データを集計します。

<span style="color: #888888;">--(中略)--</span>

<strong>個人情報</strong>

個人情報とは、名前、メール アドレス、支払い情報など、個人を特定できる情報、またはこうした情報に合理的にリンクされているその他のデータです。すべての利用者が従わなければならない Google Analytics 利用規約では、Google Analytics を使用したこの種の情報のトラッキングまたは収集、あるいはウェブ解析情報と個人情報の関連付けを禁じています。

<span style="font-size: x-small;"><a href="http://www.google.com/intl/ja/analytics/privacyoverview.html">Google プライバシー センター</a></span></blockquote>
はい、基本的に個人を特定できるような情報はGAで収集してないし、GA利用者が個人情報と関連づけることを禁じています。やろうと思えば、<a href="http://code.google.com/intl/ja/apis/analytics/docs/tracking/gaTrackingCustomVariables.html">カスタム変数</a>というユーザーセグメント機能を使って、その値に会員情報とか設定したらできるんですがそんなことしちゃだめよってことです（そんな事怖くてできないですが...）。そもそも、今回のTitanium-Google-Analyticsのライブラリではカスタム変数の機能は実装されていません。

なので、純粋に機能改善のためであれば、ユーザーの利益につながるのであれば、GAを利用すればいいんじゃないでしょうか、と思います。
<h3>そうはいっても...</h3>
法律的に大丈夫とは言っても、やはりこれはセンシティブな問題です。Google側もそれを気にしてか、ユーザー側でGAに情報を送るか送らないか選択できるように<a href="http://tools.google.com/dlpage/gaoptout">Google Analytics オプトアウト アドオン</a>を公開していたり、サイト制作者側で部分的にしかIPアドレスをGAに送らないようにするために、<a href="http://code.google.com/intl/ja/apis/analytics/docs/gaJS/gaJSApi_gat.html#_gat._anonymizeIp">_anonymizeIp()</a>というメソッドを用意してたりします。
<ul>
	<li><a href="http://jp.techcrunch.com/archives/20091124google-analytics-illegal-germany/">ドイツではGoogle Analyticsの利用は個人情報の無断収集で有罪–政府は罰金刑を検討中 </a></li>
</ul>
ドイツの件は実際に適用されるかは不明ですが、ヨーロッパ圏ではアクセス解析にまつわるプライバシーに関して厳しい印象があります。

今回調べた個人情報保護法はもちろん日本の法律なので、海外でどのような法律があって適用されるのかはちょっと分からないです。知ってる人いたら教えてください。
