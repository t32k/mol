---
layout: post
title: Googleを支える技術 ~巨大システムの内側の世界
categories:
- books
tags:
- google
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/11/google-search-system.html
  _edit_last: '1'
  pvc_views: '1869'
---
<table border="0" cellpadding="5"><tbody><tr><td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4774134325/warikiru-22/ref=nosim/" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51m8phYZbyL._SL160_.jpg" alt="Googleを支える技術 ‾巨大システムの内側の世界 (WEB+DB PRESSプラスシリーズ)" border="0" /></a></td><td valign="top"><span style="font-size:85%;"><a href="http://www.amazon.co.jp/Google%E3%82%92%E6%94%AF%E3%81%88%E3%82%8B%E6%8A%80%E8%A1%93-%E2%80%BE%E5%B7%A8%E5%A4%A7%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%81%AE%E5%86%85%E5%81%B4%E3%81%AE%E4%B8%96%E7%95%8C-WEB-DB-PRESS%E3%83%97%E3%83%A9%E3%82%B9%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA/dp/4774134325%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4774134325" target="_blank">Googleを支える技術 ‾巨大システムの内側の世界 (WEB+DB PRESSプラスシリーズ)</a><img src="http://www.blogger.com/%27http://www.assoc-amazon.jp/e/ir?t=" l="ur2&amp;o=" 9="" alt="''" border="0" height="1" width="1" /><br /><br />技術評論社  2008-03-28<br />売り上げランキング : 15225<br />おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-4-5.gif" /><br /><br /><a href="http://www.amazon.co.jp/Google%E3%82%92%E6%94%AF%E3%81%88%E3%82%8B%E6%8A%80%E8%A1%93-%E2%80%BE%E5%B7%A8%E5%A4%A7%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%81%AE%E5%86%85%E5%81%B4%E3%81%AE%E4%B8%96%E7%95%8C-WEB-DB-PRESS%E3%83%97%E3%83%A9%E3%82%B9%E3%82%B7%E3%83%AA%E3%83%BC%E3%82%BA/dp/4774134325%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4774134325" target="_blank">Amazonで詳しく見る</a></span><span style="font-size:85%;"> </span><span style="font-size:85%;">by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td></tr></tbody></table><br />『ググる』と瞬時に検索結果が返されるのが当たり前で、しかも遅いことを体験したことがないので、その凄さをつい忘れてしまうけど、本書を読んでGoogleの並々ならぬ努力を改めて理解した。考えてみれば、世界中のWebページをインデックスしてる時点で数千億、数兆？ページぐらいあるのだから、そこから最適な結果を0.何秒以内に返すってすごいことだなと思う。だってDreamweaverでちょっと容量のあるページを検索しても1秒以上かかることを考えれば、Webデザイナーの僕でもその凄さは理解できる。<br /><br />　本書は検索システムの簡単な説明から<span style="font-weight: bold;">GFS</span> (Google Fire System：分散ファイルシステム)、<span style="font-weight: bold;">Bigtable </span>(分散ストレージステム)、<span style="font-weight: bold;">Chunbby </span>(分散ロックサービス)、<span style="font-weight: bold;">MapReduce</span>（分散処理のための基盤技術）、<span style="font-weight: bold;">Sawzall </span>(手軽に分散処理するための専用言語)など、お馴染みのGoogleシステムについて解説している。<br /><br />僕はちょっと専門外なので完璧には理解できなかったけど、なんとなく分かったような気がした。というか、GFS! Bigtable! ってゆう単語聞くだけでワクワクするようなミーハーなのでｗ　ここら辺はせひともプロジェクトXなんかの番組にしたらおもしろいなと個人的に思った。<br />　<br />『データーセンターが火災で焼失した。それでもシステムは動き続けた。エンジニアは誇らしげだった（田口トモロヲ風）』<br /><br />なんて具合にｗ
