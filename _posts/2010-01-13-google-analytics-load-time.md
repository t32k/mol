---
layout: post
title: Google Analyticsでページロード時間を計測する
categories:
- analytics
tags:
- GA
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2010/01/page-load-time.html
  _edit_last: '1'
  pvc_views: '4025'
  _topsy_long_url: http://t32k.me/mol/2010/01/google-analytics-load-time/
  topsy_short_url: http://bit.ly/a7rgoo
---
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/0470562315/warikiru-22/ref=nosim/" target="_blank"><img class="fig" style="border: 0pt none;" src="http://ecx.images-amazon.com/images/I/51SGTdagbaL._SL160_.jpg" border="0" alt="Advanced Web Metrics with Google Analytics" width="125" height="160" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/Advanced-Web-Metrics-Google-Analytics/dp/0470562315%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D0470562315" target="_blank">Advanced Web Metrics with Google Analytics</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" />
Brian Clifton </span>

<span>Sybex  2010-03-15
売り上げランキング : 50643</span>

<span><a href="http://www.amazon.co.jp/Advanced-Web-Metrics-Google-Analytics/dp/0470562315%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D0470562315" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
はい、タイトル通りです。Advanced Web Metricsをパラパラ見てたらおもしろそうな項目を見つけたので自分のブログでもやってみようと思った次第です。ただ、若干古いトラッキングコードを使っている点ともうちょっとイベントトラッキングで遊びたかったので、サンプルコードを改造しています。
<a name="more"></a>
<div style="color: #4c1130; text-align: center;"><strong>注意：このコードは直帰率に影響します。詳しくは後述を参照。</strong></div>
<h5>コード実装編</h5>
先ずは以下のSCRIPT要素をBODY開始タグの直後に記述しましょう。
<pre><span style="color: #666666;">&lt;body&gt;</span>
&lt;script type='text/javascript'&gt;
<em style="color: #38761d;"> var Begin = new Date();
 var Start = Begin.getTime();
</em>&lt;/script&gt;

<span style="color: #666666;"> [ ページのコンテンツ]</span></pre>
はい、では次に以下のSCRIPT要素をBODY終了タグの直前に記述しましょう。
<pre>&lt;script type='text/javascript'&gt;
<span style="color: #666666;">try {var pageTracker = _gat._getTracker("UA-xxxxxxx-1");
pageTracker._trackPageview();</span><em><span style="color: #38761d;">

 var End = new Date();
 var Stop = End.getTime();
 var timeElapse = Stop - Start; // stored as millsecond
 var Url = location.href;
 pageTracker._trackEvent(  'Page Load',  'Load Time',  Url,  timeElapse</span>);</em><span style="color: #666666;">

 } catch(err) {}
</span>&lt;/script&gt;</pre>
BODY要素の始まりと終わりにDateメソッドでタイムスタンプをして、その差分の時間を見ようって寸法です。そして、その値をイベントトラッキングメソッドに渡しています。トラッキングコードをテンプレートに入れても大丈夫なようにlocation.hrefでそのページのURLも渡しています。

つまり、上記のコードは以下のような構造になっていますね。
<ul>
	<li><strong> 1. カテゴリ：Page Load</strong></li>
	<li><strong> 2. アクション：Load Time</strong></li>
	<li><strong> 3. ラベル：ページのURL</strong></li>
	<li><strong> 4. バリュー：ロード時間</strong></li>
</ul>
コードを記述したらデータが貯まるまで待ちましょうzzz
<h5>レポート編</h5>
<a title="イベントトラッキングサマリー by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/4268309583/"><img class="fig" src="http://farm5.static.flickr.com/4003/4268309583_9c1bb0f29a.jpg" alt="イベントトラッキングサマリー" width="491" height="500" /></a>

レポートの『<strong>コンテンツ</strong>』＞『<strong>イベントトラッキング</strong>』を見るとカテゴリ名が『<strong>Page Load</strong>』アクション名が『<strong>Load Time</strong>』って項目が見えてきますのでクリックしましょ。

<a title="イベントトラッキングラベル by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/4268309655/"><img class="fig" src="http://farm3.static.flickr.com/2778/4268309655_ea908d8cb2.jpg" alt="イベントトラッキングラベル" width="500" height="368" /></a>

