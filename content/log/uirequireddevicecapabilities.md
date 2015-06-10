---
date: 2011-04-27
title: UIRequiredDeviceCapabilities
subtitle: 初リジェクトなう！
categories: development
excerpt: 初リジェクトなう！ってことでiPhone Appの申請しましたが、めでたくリジェクトされました。大好きなあの子にリジェクトされるのは勘弁願いたいものですが、Appleなら俺何度でもアタックするよ！
---

初リジェクトなう！ってことでiPhone Appの申請しましたが、めでたくリジェクトされました。大好きなあの子にリジェクトされるのは勘弁願いたいものですが、Appleなら俺何度でもアタックするよ！

その理由はAppleさん律儀なコでして、ちゃんとどこが嫌なのか言ってくれます。そこを修正してもう一度トライすればいいんですよ。

ってことで、今回は簡単に意訳すると、「テメーのアプリ、カメラ使うのにカメラが必要って書いてないじゃん！無理じゃん！！UIRequiredDeviceCapabilitiesでググッたらいいんじゃないの！？こんなサービスめったにしないんだからねっ！！！」ってな感じなことがリンゴちゃんの返答メールの行間から読み取れました。

はい、メチャいい子です。早速、UIRequiredDeviceCapabilitieでググってみるといっぱい出てきました。みんな必ずぶち当たる登竜門みたいなもんですかね。


> Key: UIRequiredDeviceCapabilities Xcode name: “Required device capabilities” Summary: Specifies the device-related features required for the application to run. See “UIRequiredDeviceCapabilities” for details. Availability: iOS 3.0 and later

はい、アイコンのテカリを無くしたい時にも出ててきましたね、Info.plistです。そのKeyにUIRequiredDeviceCapabilitieって書いて必要な機能埋めちゃいなよって書いてあります。

その機能のリストが以下です。いろいろありますなー。

+ telephony
+ wifi
+ sms
+ still-camera
+ auto-focus-camera
+ front-facing-camera
+ camera-flash
+ video-camera
+ accelerometer
+ gyroscope
+ location-services
+ gps
+ magnetometer
+ gamekit
+ microphone
+ opengles-1
+ opengles-2
+ armv6
+ armv7

今回のアプリでrequireな機能といえば、カメラ機能なのでstill-cameraを選択しました。スチールカメラね、写真撮る方のカメラね。

> Copy the info.plist to the root of your project and edit it from there. It will be copied over to the complied project from there. - [Any way to edit the UIRequiredDeviceCapabilities key in Info.plist? » Community Questions & Answers » Appcelerator Developer Center](http://developer.appcelerator.com/question/43711/any-way-to-edit-the-uirequireddevicecapabilities-key-in-infoplist)

んで、TItanium Mobile のプロジェクトフォルダの、`buid/iphone/Info.plist`をルートディレクトリにコピーして、そのファイルで`Required device capabilitie`の項目を作って必要な機能を記入してけばいいよ。2つも3つでも必要なだけ書けばいいお！

> To use a custom Info.plist, copy the Info.plist from the build/iphone folder. If this folder does not exist, run your application in the simulator once and it should be created automatically. You’ll want to copy the Info.plist file into the root directory of your project (at the same level as tiapp.xml). Whatever values are placed in your custom Info.plist will be used as-is by the Titanium compiler.

Info.plistをルートに持ってくるのは、そのままだとビルドするときに上書きしちゃって消えちゃうからしい。

> tiapps.xmlでrequires要素を用いて、デバイス機能によるインストール制限に対応した。(UIRequiredDeviceCapabilities) - [Titanium Mobile 1.6.0がリリースされました（速報→追記しました） - JP::HSJ::Junknews::HatenaSide](http://d.hatena.ne.jp/donayama/20110224/ti160released)

んなことしなくても、どうやらTitanium Mobile 1.6からはtiapp.xmlで指定するっぽい。

```xml
<iphone>
	<requires>
		<feature>still-camera</feature>
	</requires>
</iphone>
```

多分こんな感じでうまくいった、iphone要素なかにネストでrequires要素を作ってその中に必要なfeature(機能)を記述していく感じ。

はい、そんなこんなで再申請しました。今度は通るといいな。
