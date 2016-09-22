---
date: 2016-09-22
title: カスタムドメインのGitHub PagesをSSL対応する
subtitle: Secure and fast GitHub Pages
categories: 
    - development
excerpt: HTTPSってええやん？
---

![](/mol/images/2016/0922-00.png)

このブログは、[Hugo + GitHub Pagesで運用](/mol/log/hugo/)している。`*.github.io`みたいなGitHubが提供しているドメインなら既にHTTPSの恩恵を受けられるが`t32k.me`のカスタムドメインを使用している場合はその限りではない。そうゆうわけで、21世紀だし`https://t32k.me`を目指す。

- [HTTPS for GitHub Pages](https://github.com/blog/2186-https-for-github-pages)

以前にrudolph君さんパイセンが、Kloudsecを使えばチョー楽っすよ！って言ってたのを思い出して、それを使ってみようとしてみたが既に[サービスが終了](https://www.reddit.com/r/webdev/comments/4s3kmf/got_an_email_saying_that_kloudsec_will_be/)していた／(^o^)＼

- [Kloundsec for SSL with Custom Domain on GitHub Pages \- \(rudolph\-miller\)](https://blog.rudolph-miller.com/2016/03/11/kloudsec-for-ssl-with-custom-domain-on-gh-pages/)

というわけで、1000ch君さんパイセンの記事にあるように、CloudFlareを使用してSSL対応する。

- [GitHub Pagesに設定しているカスタムドメインをHTTPS対応させる \- 1000ch\.net](https://1000ch.net/posts/2015/github-pages-custom-domain-in-https.html)

## CloudFlareでの登録

まずは、CloudFlareのアカウントを登録しよう。

- [CloudFlare \- The web performance & security company](https://www.cloudflare.com/)

んで、自分のサイトを追加する(Add Site)。次にCloudFlare Planを選べといわれるが、Free Planでも問題ない。`xxx.ns.cloudflare.com`みたいなネームサーバーが2つ、もらえるので、それに変更する。

![](/mol/images/2016/0922-01.png)

自分の場合、ドメインはお名前.comで取得したので、そこでネームサーバーを変更する。変更が反映されると、自分の追加したサイトのステータスがPendingからActiveに変わる。

![](/mol/images/2016/0922-02.png)

あとは、Page Rulesのページに行き、自分のドメインのHTTPページのすべてのアクセスをHTTPSに変更する処理を設定すれば完璧だ。

## 後処理

しばらくするとHTTPSにリダイレクトされるようになるので、寝て待とう（最大で24時間かかるとか）。自分のサイトでHTTPからのリソース読み込みがあるとちゃんと緑の鍵アイコンにならないので、調べておこう。基本的に自分のドメイン配下のリソースはルートからの相対パスで書いているので、特に問題はなかった。ただ、Amazonのアフィリエイト画像がHTTPからの読み込みだったので[全置換して対応](http://d.hatena.ne.jp/takeR/20141026/1414356669)した。

やっぱり、ドメイン系は反映に時間がかかるのでやきもきしたが、終わってみれば簡単だった。

- [Secure and fast GitHub Pages with CloudFlare](https://blog.cloudflare.com/secure-and-fast-github-pages-with-cloudflare/)