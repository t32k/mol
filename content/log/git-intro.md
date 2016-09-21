---
date: 2014-04-07
title: 開発効率をUPする Git逆引き入門
categories: 
    - books
excerpt: "id:Layzieさんより本頂いた。僕からはどちらからと言えば、デザイナー側からのレビューをしたいと思う。"
---

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4863541465/warikiru-22/ref=nosim/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/51RtoUsheVL._SL160_.jpg" alt="開発効率をUPする Git逆引き入門" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4863541465/warikiru-22/ref=nosim/" name="azlinklink" target="_blank">開発効率をUPする Git逆引き入門</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2016.1.23</div></div><div class="azlink-detail">松下 雅和,船ヶ山 慶,平木 聡,土橋 林太郎,三上 丈晴<br />シーアンドアール研究所<br />売り上げランキング: 366953<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4863541465/warikiru-22/ref=nosim/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

[id:Layzie](http://layzie.hatenablog.com/entry/20140403/1396509428)さんより本頂いた。なお著者は全員緑の会社の人である。この本はデザイナー・エンジニア両方をターゲットとしているみたいなので、僕からはどちらからと言えば、デザイナー側からのレビューをしたいと思う。

そもそも弊社某緑の会社ですが2年前くらいまではどのプロジェクトもSVNを使用していたが、1年前くらいに[GitHub Enterprise](https://enterprise.github.com/)を全社的に導入する（CAに入るとGHE使えるんだよヽ(=´▽`=)ﾉ）にあたって、SVNからGitへバージョン管理システムを移行しなければならない状況になった。その時、今回の著者の方々が移行のための勉強会を何回も開催してくれたのだった。

全社的に導入するにあたって、当然デザイナーや、HTMLコーダーのような非エンジニアに対してもフォローしなければならない。そうゆう理由もあってかこの本にはGUIクライアントである[SourceTree](http://www.sourcetreeapp.com/)の説明も多い。数多くGUIクライアントはあるが、無料でありWin/Macで問題なく動作するという意味ではSourceTreeが妥当な選択だったと思う。

また、僕のような非エンジニアが初めてGitを触った時はとりあえずはエンジニアさんから言われたとおり、AddしてCommitしてPushして、たまにブランチを切るくらいで、なんかよく分かんなくなったら、ローカルレポジトリ全部消してもう一回リモートレポジトリをPullしてくるのが精一杯だった（今でも似たようなもんだが…）。そのようなGit初心者に対して、最初から裏ワザ的なオプションとかいろいろ教えられてもキャパオーバーである。

<iframe src="http://www.slideshare.net/slideshow/embed_code/28304397" width="597" height="486" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px 1px 0; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="https://www.slideshare.net/matsukaz/git-28304397" title="いつやるの？Git入門 v1.1.0" target="_blank">いつやるの？Git入門 v1.1.0</a> </strong> from <strong><a href="http://www.slideshare.net/matsukaz" target="_blank">Masakazu Matsushita</a></strong> </div>

その点、本書に関しては図解も抱負でシンプルに解説されており非エンジニアにも優しい（SourceTreeの操作画面もふんだんにある）。本書のメイン著者である[@matsukaz](https://twitter.com/matsukaz)のスライドを見れば、その分かりやすさが理解できると思う。

この辺りに関しては、『いや、Gitのすべてを知りたいんだ！』って人もいれば、『最低限、使えればいーや』って人もいると思うので、自分にあった本を選択すれば良いと思うが、本書は少なくとも前者ではない。

弊社のように全社導入的な事例では、つまり全体のボトムアップという意味では業務で必要なことを必要な分だけ勉強できる本書のようなタイプが適切なんだろうと思う。まさしく、緑社のGit導入マニュアルと言っても過言ではないだろう。




