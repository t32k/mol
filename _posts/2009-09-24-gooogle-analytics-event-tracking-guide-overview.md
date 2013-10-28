---
layout: post
title: Google Analytics イベントトラッキング概要
categories:
- analytics
- translate
tags:
- google analytics
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/09/event-tracking-overview.html
  _edit_last: '1'
  pvc_views: '4250'
---
<cite>Event Tracking Overview - Google Analytics - Google Code
<span style="font-size: 85%;"><a href="http://code.google.com/intl/en/apis/analytics/docs/tracking/eventTrackerOverview.html">http://code.google.com/intl/en/apis/analytics/docs/tracking/eventTrackerOverview.html</a></span></cite>

イベントトラッキングは <em>ga.js</em> トラッキングコードで利用できるメソッドで、Webサイトのオブジェクト（例えば、Flashで作られたメニューなど）に対するインタラクションを記録することができます。これはあなたがトッラッキングしたいUIの要素にメソッドを実装することで可能になります。この方法を実装すれば、すべてのユーザーのその要素に対するインタラクションが計測され、Google Analytics の『イベントのトラッキング』のレポート画面で確認することができます。さらに、このイベントラッキングで計測されたインタラクションはページビューにはカウントされません。そして、イベントトラッキングはオブジェクト指向モデルを採用していて、異なるタイプのインタラクションを収集・分類することができます。
反対に<em> urchin.js</em> トラッキングコードを使用した場合、仮想URLが必要になり、オブジェクトの階層も表現できません。古い<em> urchin.js</em> ですと、オブジェクトに対するユーザーのインタラクションはサイトの総ページビュー数の一部として計測、表示されるので、実際のPVと仮想のPVの区別がつきません。

<em>ga.js</em> ですと、以下のようなオブジェクトにイベントトラッキングを難なく適用できます。
<ul>
	<li>FlashサイトやFlashビデオプレーヤーなどのFlashで作られた要素</li>
	<li>AJAXが埋め込まれたページ部分</li>
	<li>ガジェット</li>
	<li>ファイルのダウンロード</li>
	<li>データのロード時間</li>
</ul>
このドキュメントは Google Analytics Tracking Code（GATC）の設定に詳しい方を想定しています。また、<em>ga.js</em> をインクルードしたページにここに記述されているようなイベントトラッキングのコードを実装していることが前提です。GATC についての詳しい情報は <a href="http://code.google.com/apis/analytics/docs/tracking/gaTrackingOverview.html">Tracking Sites</a> を見たり、このサイトの Analytics Concepts セクションの部分を参照してください。
<h3>デザイン原則</h3>
イベントトラッキングのデザインモデルは柔軟性が高く、設計次第で基本的なユーザートリガーイベントモデルを超えるものも計測可能です。この理由のため、優れたイベントトラッキングレポート作成にはレポート閲覧者の協力やレポート計画が必須です。
<ul>
	<li><strong>事前にトラッキングしたいすべての要素を決定してください</strong>
初期段階で１つのオブジェクトしかトラッキングしないとしても、トラッキングしたいすべてのオブジェクト・イベントの種類を想定することで、スケーラビリティの高いレポート構造を作成することができます。</li>
	<li><strong>レポート閲覧者と一緒にイベントトラッキングレポートを計画してください</strong>
事前にどのようにレポートを見るべきか知っていれば、イベントトラッキングの実装を指示できるでしょう。例えば、もしビデオUIインタラクションのレポートしか必要ないのであれば、カテゴリーの構造はFlashメニューや、ページに埋め込まれたガジェット、ロード時間などをトラッキングする場合とはかなり異なります。さらに、レポート閲覧者に対してあなたが実装したイベントトッラキングとはまた別のトラッキングの可能性を教えることができます。例えば、レポート閲覧者はFlashビデオインターフェィスにおけるユーザー行動に興味を持つかもしれませんし、ビデオをロードする待ち時間にも興味をもつかもしれません。その場合、前もってイベントの呼び出し時に意味のある名前をつけることが可能になります。</li>
	<li><strong>明確で一貫性がある命名規則を心がけてください</strong>
イベントトラッキングを実装する上で、あなたが決めるカテゴリ名、アクション名、ラベル名の全ての名前はレポート上に表示されます。さらに、カテゴリーとアクションは１つの要素として扱われるため、似たようなカテゴリに属するすべてのオブジェクトがどのように計算されるのか最初に考えておかなければなりません。</li>
</ul>
