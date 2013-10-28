---
layout: post
title: Google Analytics イベントトラッキングガイド
categories:
- analytics
- translate
tags:
- google analytics
status: publish
type: post
published: true
meta:
  pvc_views: '12824'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/09/event-tracking-guide.html
  _edit_last: '1'
  _topsy_long_url: http://t32k.me/mol/2009/09/google-analytics-event-tracking-guide/
  topsy_short_url: ''
---
<cite>Event Tracking Guide - Google Analytics - Google Code
<span style="font-size: 85%;"><a href="http://code.google.com/intl/en/apis/analytics/docs/tracking/eventTrackerGuide.html">http://code.google.com/.../docs/tracking/eventTrackerGuide.html</a></span></cite>
<h2>コンテンツ</h2>
<ul>
	<li>1. <a href="#s01">イベントトラッキングのセットアップ</a></li>
	<li>2. <a href="#s02">イベントトラッキングの構造 </a>
<ul>
	<li>1. <a href="#ss01">カテゴリ</a></li>
	<li>2. <a href="#ss02">アクション</a></li>
	<li>3. <a href="#ss03">ラベル</a></li>
	<li>4. <a href="#ss04">バリュー</a></li>
	<li>5. <a href="#ss05">暗黙的カウント</a></li>
</ul>
</li>
	<li>3. <a href="#s03">実装上の注意事項 </a></li>
</ul>
<h2 id="s01">イベントトラッキングのセットアップ</h2>
イベントトラッキングのセットアップは簡単な2ステップが必要です。
<ol>
	<li><em>ga.js</em> のトラッキングコードが設定されているかどうか確認してください。セットアップについての詳しい説明は<a href="http://code.google.com/intl/en/apis/analytics/docs/tracking/asyncTracking.html">Tracking Sites</a>をご覧ください。</li>
	<li>イベントトラッキングで追跡したい各ページのオブジェクトもしくは要素に対して、 <em>_trackEvent()</em> メソッドをそのオブジェクトから呼び出してください。後述のガイドラインでこのメソッドを使ったベストプラクティスを説明します。</li>
</ol>
イベントトラッキングのレポートを見るには、『コンテンツ』の『イベントトラッキング』を選択します。
このメソッドをビデオやガジェットもしくはページのオブジェクトのソースコードに挿入してください。 <em>_trackEvent()</em> メソッドの仕様は以下です。
<pre><code>_trackEvent(category, action, optional_label, optional_value)</code></pre>
<strong>カテゴリ (必須) </strong>
追跡したいオブジェクトグループの名前

<strong>アクション (必須) </strong>
この文字列は各カテゴリー内で一意の名前であり、オブジェクトに対してのユーザーの行動を分かりやすく定義したもの

<strong>ラベル（オプション）</strong>
イベントデータを細分化したい場合、使用する文字列

<strong>バリュー（オプション）</strong>
ユーザーイベントに対して数値データを付与する整数
<h2 id="s02">イベントトラッキングの構造</h2>
イベントトラッキングのデータモデルは、GAレポートで要素にマッピングされた項目を表示します。
<ul>
	<li>カテゴリ</li>
	<li>アクション</li>
	<li>ラベル</li>
	<li>バリュー</li>
	<li>暗黙的なカウント</li>
</ul>
サイト上でビデオの再生リンクのイベントをトラキングする場合、どのように使用すればよいのか簡単な例を用いて説明します。
<pre><code>&lt;a href="#" onclick="pageTracker._trackEvent('Videos', 'Play', 'Baby\'s First Birthday');"&gt;Play</code></pre>
このシナリオのイベントレポートには、カテゴリは『Videos』、アクションには『Play』、ラベルには『Baby's First Birthday』が表示されます。これらの項目については後ほど説明します。イベントトラッキングを実装する際、この解析モデルをガイドとして利用でき、簡単ににユーザーの行動をセグメント化できることを頭の隅に置いておいてください。
<h3 id="ss01">カテゴリ</h3>
イベントトラッキングにおいて、『カテゴリ』はトラッキングするオブジェクトのグループ名を表します。 <em>_trackEvent()</em> メソッドの最初のパラメータで、必須です。

『カテゴリ』はイベントトラッキングレポートの概要ページのトップカテゴリに表示されます。これはカテゴリがイベントトラッキングの階層構造の中でルート要素であることを表していて、あなたは必要に合わせてカテゴリのグループを変更できます。一般的にカテゴリを分類するためにUIエレメントに基づいた同じ名前を複数回使用することになるでしょう。

