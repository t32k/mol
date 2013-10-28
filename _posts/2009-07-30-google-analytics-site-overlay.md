---
layout: post
title: Google Analyticsの『サイト上のデータ表示』は信頼できるのか？
categories:
- analytics
tags:
- google analytics
status: publish
type: post
published: true
meta:
  pvc_views: '3132'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/07/google-analytics-site-overlay.html
  _edit_last: '1'
---
<img class="aligncenter" src="http://lh4.ggpht.com/_1drnogi3vdg/SnFOnMi2ijI/AAAAAAAAAeQ/d0yu8Sumky0/ga.png" alt="Site Overlay Report" width="520" height="232" />
<img class="alignleft" style="margin: 12px;" src="http://lh5.ggpht.com/_1drnogi3vdg/SnAE1vt6DHI/AAAAAAAAAdo/H4H_ix2eryA/ga2.png" alt="" width="180" />
ちょっと調べてみた。

『サイト上のデータ表示』とは『コンテンツ』ナビゲーションの下にある機能で、ページにあるリンクのクリック率がわかるというものです。小難しい数字の羅列のレポートとは違って、どこが押されているのか直感的に分かる素晴らしい機能ですが、個人的には毎回ちょっと違和感を覚える結果だったので何となく信用していませんでした。

先日、会社の方でこの機能を見たらクリック率がすべて0%になっている、ありえない状態を発見したので、この『サイト上のデータ表示』はどのような仕組みで動いてるのか気になったので調べてみました。
<h3>なぜクリック率がすべて0%になっていたのか？</h3>
<blockquote><span class="Apple-style-span" style="font-weight: bold;">URL の書き換え</span>
フィルタを使用して URL を書き換ると、実際の HTML に記述されたリンクの URL とコンテンツ サマリー レポートの [ナビゲーション サマリー] に表示されるフィルタで書き換えられた URL は一致しなくなります。 この場合、サイト上のデータ表示レポートは、HTML のリンクとレポートに記録されたデータを正しく関連付けられなくなります。
<div style="text-align: right;">

<a href="http://www.google.com/support/googleanalytics/bin/answer.py?hlrm=en&amp;answer=66982"><span class="Apple-style-span" style="font-size: small;">サイト上のデータ表示が機能しません。- Analyticsヘルプ</span></a>

</div></blockquote>
Analyticsヘルプに見たらあっさり解決しましたｗ

確かに会社の方では複数のサブドメインをひとつのプロファイルでまとめていたので、ドメインを表示させるアドバンスフィルタ（通常のURL表示はドメイン以下のみを表示する仕様なので）をかけてありました。でもね、これね、もとはと言えば、↓これを見てやったのに。。
<ul>
	<li><a href="http://www.google.com/support/googleanalytics/bin/answer.py?hl=jp&amp;answer=55524"><span class="Apple-style-span" style="font-size: small;"><span class="Apple-style-span" style="font-weight: bold;">サイトのすべてのサブドメインを 1 つのプロファイルでトラッキングする - Analytics ヘルプ</span></span></a></li>
</ul>
別にいらんことしたわけじゃないんですよｗ　言われたとおりやっただけなのに、ほかの機能が使えなくなるのはどうかなと思ってしまいます。まぁ無料だからね。。

とはいえ、もしフィルタを使ってなかったとしても『サイト上のデータ表示』は少々癖があります。
<h4><span class="Apple-style-span" style="font-weight: bold;">同一URLリンクはまとめてカウントされる</span></h4>
例えば、同じページ上に『トップページへ戻る』リンクがサイトロゴ画像とテキストリンクであった場合、それらは同じURLなので、まとめてカウントされます。（実際はサイトロゴが6回、テキストリンクが4回クリックされたとしても、GA上ではどちらもクリック数10と表示されます。）
<h4><span class="Apple-style-span" style="font-weight: bold;">（A要素のhref属性で記述された）標準的なリンクしか計測できない</span></h4>
ざっと挙げる限りこれだけ計測できないリンク（というかクリックイベント）がある。
<ul>
	<li>JavaScriptリンク（onclick属性でwindow.openなど）</li>
	<li>pageTrackerで作成した仮想ページビュー（_trackPageview()など）</li>
	<li>URLリダイレクト</li>
	<li>サブドメインのページへのリンク</li>
	<li>外部サイトへのリンク</li>
	<li>ダウンロードファイル(PDFに直リンクとか)</li>
	<li>フレームへのリンク</li>
	<li>フォームのinputボタン</li>
	<li>Flashコンテンツ</li>
	<li>イメージマップ（AREA要素のhref属性なので）</li>
</ul>
URLの書き換えの項を見る限り、[ナビゲーション サマリー]のデータを基にしているのかもしれない。だから、A要素のhref属性でも飛び先にga.jsがインクルードされていない外部サイト、ダウンロードファイルなどは計測されないのね。結局、使いどころとしてはあまりやんちゃなことしてない静的ページくらいしか使えないのかもしれない。

同じような機能で有料のCrazyEggがあるので、オーバーレイで直感的に確認したいという方はそちらの方の使用を薦める。ただ、CrazyEggもCSSの兼ね合いによっては不具合が予想されるのでそこは注意したい。
<ul>
	<li><a href="http://crazyegg.com/help/Viewing_Results/Why_is_my_report_data_misaligned_from_my_actual_site/">Why is my report data misaligned from my actual site? - Crazy Egg</a></li>
	<li><a href="http://crazyegg.com/help/Viewing_Results/Why_is_my_website_not_displaying_all_the_images_or_CSS/">Why is my website not displaying all the images or CSS?  - Crazy Egg</a></li>
</ul>
<h4><span class="Apple-style-span" style="font-size: small;">参考サイト</span></h4>
<ul>
	<li><a href="http://www.analyticsexperts.com/google-analytics/site-overlay-is-not-working-why-not/"><span class="Apple-style-span" style="font-size: small;">Site overlay is not working, why not?</span></a><span class="Apple-style-span" style="font-size: small;">
</span></li>
	<li><a href="http://blog.vkistudios.com/index.cfm/2008/12/12/Google-Analytics-Power-User-Part-2--Site-Overlay-Report"><span class="Apple-style-span" style="font-size: small;">Site Overlay Report: Google Analytics Power User Part 2 - VKI Studios Blog</span></a></li>
</ul>