そうすると、<strong>ラベル：ページURL</strong>毎の<strong>イベント値：ロード時間</strong>が確認できるでしょう。まぁこれでは、ちょっとおもしろくないのでデータの見せ方を変えてみましょう。

<a title="イベントトラッキングラベル（ピボット） by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/4268309803/"><img class="fig" src="http://farm3.static.flickr.com/2722/4268309803_bb8367c678.jpg" alt="イベントトラッキングラベル（ピボット）" width="500" height="315" /></a>

表示形式（青枠部分）を<strong>ピボット形式</strong>にして、ピボット（青枠部分）の値を<strong>ブラウザ</strong>にしてみましょう。なんということでしょう。ブラウザ毎のロード時間が確認できるようになりましたね。今回の計測の場合、FxとIEと比べてみたら断然にFxの方がロード時間が短いという結果も理解できるかと思います。

また、<a href="http://warikiru.blogspot.com/2009/11/high-performance-web-design.html">1番のページ</a>はフラッシュオブジェクトや画像が多いので他のページよりも重いので、<a href="http://warikiru.blogspot.com/2009/11/design-at-facebook.html">5番のテキストだけのページ</a>よりもロード時間が長いのも理解できますよね。レポートの値もそうなっています。まぁ、絶対値がどうとか言うよりもページ毎に比較できるようになったのでこれを参考にパフォーマンス改善していけばいいんじゃないでしょうか。

余談ですが、コードの実装段階でブラウザ情報もJSで取得してイベントトラッキングに渡そうと思ったんだけど、難しくて良く分かんなかった。でも考えてみたらGAの本体コードでブラウザ情報取っているわけだからそれをなんとかできんもんかといろいろ弄ってたら、たまたまできましたｗGoogle Analyticsおもしろいですね。
<h5>不具合編</h5>
<a title="ユーザーの直帰率 by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/4268309861/"><img class="fig" src="http://farm5.static.flickr.com/4006/4268309861_20725d427e.jpg" alt="ユーザーの直帰率" width="500" height="426" /></a>

不具合というか、そういう仕様なので仕方がないのですが、このコードを入れると直帰率が減少していきます。ゼロにもなります。というのもGoogle Analyticsの直帰率の定義が１回のGIFリクエストとなっているので。詳しくは以下を参照。
<blockquote><span style="font-size: x-small;"><strong>直帰率への影響</strong>
一般的に『直帰』というのは１ページだけの訪問と言われています。Google Analyticsにおいて、直帰は１回のGIFリクエストがトリガーとなって明確にセッションとして記録されます。それは、あるユーザーがあなたのサイトに来て、出て行く時に２回目のリクエストをAnalyticsサーバーにリクエストしないようなセッションです。しかしながら、イベントトラッキングが実装するのなら、あなたはこれらのイベントトラッキングコードが実装されているページの直帰率の変化に気づくでしょう。これらは原因はイベントトラッキングがGIFリクエストを発生させるためです。</span>

一回の訪問（ユーザーセッション）で、トラッキングできるGATCリクエスト（イベントもPVも含めて）の最大数はおおよそ500です。
<a href="http://warikiru.blogspot.com/2009/09/event-tracking-guide.html%20"></a>
<div style="text-align: right;"><a href="http://warikiru.blogspot.com/2009/09/event-tracking-guide.html"><span style="font-size: x-small;">Google Analytics イベントトラッキングガイド | warikiru</span></a></div></blockquote>
つまり、ページを読み込んだ時点でブラウザ情報など基本的な情報がGIFリクエストとしてAnalyticsサーバーに送信されるとともに、ページのロード時間を計測したイベントトラッキングの情報もGIFリクエストされるので1ページ見ただけで２回のGIFリクエストしたことになります。これは普通に2ページ見たのと同じだとGAは解釈するわけで、つまり直帰していないという風にレポートでは表示されます。

そのほかにもマウスオーバーや、ビデオプレーヤのボタンクリックなどページ遷移をしないイベントでトラッキングすると意図しない直帰率の減少が懸念されますので注意してくださいね。

なんか上手い回避方法ないんですかね... せめて回避方法はなくてもプロファイルでフィルタでデータを整理とかできんもんかなと。誰か偉い人教えてください＞＜

[追記]
新たにプロパティID発行してロード時間測定用のオブジェクトとして別で計測すればレポート分離できるなと思いついた。あとで試す。
