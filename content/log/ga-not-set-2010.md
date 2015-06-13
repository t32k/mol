---
date: 2010-09-30
title: Google Analytics、 (not set) エントリの異常増加
categories: analytics
excerpt: 最近、ユーザー > PC環境 > 画面の解像度 のメニューにおいて、 (not set) エントリが異常に多いことを同僚から指摘されました。
ogimage: http://t32k.me/static/blog/2010/09/screenresolution.png
---

最近、ユーザー > PC環境 > 画面の解像度 のメニューにおいて、 (not set) エントリが異常に多いことを同僚から指摘されました。調べてみると、一部のプロファイルでそのような現象を確認することが出来ました。

Google Analytics で (not set)  と言えば、[キャンペーントラッキングでのキーワード](http://analytics-ja.blogspot.ca/2010/02/not-set-entries.html)問題が有名ですね。キーワードが取れていないから (not set) であるので、画面の解像度 においても解像度が取れてないのだろうと考えましたが、全体の中で10％も (not set) というのは、ちょっとどうゆう状況なのか考えらませんでした。数件、数十件であれば、トラッキングコード実行時になんらかのエラーがあって取れないということも考えられるでしょうが、今回の場合は多すぎます。

![](http://t32k.me/static/blog/2010/09/screenresolution.png)

そこで、年次スパンで (not set) エントリの推移を見てみますと、どうやら5/3から急激に増加しているのが分かります。ということで、該当の期間にトラッキングコード、フィルタの変更を行ったかといえば、それも思い当たるふしがありません。

ということで、他のGAユーザーも同じ問題になっていないのか検索してみました。たいていは、アクセス解析Q＆Aフォーラムを調べれば分かるのですが、分からないこともあります。

そんなときは、[Google Analytics Help forum](https://productforums.google.com/forum/?hl=en#!forum/analytics)のほうを検索してみましょう。

+ [Huge increase in Screen Resolution/Colors of (Not Set) - Google Product Forums](https://productforums.google.com/forum/?hl=en#!category-topic/analytics/discuss-issues-related-to-your-accounts-reports-and-data/rg0H0aJal0o)

検索してみると、どうやら上記の質問と似ているように思えます。時期的にも同じだし、症状も似ている。この人は 画面の解像度 だけでなく、画面の色 でも (not set) エントリが出ているみたい。そこで、自分のプロファイルを再度確認したところ、画面の色 においても同じ現象が確認できました。その他にも(not set)  エントリの異常増加は、自分のプロファイルでは、下記メニューで確認できました。

+ 画面の解像度　（Screen Resolutions）
+ 画面の色　（Screen Colors）
+ フラッシュのバージョン　(Flash Versions）
+ 言語　（Languages）
+ ホスト名 （Hostnames） ※これは増加ではなく急激な減少でした。

そんわけでいろいろ調べた結果、なんかGA自体のバグくさいので、今回はGooogle さんに問い合わせてみようと思いました。実はちゃんとGoogle Analytics のお問い合わせフォームが存在してまして、調べてみてどうしてもわからない場合は問い合わせてみるのも良いでしょう。（要：AdWordsアカウント）

+ [Analytics Help](https://support.google.com/analytics/?rd=1#topic=3544906)

問い合わせた結果、この問題について既に認識しており、現在、エンジニアが問題の解決に向けて鋭意対応中ではあるが、改善時期は未定とのことです。

Google Analyticsでは、以前にもナビゲーション サマリーにおいて離脱数が0%になるバグが発生していました。（現在は修正済）　そういったバグは他にもあるかもしれませんので、こういった問題は僕らにはどうしようもできないことです。つまり、何を言いたいかと言いますと、バグ見つけたら記事にしてGoogleに問い合わせて共有しようぜってことです。3人よれば文殊の知恵ですがな。