例えば、一つのビデオインターフェイスにおいて3つの異なるユーザー行動をトラッキングする場合はこうなるでしょう。
<pre><code>pageTracker._trackEvent("Videos", "Play", "Gone With the Wind");
pageTracker._trackEvent("Videos", "Pause", "Gone With the Wind");
pageTracker._trackEvent("Videos", "Stop", "Gone With the Wind");</code></pre>
また、このビデオが何回ダウンロードされたか調べたい場合は以下のようにすれば良いでしょう。
<pre><code>pageTracker._trackEvent("Videos", "Downloaded", "Gone With the Wind");</code></pre>
この場合、イベントラッキングの『概要』には1つのカテゴリ（Videos）しか表示されてないでしょう。また、ビデオオブジェクトに対するユーザー行動の指標のセットを確認できます。

しかしながら、2つ以上のオブジェクトをイベントトラッキングしたい場合、コードを実装する前にレポート上でどのように分類したいのか考慮する必要性があります。例えば、ある一人のユーザー行動ではなく、すべてのユーザー行動の総数を知りたいと思ったとき、『Videos』カテゴリ以下にある、すべてのビデオを別々にトッラキングすればよいだろう。

一方で、ビデオの種類（映画やPV等）によってカテゴリを分類したいかもしれない。またダウンロードは別にカテゴリ分けしたいかもしれない。
<ul>
	<li>Videos - Movies</li>
	<li>Videos - Music</li>
	<li>Downloads</li>
</ul>
このシナリオの場合、イベントトラッキングの『概要』にて3つのカテゴリのイベント総数を決定できる。『イベント数』はあなたが実装したカテゴリのすべてのイベントを表示する。しかしながら、あなたはDownloadsを抜いてVideosだけのイベント数を見ることできないだろう。なぜなら、詳細なイベント数はそれぞれのカテゴリでまとめられているから。

イベントトラッキンは柔軟性が高い一方で、あなたは同じようなWebオブジェクトで <em>_trackEvent()</em> メソッドを呼ぶ前に何よりも、あなたが望むレポートになるように設計すべきでしょう。もし、同じカテゴリ名を複数のページで使用する場合、それが正しいかどうか気をつける必要性が出てきます。例えば、ビデオをトラッキングするのに『Video』を使用し、その後、そのことを忘れて複数形の『Videos』を使うと2つの異なるカテゴリを持つことになります。加えて、すでにトラッキングしてしまったカテゴリ名を変えようとしたとき、変更以前のオリジナルのデータは新しいカテゴリ名にまとめられません。つまり、あなたは同じページの要素をトラッキングするのに2つのカテゴリを持つことになります。
<h3 id="ss02">アクション</h3>
イベントトラッキングにおいて、『アクション』は <em>_trackEvent() </em> メソッドの2番目のパラメータを参照しこれもまた必須です。
<pre><code>pageTracker._trackEvent("Videos", "Play", "Gone With the Wind");</code></pre>
一般的に、アクションのパラメータにはトッラキングしたい要素に対するイベント・行動のタイプを記述します。例えば、あるひとつの『Video』カテゴリにおいてこのパラメータで特定のイベント数を計測したい場合、以下のようなイベントが考えられます。
<ul>
	<li>ビデオのロードに要した時間</li>
	<li>"Play" ボタンのクリック数</li>
	<li>"Stop"ボタンのクリック数</li>
	<li>"Pause"ボタンのクリック数</li>
</ul>
カテゴリと同様に、『アクション』にどのような名前を付けるかはあなた次第でありますが、イベントアクションがどのように振る舞うのか２つの特徴を押さえておきましょう。

<strong>すべてのアクションはその親のカテゴリから独立してリストされる。</strong>
これはイベントデータでセグメントできるということである。
<strong>ユニークなイベントはユニークなアクション名によって決まる</strong>
カテゴリを超えて同じアクション名が使えるが、ユニークイベントの算出方法に影響する可能性がある。詳細は<a href="http://www.blogger.com/post-edit.g?blogID=1533537395474955628&amp;postID=5102672605018060117#ss05">Implicit Count</a>の項目を参照していただきたい。

サイト内で広範囲に設置したイベントトラッキングの最適なレポートをアーカイブするためにも以下のことを気をつけましょう。

