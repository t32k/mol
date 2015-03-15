---
date: 2011-06-22
title: Version Number (iTunes Connect) と Bundle version (CFBundleVersion)
subtitle: バージョン番号ではまるの巻
categories: development
excerpt: 前出したバージョンより、CFBundleVersionが低いからダメってことよね？1.2から1.2.1ってどーみても上がってんじゃん！てめぇ数字数えられねーのかよ!?てことで調べてみた。
ogimage: http://t32k.me/static/blog/2011/06/itunes.png
---

こないだ[Nyars](/mol/log/nyars/)のバージョンを1.2から1.2.1にアップデートした。アップデート理由は文言修正など細かな修正だったので1.0, 1.1, 1.2 ときたバージョンアップだが、今回はマイナーアップデートてことで、1.2.1にして申請を出してみた。

だがしかし、拒否られた。

> The binary you uploaded was invalid. The key CFBundleVersion in the Info.plist file must contain a higher version than that of the previously uploaded version.

前、申請したバージョンよりCFBundleVersionが低いからダメってことよね？1.2から1.2.1ってどーみても上がってんじゃん！てめぇ、数字も数えられねーのかよ!てことで調べてみた。

## Version (tiapp.xml)

![Titanium Developer](http://t32k.me/static/blog/2011/06/tidev.png)

バージョンに関して記入するところと言えば、Titanium Developer 1.2.2では上図。

![Titanium Studio](http://t32k.me/static/blog/2011/06/tistudio.png)

Titanium Studioでは上図。

```
<version>1.0</version>
```

この部分がtiapp.xmlに反映されるわけ。


## Bundle version (CFBundleVersion)

![Xcode](http://t32k.me/static/blog/2011/06/info.png)

前述のtiapp.xmlの内容が、`/APPLICATION_PROJECT/build/iphone/Info.plist` のBundle version (CFBundleVersion) に反映される。通常のテキストエディタでInfo.plistを開いてみると、

```
<key>CFBundleVersion</key> <string>1.0</string>
```

こんな感じになってるかと思う。試しにテストアプリを作ってバージョンはどの段階においても1.0だ。問題ない。

## Build Number

はい、でこのアプリを実機にインストールもしくはパッケージ化し、Info.plistのBundle Versionを確認してみよう。なんということでしょう。こんなんになってた！

```
1.0.1308740503
```

1.0以降に変な数字でてるやないですか！たぶんこれ__Build Number__ってゆうやつだと思われる（なんかググってみてそんな感じのようなことが書かれてた）。これがなんか勝手に生成されるようだ。

ってことで、今回のNyarsマイナーアップデート申請がなぜ却下されたのか考えてみると、前回のバージョンが1.2で今回出したバージョンが1.2.1てことで、それらにBuild Numberをくっつけたのを比較してみますと、

```
1.2.BUILD_NUMBER
1.2.1.BUILD_NUMBER
```

ってことなので、3番目の値で比較（Build Numberと1）され却下されたのではないかと結論づけた。


## Version Number (iTunes Connect)


![iTunes Connect](http://t32k.me/static/blog/2011/06/itunes.png)

ということで今回は、1.2.0って最初から出しとけば問題なかったわけですな。けどもVersion1.2.0でたぜ！ってゆうのもアレだと思った方、心配ご無用。CFBundleVersionはいわゆる内部バージョン番号みたいなものなので、iTunes Connect（お店に並ぶときのバージョン）に出すのは別でよいので、そこは1.2って提出しとこう。

Windows7の内部的なバージョン番号が 6.1のようなものだろう。てことで、今回僕は、1.2.1では通らなかったのでCFBundleVersionは1.3.0で提出してiTunes Conectには1.2.1を提出して無事アップデートできました。

めでたしめでたし。めんどくさかったらこの人みたいに最初から整数値でアップデートしていくのも手かと。

+ [viva Cocoa / Cocoa GUI App no.10](http://vivacocoa.jp/cocoaApp/cocoaApp10.cgi)

参考：

+ [Basuke's Blog: AppStoreのバージョン番号ではまる](http://basuke.blogspot.ca/2010/02/appstore.html)
+ [Versioning Mac OS X Applications Best Practicies - Dave Dribin's Blog](http://www.dribin.org/dave/blog/archives/2006/08/02/versioning_os_x_apps/)

