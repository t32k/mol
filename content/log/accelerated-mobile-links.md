---
date: 2017-01-24
title: Accelerated Mobile Linksを試してみる
subtitle: Introducing Accelerated Mobile Links
categories: 
    - development
excerpt: モバイルWeb全体が速くなりますように( ˘ω˘)ｽﾔｧ
---

マイブームのAMPネタ。AMPとはモバイルWebの爆速化プロジェクトですが、一応オープンソースプロジェクトということになってるが、いかんせんGoogleが主導しているわけで、Googleの検索結果ページから遷移するとそのメリットを最大限に享受できる。

- [Google Developers Japan: Accelerated Mobile Links のご紹介: モバイル ウェブアプリを高速に](https://developers-jp.googleblog.com/2017/01/introducing-accelerated-mobile-links-making-the-mobile-web-app-quick.html)

ちょっと限定的な印象だったわけだが、今回CloudflareさんもAMPに対応したサービスを出したってもんだから、Web全体にスピード貢献に期待できる。その名もAccelerated Mobile Links!!!

Cloudflareを利用しているサイト上で、AMP対応したURLがあると、Googleの検索結果ページ同様、先読みしAMPビューワーでチョッパヤに表示してくれる代物。

たしか、このブログも[SSL対応](https://t32k.me/mol/log/secure-and-fast-github-pages/)したときに、Cloudflareを利用した。というわけで、設定ページを見たら、あった！

![](/mol/images/2017/0124-00.png)

ENABLE ACCELERATED MOBILE LINKSをONにしましょう。

これで対応OK!

さて、以下のリンクはAMP対応しているURLだ。

- [メルカリ アッテ \- 手数料無料！なんでも募集できる地域コミュニティアプリ](https://www.mercariatte.com/jp/)

モバイルデバイスで閲覧すると、先頭にAMPマークがついてるのが分かる。これをクリックするとGoogleの検索結果じゃないにもかかわらず、AMPビューワーが立ち上がる。

<img src="/mol/images/2017/0124-01.gif" width="240" alt="">

```
https://www-mercariatte-com.amp.cloudflare.com/i/s/www.mercariatte.com/files/img/icon-app.svg
```

しかも、`*.cdn.ampproject.org`じゃなくて、`*.amp.cloudflare.com`からリソースが配信されている。Cloudflareさん太っ腹じゃないか。

というわけで、すでにCloudflareを利用しているサイトなら、とりあえず Accelerated Mobile Linksを有効にしといて損はないんじゃないかな。

もっと、他のパートナーも加わってモバイルWeb全体が速くなりますように( ˘ω˘)ｽﾔｧ