<strong>アクション名はレポートデータと関連したものでなければならない</strong>
イベントトラッキングは異なるカテゴリの２つの同じアクション名のデータを合計します。例えば、もし"Click"とアクション名を"Downloads"と"Videos"カテゴリ内で使ったとすると、アクションレポートのトップには"Click"という名前ですべての行動が記録されます。カテゴリレポートの次のレベルで"Click”の詳細は見ることできますが、イベントトラッキングコードに"Click"というアクション名を見境なく実装すれば、そのセグメントのレポートは役にたたなくなってしまうでしょう。もしサイト全体で広範囲にイベントトラッキングしようとするのならば、カテゴリに関連づけられたアクション名を考慮すべきです。例えば、"Click"はガジェット系のインタラクションを表すためにとっておき、また"Play" "Pause"や"Stop"はビデオプレーヤー用のインタラクションに取っておいてもよいでしょう。

<strong>全体で使うアクション名はインタラクションをまとめられるか区別できるようなアクション名にすべきです。</strong>
例えば、あなたのサイトのすべてのビデオに"Video"カテゴリの"Play"というアクション名をつけます。このモデルでは、アクションレポートのトップには"Play"アクションの合計数が表示され、"Pause" や "Stop"のような他のアクションとどのくらい違うのか確認できます。

しかし、1つのVideosカテゴリー内で２つの異なるビデオプレーヤのUIについてもっと情報が欲しいとも思うでしょう。新たにカテゴリを作らずに異なるChromeのプレーヤを区別できます。このレポートではサイト上のすべてのビデオのデータを合計するするメリットも失うことなく２つのスタイルのプレーヤを区別できます。
<pre><code>videoTracker._trackEvent("Videos", "Play - Mac Chrome");
videoTracker._trackEvent("Videos", "Play - Windows Chrome");</code></pre>
<strong>アクションは必ずしも"action"を意味しません</strong>
アクションのパラメータにはどんな文字列でも指定できます。ある状況では、実際のイベントもしくはアクション名はその名の意味するものでもないので、アクションパラメータにほかの要素をトラッキングする情報を使用しても問題ありません。例えば、ページのダウンロード数を調べたいとき、ダウンロードイベントのアクションパラメータにドキュメントのファイルの種類を記述することができる。このシナリオでは、"Downloads"カテゴリ内にpdf、doc、 xlsのようなファイルの種類を確認できます。

<strong>ユーザアクションごとにユニークイベントが増加する </strong>
ユーザは特定のアクション名の付いた要素にインタラクションすると、最初のインタラクションはそのアクション名の１ユーザーとしてカウントされます。続いて同じアクション名のついた行動をしてもそのアクションのユニークイベントにはカウントされません。これは、たとえユーザがオブジェクトから離れたとしても、もしくはほかの同じアクション名のオブジェクトを操作しても、ユニークイベントはカウントされません。

