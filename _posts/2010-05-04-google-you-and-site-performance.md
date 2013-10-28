---
layout: post
title: Googleとあなたとサイトパフォーマンス
categories:
- performance
- translate
tags:
- google
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '4062'
---
<a href="http://googlewebmastercentral.blogspot.com/2010/05/you-and-site-performance-sitting-in.html">Official Google Webmaster Central Blog:You and site performance, sitting in a tree...</a> より

<object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" width="470" height="285" codebase="http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,40,0"><param name="allowFullScreen" value="true" /><param name="allowscriptaccess" value="always" /><param name="src" value="http://www.youtube.com/v/OpMfx_Zie2g&amp;hl=ja_JP&amp;fs=1&amp;rel=0" /><param name="allowfullscreen" value="true" /><embed type="application/x-shockwave-flash" width="470" height="285" src="http://www.youtube.com/v/OpMfx_Zie2g&amp;hl=ja_JP&amp;fs=1&amp;rel=0" allowscriptaccess="always" allowfullscreen="true"></embed></object>

「ウェブマスターのためのサイトパフォーマンス」という題でMaile Ohyeさんが解説しています。英語は聞き取れないのですが、なんとなく言っていることとして。

<!--more-->

スピードの必要性ってことで、<a href="http://t32k.me/mol/2010/03/performance-business/">Shopzilla</a>, <a href="http://blog.mozilla.com/metrics/2010/03/22/addition-by-subtraction/">Firefox</a>でのコンバージョン増加の事例を説明してあったり、<a href="http://t32k.me/mol/2009/11/introduction-to-web-performance/">Google/Microsoft</a>のテストの事例など説明しています。

SEOに関しては、スピードは200以上あるアルゴリズムの1つにしかすぎない。コンテンツと関連性がいまだに重要だと言っています。

フロントエンドを改善すればパフォーマンスは良くなるし、すごく簡単ですよってことで、<a href="http://www.webpagetest.org/test">WebPagetest</a>を使ったり、<a href="http://twitter.com/maileohye">@maileohy</a>が<a href="http://maileohye.com/">自分のサイト</a>をPage Speedでテストして、Expireの設定を実演してくれています。

んで、ここから重要なQ&amp;Aってことで、文字におこしてあったので、翻訳
<h3>Q&amp;A</h3>
<strong>世界中の異なる地域からの自分のサーバーのレスポンスタイムを確認することができますか？</strong>

はい、できます。<a href="http://www.webpagetest.org/test">WebPagetest.org</a>では、米国（東海岸、西海岸両方とも）、英国、中国、ニュージーランドからのパフォーマンステストをすることが可能です。

<strong>目標にすべきベストなレスポンスタイムはどのくらいなのでしょうか？</strong>

まず、もし、あなたの競合会社が速いページだったとしたら、彼らはあなたの会社よりも良いユーザーエクスペリエンスを提供できていることになります。この場合においては、競合会社よりも速く、良いサイトにすれば良いでしょう。

また、別の観点から言えば、<a href="http://www.akamai.com/html/about/press/releases/2009/press_091409.html">Akamaiが調査</a>したデータによると、Eコマースサイトにおいてユーザーが許容できるのは2秒までという報告があります。参考までに、Googleにおいては、0.5秒以下を目標にしています。

<strong>プログレッシブ・レンダリングはユーザーに役立ちますか？</strong>

間違いなく！プログレッシブ・レンダリングは全てのコンテンツの読み込みを待って一度に表示するのではなく、読み込みが完了したコンテンツから徐々に表示していきます。これは、ユーザーに視覚的なフィードバックを提供できるとともに、ユーザーがコントロールしているという印象も与えます。<a href="http://www.bing.com/">Bing</a>が<a href="http://assets.en.oreilly.com/1/event/29/The%20User%20and%20Business%20Impact%20of%20Server%20Delays,%20Additional%20Bytes,%20and%20HTTP%20Chunking%20in%20Web%20Search%20Presentation.pptx">プログレッシブ・レンダリングについての実験（pptxファイル）</a>をしました。それは、ビジュアルヘッダー（ロゴや検索ボックスのようなもの）をまず表示させ、その次に、検索結果や広告を利用可能にするという方法です。その結果、Bingはプログレッシブ・レンダリングによって、ユーザーの満足度が0.7％向上したことを発見しました。彼らはこの改善はフルバージョンアップ並の効果をもたらしたとコメントしました。

どうしたらプログレッシブ・レンダリングを実装できるのでしょうか？<a href="http://code.google.com/speed/page-speed/docs/rtt.html#PutStylesBeforeScripts">ページの上部にスタイルシート</a>を置くだけです。これで、ブラウザは可能な限り速く、レンダリングを開始します。

--

そんなわけで、プログレッシブ・レンダリングはHTTPリクエストなどこれ以上減らせないって時に、役に立つ考え方ですね。読み込み速度は変わらないんだけども見せ方で速く表示できているように感じさせる。この辺、興味ありありです、個人的に。
