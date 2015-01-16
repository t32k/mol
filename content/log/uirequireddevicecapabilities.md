---
date: 2011-04-27
title: UIRequiredDeviceCapabilities
categories: memo
---
<img class="alignnone size-full wp-image-2988" title="still-camera" src="/static/blog/2011/04/still-camera.png" alt="still-camera" width="470" height="105" />

初リジェクトなう！ってことでiPhone Appの申請しましたが、めでたくリジェクトされました。大好きなあの子にリジェクトされるのは勘弁願いたいものですが、Appleなら俺何度でもアタックするよ！

その理由はAppleさん律儀なコでして、ちゃんとどこが嫌なのか言ってくれます。そこを修正してもう一度トライすればいいんですよ。

<!--more-->

ってことで、今回は簡単に意訳すると、「テメーのアプリ、カメラ使うのにカメラが必要って書いてないじゃん！無理じゃん！！UIRequiredDeviceCapabilitiesでググッたらいいんじゃないの！？こんなサービスめったにしないんだからねっ！！！」ってな感じなことがrりんごちゃんの返答メールの行間から読み取れました。

はい、メチャいい子です。早速、UIRequiredDeviceCapabilitieでググってみるといっぱい出てきました。みんな必ずぶち当たる登竜門みたいなもんですかね。
<blockquote><span style="color: #000000;">Key: </span>UIRequiredDeviceCapabilities
<span style="color: #000000;">Xcode name: </span>"Required device capabilities”
<span style="color: #000000;">Summary: </span>Specifies the device-related features required for the application to run. See “UIRequiredDeviceCapabilities” for details.
<span style="color: #000000;">Availability: </span>iOS 3.0 and later

<span style="font-size: x-small;"><a href="http://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/iPhoneOSKeys.html">Information Property List Key Reference</a></span></blockquote>
はい、<a href="http://t32k.me/mol/log/ios-prerendered-icon/">アイコンのテカリを無くしたい時にも出ててきましたね</a>、Info.plistです。そのKeyにUIRequiredDeviceCapabilitieって書いて必要な機能埋めちゃいなよって書いてあります。

その機能のリストが以下です。いろいろありますなー。

<strong><a href="http://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/iPhoneOSKeys.html#//apple_ref/doc/uid/TP40009252-SW3">Dictionary keys for the UIRequiredDeviceCapabilities key</a></strong>
<ul>
	<li>telephony</li>
	<li>wifi</li>
	<li>sms</li>
	<li>still-camera</li>
	<li>auto-focus-camera</li>
	<li>front-facing-camera</li>
	<li>camera-flash</li>
	<li>video-camera</li>
	<li>accelerometer</li>
	<li>gyroscope</li>
	<li>location-services</li>
	<li>gps</li>
	<li>magnetometer</li>
	<li>gamekit</li>
	<li>microphone</li>
	<li>opengles-1</li>
	<li>opengles-2</li>
	<li>armv6</li>
	<li>armv7</li>
</ul>
今回のアプリでrequireな機能といえば、カメラ機能なのでstill-cameraを選択しました。スチールカメラね、写真撮る方のカメラね。
<blockquote>Copy the info.plist to the root of your project and edit it from there. It will be copied over to the complied project from there.

<span style="font-size: x-small;"><a href="http://developer.appcelerator.com/question/43711/any-way-to-edit-the-uirequireddevicecapabilities-key-in-infoplist">Appcelerator Developer Center - Any way to edit the UIRequiredDeviceCapabilities key in Info.plist?</a></span></blockquote>

<img class="fig" title="UIRequiredDeviceCapabilitie" src="/static/blog/2011/04/UIRequiredDeviceCapabilitie.png" alt="Required device capabilitie" width="470" height="108" />

んで、TItanium Mobile のプロジェクトフォルダの、buid/iphone/Info.plistをルートディレクトリにコピーして、そのファイルでRequired device capabilitieの項目を作って必要な機能を記入してけばいいよ。2つも3つでも必要なだけ書けばいいお！

<blockquote>Custom Info.plist

To use a custom Info.plist, copy the Info.plist from the build/iphone folder. If this folder does not exist, run your application in the simulator once and it should be created automatically. You'll want to copy the Info.plist file into the root directory of your project (at the same level as tiapp.xml). Whatever values are placed in your custom Info.plist will be used as-is by the Titanium compiler.

<span style="font-size: x-small;"><a href="http://wiki.appcelerator.org/display/guides/The+Application+Project+Structure#TheApplicationProjectStructure-CustomInfo.plist">The Application Project Structure - Documentation Guides - Appcelerator Wiki</a></span></blockquote>
Info.plistをルートに持ってくるのは、そのままだとビルドするときに上書きしちゃって消えちゃうからしい。

<blockquote>tiapps.xmlでrequires要素を用いて、デバイス機能によるインストール制限に対応した。(UIRequiredDeviceCapabilities)

<span style="font-size: x-small;"><a href="http://d.hatena.ne.jp/donayama/20110224/ti160released ">Titanium Mobile 1.6.0がリリースされました - JP::HSJ::Junknews::HatenaSide</a></span></blockquote>
んなことしなくても、どうやらTitanium Mobile 1.6からはtiapp.xmlで指定するっぽい。

[xml]
&lt;iphone&gt;
　&lt;requires&gt;
　　&lt;feature&gt;still-camera&lt;/feature&gt;
　&lt;/requires&gt;
&lt;/iphone&gt;
[/xml]

多分こんな感じでうまくいった、iphone要素なかにネストでrequires要素を作ってその中に必要なfeature(機能)を記述していく感じ。

はい、そんなこんなで再申請しました。今度は通るといいな。