レポートにおいて２つの注目すべき点があります。まず最初に、ユーザが別々のカテゴリにある2つの異なるビデオプレーヤの"Play"のボタン操作したとします。アクションレポートのトップには２つのプレーヤを操作したにもかかわらず１つのユニークイベントしか記録されていない点です。次に、各々のカテゴリのアクションレポートには１つのユニークアクションが記録されている点です。確かに、カテゴリ/アクションごとにユニークイベントは1回しか起きていません。詳細は<a href="http://www.blogger.com/post-edit.g?blogID=1533537395474955628&amp;postID=5102672605018060117#ss05">Implicit Count</a>をご覧ください。
<h3 id="ss03">ラベル</h3>
イベントトラッキングモデルの <em>_trackEvent()</em> メソッドの3番目のパラメータである。このパラメータはオプションです。ラベルを使うことで、上記例のビデオの映画タイトルやダウンロードファイルのファイル名のような詳細な情報を記述することができます。
<pre><code>pageTracker._trackEvent("Downloads", "PDF", "/salesForms/orderForm1.pdf");</code></pre>
カテゴリ、アクションと同様に、ラベルはすべてのラベル名を表示するレポートインターフェイスを持ちます。ラベル名はページのオブジェクトに対するユーザ操作レポートの項目を追加する方法として考えるべきです。例えば、あるページに5つのトラッキングしたいビデオプレーヤがあるとします。各々のプレーヤは"Videos" カテゴリの"Play" アクションとして記述できますが、ラベルにはレポートで区別して表示するために異なるラベルを（映画のタイトルなど）記述することができます。
<pre><code>pageTracker._trackEvent("Videos", "Play", "Gone With the Wind");
pageTracker._trackEvent("Videos", "Play", "Huckleberry Finn");</code></pre>
<h3 id="ss04">イベント値</h3>
"Value" は <em>_trackEvent()</em> メソッドで使える４番目のオプションのパラメータです。このパラメータは文字列というより整数値という点で他と異なるので、ページオブジェクトに対しては数値を割り当てなければなりません。例えば、プレーヤのロードする秒数や、ビデオプレーヤの特定の操作をドル価値に当てたものなど測定できます。
<pre><code>pageTracker._trackEvent("Videos", "Video Load Time", "Gone With the Wind", downloadTime);</code></pre>
このイベント値は数値として解釈され、レポートには各々のイベントカウント（下記<a href="http://www.blogger.com/post-edit.g?blogID=1533537395474955628&amp;postID=5102672605018060117#ss05"> Implicit Count</a>参照 ）の合計値が表示される。このレポートはカテゴリの平均値もまた測定できます。上記のコードにおいて、 <em>_trackEvent()</em> メソッドはビデオのロードが完了すると"Video Load Time" アクションが呼び出される。ビデオのタイトルはラベルによって決まり、各々のロード時間が正確に計測される。"Videos"の全ての"Video Load Time" アクションの平均値を確認することができる。あなたのサイトで5つのビデオダウンロードがあったとする。ダウンロード時間は以下の通りだ。
<ul>
	<li>10</li>
	<li>25</li>
	<li>8</li>
	<li>5</li>
	<li>5</li>
</ul>
レポートインターフェイスは以下の通りで数値は秒数を表している。
<table class="tbl" width="400">
<tbody>
<tr>
<th scope="col"># Visits w/Events</th>
<th scope="col">Value</th>
<th scope="col">Average Value</th>
</tr>
<tr>
<td>5</td>
<td>53</td>
<td>10.6</td>
</tr>
</tbody>
</table>
<em>現時点で負の値はサポートされていません。</em>
<h3 id="ss05">暗黙的カウント Implicit Count</h3>
イベントトラッキングにおいて、各々のページオブジェクトに対するインタラクションはカウントされ、ユーザーセッションに関連付けられています。レポート上、イベント総数はページオブジェクトに対するインタラクションの合計で計算される。一方で一回のユーザーセッションもしくは訪問で複数回のイベントを持つ場合、これは１訪問もしくは1ベントとしてカウントされます。

例えば、あるユーザーがビデオの同じボタンを５回クリックすると、ビデオの合計イベント数は５で、ユニークイベントは１ということになります。

