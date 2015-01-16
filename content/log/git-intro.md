---
date: 2014-04-07
title: 開発効率をUPする Git逆引き入門
categories: blog
excerpt: "id:Layzieさんより本頂いた。僕からはどちらからと言えば、デザイナー側からのレビューをしたいと思う。"
---

<table  border="0" cellpadding="5"><tr><td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4863541465/warikiru-22/ref=nosim/" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51RtoUsheVL._SL160_.jpg" border="0" alt="開発効率をUPする Git逆引き入門" /></a></td><td valign="top"><font size="-1"><a href="http://www.amazon.co.jp/%E9%96%8B%E7%99%BA%E5%8A%B9%E7%8E%87%E3%82%92UP%E3%81%99%E3%82%8B-Git%E9%80%86%E5%BC%95%E3%81%8D%E5%85%A5%E9%96%80-%E6%9D%BE%E4%B8%8B-%E9%9B%85%E5%92%8C/dp/4863541465%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4863541465" target="_blank">開発効率をUPする Git逆引き入門</a><img src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&l=ur2&o=9" width="1" height="1" style="border: none;" alt="" /><br />松下 雅和 船ヶ山 慶 平木 聡 土橋 林太郎 三上 丈晴 <br /><br />シーアンドアール研究所  2014-04-09<br />売り上げランキング : 306<br /><br /><a href="http://www.amazon.co.jp/%E9%96%8B%E7%99%BA%E5%8A%B9%E7%8E%87%E3%82%92UP%E3%81%99%E3%82%8B-Git%E9%80%86%E5%BC%95%E3%81%8D%E5%85%A5%E9%96%80-%E6%9D%BE%E4%B8%8B-%E9%9B%85%E5%92%8C/dp/4863541465%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4863541465" target="_blank">Amazonで詳しく見る</a></font> <font size="-2">by <a href="http://www.goodpic.com/mt/aws/index.html" >G-Tools</a></font></td></tr></table>


[id:Layzie](http://layzie.hatenablog.com/entry/20140403/1396509428)さんより本頂いた。なお著者は全員緑の会社の人である。この本はデザイナー・エンジニア両方をターゲットとしているみたいなので、僕からはどちらからと言えば、デザイナー側からのレビューをしたいと思う。

そもそも弊社某緑の会社ですが2年前くらいまではどのプロジェクトもSVNを使用していたが、1年前くらいに[GitHub Enterprise](https://enterprise.github.com/)を全社的に導入する（CAに入るとGHE使えるんだよヽ(=´▽`=)ﾉ）にあたって、SVNからGitへバージョン管理システムを移行しなければならない状況になった。その時、今回の著者の方々が移行のための勉強会を何回も開催してくれたのだった。

全社的に導入するにあたって、当然デザイナーや、HTMLコーダーのような非エンジニアに対してもフォローしなければならない。そうゆう理由もあってかこの本にはGUIクライアントである[SourceTree](http://www.sourcetreeapp.com/)の説明も多い。数多くGUIクライアントはあるが、無料でありWin/Macで問題なく動作するという意味ではSourceTreeが妥当な選択だったと思う。

また、僕のような非エンジニアが初めてGitを触った時はとりあえずはエンジニアさんから言われたとおり、AddしてCommitしてPushして、たまにブランチを切るくらいで、なんかよく分かんなくなったら、ローカルレポジトリ全部消してもう一回リモートレポジトリをPullしてくるのが精一杯だった（今でも似たようなもんだが…）。そのようなGit初心者に対して、最初から裏ワザ的なオプションとかいろいろ教えられてもキャパオーバーである。

<iframe src="http://www.slideshare.net/slideshow/embed_code/28304397" width="597" height="486" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px 1px 0; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/matsukaz/git-28304397" title="いつやるの？Git入門 v1.1.0" target="_blank">いつやるの？Git入門 v1.1.0</a> </strong> from <strong><a href="http://www.slideshare.net/matsukaz" target="_blank">Masakazu Matsushita</a></strong> </div>

その点、本書に関しては図解も抱負でシンプルに解説されており非エンジニアにも優しい（SourceTreeの操作画面もふんだんにある）。本書のメイン著者である[@matsukaz](https://twitter.com/matsukaz)のスライドを見れば、その分かりやすさが理解できると思う。

この辺りに関しては、『いや、Gitのすべてを知りたいんだ！』って人もいれば、『最低限、使えればいーや』って人もいると思うので、自分にあった本を選択すれば良いと思うが、本書は少なくとも前者ではない。

弊社のように全社導入的な事例では、つまり全体のボトムアップという意味では業務で必要なことを必要な分だけ勉強できる本書のようなタイプが適切なんだろうと思う。まさしく、緑社のGit導入マニュアルと言っても過言ではないだろう。




