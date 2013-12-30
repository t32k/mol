---
layout: post
title: 【Titanium Advent Calendar 2011：一日目】既にリリースしたアプリ名の変更（AppStore編）
categories:
- Titanium Mobile
tags:
- appstore
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '7816'
  _aioseop_keywords: advent
  _aioseop_description: 小ネタですみませんすみませんすみません。時間なかったんですごめんなさい。今度はアニメーションについて書きたいです。
---
<img class="alignnone size-full wp-image-3734" title="rename" src="/static/blog/2011/11/rename.png" alt="" width="500" height="200" />
<blockquote><strong><a href="http://atnd.org/events/21951">Titanium Advent Calendar 2011 </a></strong>
ありがとう、2011。ありがとう、Titanium。</blockquote>
ということで始まりました、てか<a title="【Titanium Advent Calendar 2011：前座】Titanium Studioの怪 " href="http://d.hatena.ne.jp/kaz_konno/20111130/1322664751">既に始まっている（@kaz_konno） </a>Titanium Advent Calendar 2011！25日まで毎日誰かさんがTitaniumについて記事を書いていくというも催し事です。栄えある1日目としては、軽く小ネタで行こうと思います。すみませんすみません、もはやTitaniumでもないような気がしますが、けっこう手間取ったのでシェア。

<!--more-->

前回、<a href="http://tissa.t32k.me/">ticktock</a>というあタイマーアプリを作成・公開したのですが、それからほどなくしてAppleさんからメールを頂きました。内容は、私が出したアプリと同名のアプリ会社さんからの権利侵害だーって申し出がきてるよ。んで、Apple的にはちゃんとレビューしたし問題ないとは思ってるけど、当事者同士で話し合いしてね♪って感じでした、たぶん。

確認してみると、確かに同名のゲームアプリ既にAppStoreでは存在していました。しかし、ticktockって名前的にタイマーアプリなんだからこっちのほうが妥当だろうに。。とか思ったのですが、言い返す英語力もない&amp;アプリ名にこだわりもなかったので変更することにしたってのが今回の記事の主旨です。

仕方なくアプリ名変更しようと思ったけど、どうやんのこれ？新規Titanium Mobile Project作成時にはproject nameを入力できたけど、プロジェクト作成後にはそんな項目いじれるとこない。

<img class="fig" title="tiapp.xml" src="/static/blog/2011/11/tiapp.png" alt="" width="500" height="328" />

tiapp.xmlのname要素をいじってclean buildしたけども、これは効果がなかった。やっぱりプロジェクト名を変更するしかないようで、<a href="http://developer.appcelerator.com/questions/newest">Q&amp;A</a>を探ってたらありました。
<blockquote>You can create a new project and just copy in your Resources to the new project (and then just delete old).
<span style="font-size: x-small;"><a href="http://developer.appcelerator.com/question/19001/how-can-i-rename-my-iphone-app-project">How can i rename my iphone app project? » Appcelerator Developer Center </a></span></blockquote>
プロジェクト名変えたかったら新しくプロジェクト作ってコピーすればいいじゃん(・∀・)!!ってことですね。なるほど原始的。

<img class="fig" title="New Titanium Mobille Project" src="/static/blog/2011/11/new_project.png" alt="" width="500" height="455" />

ということ、新規プロジェクトで変更したい名前にして作成。

<img class="fig alignnone" title="Replace" src="/static/blog/2011/11/replace.png" alt="" width="192" height="344" />

旧プロジェクトから必要なリソースファイルを新プロジェクトにコピペ・上書きすればOKです。チョー簡単です。これで、シュミレーターや実機のホーム画面で表示されるアプリ名が変更できました。

はい、これでめでたしめでたしでは終わりません。もう一個変更しなければならないところがあります。
<h2>Change App Name</h2>
AppStoreで表示されるアプリ名を変えなければなりません。僕はこれを忘れてSubmitしたため、AppStoreではticktockと表示されているのに、落としてきてみるとtissaとアプリ名が表示されるチグハグなことが起きてしまいました。

<img class="fig" title="itunes_connect" src="/static/blog/2011/11/itunes_connect.png" alt="" width="500" height="466" />

<a href="https://itunesconnect.apple.com/">iTunes Connect </a>の App Summary ページなんですけど、今はReady for Saleの状態なの編集できませんが、新しいバージョンのアプリをSubmitして、Waiting fo Reviewになっている間はこの<strong>Detailsの横にEditボタンが現れます</strong>。そこでボタンを押して App Nameを変更すればOKです。Ready for SaleになっちゃうとEditボタンがなくなるので、てっきりAppStoreのアプリ名てのは一回提出したら編集できないものかと思ってましたが、どうやら違ったようです。よかったです。

これを理解するのに1週間、アプリ名の変更に2回バージョンアップしてバージョアップ待ちに4週間くらいかかってるので、かなりの時間を浪費しました(；´Д｀)

みなさんも、アプリ名で揉めたら試してみてください♪
<ul>
	<li><strong><a href="http://tissa.t32k.me/">tissa - Clock &amp; Stopwatch &amp; Timer for iOS </a></strong></li>
</ul>
<div>明日の<a href="http://blog.mogya.com/">もぎゃさん</a>はきっとやってくれるはず！！！</div>