以下の表によれば、カテゴリ内のレポート上でデータがのどのようにまとめらるのか分かるでしょう。この例では、同じカテゴリ名で２つの異なるビデオプレーヤがあり、ラベルによって区別されます。これらのプレーヤはFlash UI上で、"Play"や"Stop"などのアクション名を共有しています。
<table class="tbl"><caption>Event trackingfor "Videos" category</caption>
<tbody>
<tr>
<th scope="col">Action Type</th>
<th scope="col">Label: "Gone With the Wind"</th>
<th scope="col">Label: "Mr Smith Goes to Washington"</th>
<th scope="col">Totals</th>
</tr>
<tr>
<td scope="row">Play</td>
<td>10 visits w/Event</td>
<td>5 visits w/Event</td>
<td>15 unique events "Play"</td>
</tr>
<tr>
<td scope="row">Pause</td>
<td>2 visits w/Event</td>
<td>8 visits w/Event</td>
<td>10 unique events "Pause"</td>
</tr>
<tr>
<td scope="row">Stop</td>
<td>2 visits w/Event</td>
<td>3 visits w/Event</td>
<td>5 unique events "Stop"</td>
</tr>
<tr>
<th>Totals</th>
<td>14 unique events for GWTW</td>
<td>16 unique events for Mr Smith</td>
<td>30 unique events for category "videos"</td>
</tr>
</tbody>
</table>
上記の表は、別々のユーザーセッション・訪問において、"Gone With the Wind"と"Mr Smith Goes to Washington" のインタラクションが独立して発生していると想定しています。しかしながら、以下の表はどのようにアクションが計測されるのか、もう少し複雑で典型的な（一回の訪問に対して、ユーザがあるビデオの"Play"ボタンを押し、さらにもう一つ別のビデオの"Play"ボタンを押したりするような）例を用いて説明しています。ユニークイベント総数はラベルを超えて”Play”アクションのユニークイベント総数に対して影響します。アクションのラベルごとのユニークイベントは17であるけれども、これは関連するディメンションごとのユニークイベントの合計であることを注意してください。それで、"Videos"カテゴリ内のユニークイベントの合計数は16になり、訪問数も16になります。
<table class="tbl"><caption>Event Tracking Calculation for "Play" Action</caption>
<tbody>
<tr>
<th scope="col">Action Type</th>
<th scope="col">Label: "Gone With the Wind"</th>
<th scope="col">Label: "Mr Smith Goes to Washington"</th>
<th scope="col">Totals</th>
</tr>
<tr>
<td scope="row">Play</td>
<td>10 visits w/event</td>
<td></td>
<td>10 unique events "Play"</td>
</tr>
<tr>
<td scope="row">Play</td>
<td></td>
<td>5 visits w/event</td>
<td>5 unique events "Play"</td>
</tr>
<tr>
<td scope="row">Play</td>
<td colspan="2">1 visit w/event on BOTH movies (two clicks on "Play")</td>
<td>1 unique event "Play"</td>
</tr>
<tr>
<th>Totals</th>
<td>11 unique play events for GWTW</td>
<td>6 unique play events for Mr Smith</td>
<td>16 unique events for category "Videos" and 16 unique events for action "Play"</td>
</tr>
</tbody>
</table>
<h2 id="s03">実装上の注意事項</h2>
イベントトラッキングを実装する際に以下のことを覚えておいてください。
<h3>直帰率への影響</h3>
一般的に『直帰』というのは１ページだけの訪問と言われています。Google Analyticsにおいて、直帰は１回のGIFリクエストがトリガーとなって明確にセッションとして記録されます。それは、あるユーザーがあなたのサイトに来て、出て行く時に２回目のリクエストをAnalyticsサーバーにリクエストしないようなセッションです。しかしながら、イベントトラッキングが実装するのなら、あなたはこれらのイベントトラッキングコードが実装されているページの直帰率の変化に気づくでしょう。これらは原因はイベントトラッキングがGIFリクエストを発生させるためです。

例えば、ビデオプレーヤを埋め込んだページがあるとしましょう。通常このようなページは直帰率が高いです。加えて、このページにはイベントトラッキングコードは実装されていません。もし、その後このプレーヤにイベントトラッキングコードを実装したのなら、このページの直帰率は減少するはずです。なぜなら、Google Analyticsはユーザのビデオプレーヤに対するインタラクションを記録し、サーバにGIFリクエストを送信しているのです。したがって、実際に直帰している人の割合は変わっていないけれども、ビデオプレーヤのイベントトラッキングが読み込まれるため、このような振る舞いは直帰とは見なされないのです。

このように、イベントトラッキングを実装したページの『直帰』とは普通とは微妙に違うことを意味します。1ページだけの訪問とはトラックイベントを含まないことです。

<em>ページロード時に自動的にイベントトラッキングを実装するような場合、直帰率がゼロになることありますので、非常に注意しなければなりません。このようなケースはTimeTrackerの例や同様なユーティリティ的な実装に起こります。</em>
<h3>イベント毎のセッション時間</h3>
一回の訪問（ユーザーセッション）で、トラッキングできるGATCリクエスト（イベントもPVも含めて）の最大数はおおよそ500です。プログラム的にイベントを生成する場合は覚えておかなければなりません。注意すべきことは、一回のセッションでリクエスト数が限界に近づくにつれて、イベントはトッラキングされないかもしれません。例えば、このようにすべきです。
<ul>
	<li>再生している毎秒ごとにイベントは発生させたり、連続的に発生するイベントトリガーを生成するようなスクリプトは避けるべきです</li>
	<li>マウスの動きを過度にトラッキングすることは避けるべきです。</li>
	<li>細かくカウントするようなタイムラップの仕組みは避けるべきです。</li>
</ul>
さらにセッションの仕組みについての情報が欲しければ、<a href="http://www.google.com/support/analytics/bin/answer.py?answer=33073">このトピック</a>を参照してください。
