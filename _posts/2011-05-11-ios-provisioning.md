---
layout: post
title: Titanium MobileのKitchenSinkを実機(iPhone)にインストール
categories:
- Titanium Mobile
tags:
- iphone
status: publish
type: post
published: true
meta:
  pvc_views: '39900'
  _edit_last: '1'
  _aioseop_keywords: iphone, titanium mobile
  _aioseop_description: 上記サイトから行うのですが、いやはや全く意味不明です。自分が何のために今どのような作業をしているのか分からず、Web上の記事を参考にとりあえず前に進んだという状況だったので、それじゃいかんじゃろということで自分なりにまとめてみる。
---
KitchenSinkどうこうではなく、ほぼProvisioningに関するお話ですがお付き合いくださいませ。

あ、ちなみに私の環境はXcode 4 + Titanium Developer 1.2.2 + Titanium SDK 1.6.2です。

<img class="fig" title="iOS Provisioning Portal - Apple Developer" src="/static/blog/2011/05/ios.png" alt="iOS Provisioning Portal" width="470" height="240" />

iPhoneアプリ公開で一番手をこまねいた作業といえばプログラミングでもなくデザインでもなく、プロビジョニングです。アプリを実機にインストールするのにもプロビジョニングファイルの作成が必須です。
<ul>
	<li><strong><a href="https://developer.apple.com/ios/manage/overview/index.action"> iOS Provisioning Portal - Apple Developer </a></strong></li>
</ul>
上記サイトから行うのですが、いやはや全く意味不明です。自分が何のために今どのような作業をしているのか分からず、Web上の記事を参考にとりあえず前に進んだという状況だったので、それじゃいかんじゃろということで自分なりにまとめて理解してみる。

<!--more-->

まずは、ぷろびじょにんぐってなんやねん？ってとこから、Wikipediaさんには以下のように書いてある。
<blockquote>プロビジョニング（英: Provisioning）は、本来は「準備、提供」などの意味であり、現在では通常、音声通信やコンピュータなどの分野における、ユーザーや顧客へのサービス提供の仕組みを指す。</blockquote>
はい、意味がわかりません。もうちょっと読み進めるとそれっぽいことが書いてありました。
<blockquote>ユーザ・プロビジョニングとは、1つまたは複数のシステムやディレクトリやアプリケーションにおいて、ユーザアカウントの生成・保守・削除などを行うこと</blockquote>
ははーん、つまり、iOS Provisioning Portalってとこはユーザーのアカウントとアプリの設定を管理するとこなのね、OK、余裕。

てことで、iOS Provisioning Portalはだいたい以下の4つのメニューから構成されています。
<ol>
	<li><a href="#certificates"><strong>Certificates（証明書の取得）</strong></a></li>
	<li><strong><a href="#devices">Devices（デバイスの登録）</a></strong></li>
	<li><strong><a href="#appids">App IDs（App IDの登録）</a></strong></li>
	<li><strong><a href="#provisioning">Provisioning（プロビジョニングファイルの作成）</a></strong></li>
</ol>
では、Titanium Mobile でKitchenSinkのアプリを実機に転送するまでをやってみましょう。
<h2 id="certificates">Certificates</h2>
まずは証明書の取得。証明書は開発用とアプリ公開用の2種類があります。
<ul>
	<li>Development Certificates（開発用）</li>
	<li>Distribution Certificate（アプリ公開用）</li>
</ul>
DevelopmentもDistributionも基本同じ手順なので安心してください。今回はDevelopment用の証明書を作成します。

<a href="/static/blog/2011/05/keychain01.png"><img class="fig" title="キーチェーンアクセス" src="/static/blog/2011/05/keychain01.png" alt="" width="470" height="281" /></a>
<ol>
	<li>キーチェーンアクセス.appを立ち上げる</li>
	<li>証明書アシスタント &gt; <strong>認証局に証明証を要求...</strong>をクリック</li>
	<li>ユーザーのメールアドレス：<strong>Apple Developer Centerで登録したアドレス</strong>
通称：<strong>Apple Developer Centerで登録した名前</strong>
CAのメールアドレス：<strong>無記入</strong>
要求の処理：<strong>ディスクに保存</strong>、鍵<strong>ペア情報を指</strong>定にチェック</li>
	<li>ファイルを適当な保存場所に指定</li>
	<li>鍵のサイズ：<strong>2048ビット</strong>
アルゴリズム：<strong>RSA </strong></li>
	<li>できたCertificateSigningRequest.certSigningRequestを<a href="https://developer.apple.com/ios/manage/certificates/team/index.action  ">Certificates - iOS Provisioning Portal</a>にSubmit</li>
	<li>送信すると状態がpendingになるのでリロードして証明書をダウンロード</li>
	<li>
<blockquote>*If you do not have the WWDR intermediate certificate installed, <span style="text-decoration: underline;">click here to download now</span></blockquote>
って小さく書かれているリンクからAppleのデベロッパー証明書もついでにダウンロード</li>
</ol>
で、以下の2ファイルが取得できてダブルクリックすると晴れて証明書がインストールされます。
<ul>
	<li>AppleWWDRCA.cer （Apple World Wide Developer Relations Certification Authority）</li>
	<li>developer_identity.cer （iPhone Developer: USER_NAME）</li>
</ul>
タブが違うだけでDistributionも同じ手順でOKだよ(・∀・)ｽﾝｽﾝｽｰﾝ♪
<h3>複数のMacで開発を行いたい場合</h3>
はい、ちょっと話はそれます。私はMac miniとMacBook Airを持ってまして両方の機器で作業したいわけです。そんなときは片方の機器で作成した証明書（developer_identity.cer）をクリックしても鍵が合わないのでうまく認識してくれません。そこで個人情報交換（Personal Information Exchange）フォーマットで書き出す必要がでてきます。

<a href="/static/blog/2011/05/keychain02.png"><img class="fig" title="キーチェーンアクセス.app" src="/static/blog/2011/05/keychain02.png" alt="キーチェーンアクセス.app" width="470" height="182" /></a>

キーチェーンアクセス.appを立ち上げで、iPhone Developer: USER_NAMEの証明書を選択、右クリックして、<strong><em>証明書</em>を書き出す</strong>を選択する。

<a href="/static/blog/2011/05/keychain03.png"><img class="fig" title="個人情報交換(.p12)" src="/static/blog/2011/05/keychain03.png" alt="個人情報交換(.p12)" width="470" height="180" /></a>

個人情報交換(.p12)を選択して保存。そして開発したいMacに持って行きダブルクリックしてインストール完了です。これで、複数台でのアプリケーション開発が可能となりました。

詳しくは下記参照。
<ul>
	<li><a href="http://d.hatena.ne.jp/paella/20090218/1234948743">1アカウントのみで出来る、iPhoneアプリの開発を複数台のMacで行う方法 - Ni chicha, ni limona</a></li>
</ul>
<h2 id="devices">Devices</h2>
次はテストしたいデバイスの登録です。これは簡単です。

<a href="/static/blog/2011/05/organizer.png"><img class="fig" title="Organizer" src="/static/blog/2011/05/organizer.png" alt="" width="470" /></a>

iPhoneをMacに繋げて、XcodeのOrganizerを立ち上げて、<strong>Identifier</strong>の部分をメモっておきましょう。
<ul>
	<li><a href="http://developer.apple.com/ios/manage/devices/index.action">Devices - iOS Provisioning Portal - Apple Developer </a></li>
</ul>
上記ページからAdd Devicesをクリックして、<strong>Device Name</strong>にあなたの持ってるiPhone/iPod/iPadなど区別できる名前をつけて、<strong>Device ID (40 hex characters)</strong>に先ほどメモっておいた<strong>Identifier</strong>をコピペしSubmitボタンを押せばデバイスの登録完了です。ちなみに登録できるデバイスは100個までです。
<h2 id="appids">App IDs</h2>
はい、ここ重要です！テストに出ます！！ってことで、なんでこのパートが重要かと言いますと、これまでの証明書もデバイスも間違えて登録してしまったら削除してやり直せばいいんですけど、このApp IDはそれができません。つまり、あなたが出来心で作ったunkoといった名前のApp IDはずっと残ります。消せません。

てことで、慎重にやっていきましょう。
<ul>
	<li><a href="http://developer.apple.com/ios/manage/bundles/index.action">App IDs - iOS Provisioning Portal - Apple Developer </a></li>
</ul>
上記ページからNew App IDをクリックして、項目を埋めていきます。

<a href="/static/blog/2011/05/create-app-id.png"><img class="fig" title="Create App ID" src="/static/blog/2011/05/create-app-id.png" alt="Create App ID" width="470" /></a>
<ol>
	<li><strong>Description</strong>
App IDの名前（説明文）です。</li>
	<li><strong>Bundle Seed ID (App ID Prefix)</strong>
新しく作るので、<strong>Generate New</strong> を選択します。</li>
	<li><strong>Bundle Identifier (App ID Suffix)</strong>
例にあるように、ドメインを逆から記入スタイルが推奨されてるっぽいです。
ということで、私はとりあえず、 <strong>me.t32k.development </strong>にしました。</li>
</ol>
<blockquote>そこで，App IDを「*」とすることでどのようなBundle Identifierを持つアプリでも動作させることができるようになります。
<span style="font-size: x-small;"><a href="http://gihyo.jp/dev/serial/01/iphone/0009">目指せ！iPhoneアプリ開発エキスパート：第9回　デバイスでアプリを動かす｜gihyo.jp</a></span></blockquote>
上記ページには*アスタリスク使うといいぜ！って書いてあるのですが、実際にアスタリスクでやると、注意（Game Center使えないよ）っぽいこと言われるので、げんなりします。（下記図参照）

<a href="/static/blog/2011/05/App-IDs.png"><img class="fig" title="App IDs" src="/static/blog/2011/05/App-IDs.png" alt="App IDs" width="470" /></a>

てことで、Submit押せばApp IDの登録完了です。
<h2 id="provisioning">Provisioning</h2>
<a href="/static/blog/2011/05/flow.png"><img class="fig" title="flow" src="/static/blog/2011/05/flow.png" alt="" width="470" height="123" /></a>

ようやく最後のプロビジョニングファイルの作成です。プロビジョニングファイルっていうのはこれまで登録した情報（証明書、デバイス、App ID）を組み合わせて作成するもんです。下記のような感じですね。

<strong>開発用 Provisoning File </strong>
= Development Certificate + Device ID + App ID

<strong>公開用 Provisoning File </strong>
= Distribution Certificate + App ID

要はこんなめんどくさいことをして、不正な経路でのアプリケーションのインストールを防止してるっちゅう話です。

はい、では下記ページNew Profileをクリックして、項目を埋めていきます。
<ul>
	<li><a href="http://developer.apple.com/ios/manage/provisioningprofiles/index.action">Provisioning Profiles - iOS Provisioning Portal - Apple Developer </a></li>
</ul>
<a href="/static/blog/2011/05/Create-iOS-Development-Provisioning-Profile.png"><img class="fig" title="Create iOS Development Provisioning Profile" src="/static/blog/2011/05/Create-iOS-Development-Provisioning-Profile.png" alt="Create iOS Development Provisioning Profile" width="470" /></a>
<ol>
	<li>Profile Name：適当に</li>
	<li>Certificates：チェックを付ける</li>
	<li>App ID：選択する</li>
	<li>Devices：チェックを付ける</li>
</ol>
Submitボタンを押せばプロビジョニングファイルの完成です。ダウンロードしてダブルクリックでXcodeにインストールしましょう。
<h2 id="runondevice">Run on Device</h2>
実機にインストールする前に、<strong><a href="https://github.com/appcelerator/KitchenSink">KitchenSinkをGitHubよりダウンロード</a></strong>して、プロジェクトをインポートしておきましょう。ちなみにKitchenSinkってゆうのはTitaniumの機能を全部載っけた見本アプリのようなものです。これを動かしてどのような動きをするのか確認して、パクリたいとこはソースを見てパクるという教科書みたいなものです。

<a href="/static/blog/2011/05/run_on-device.png"><img class="fig" title="Run on Device" src="/static/blog/2011/05/run_on-device.png" alt="Run on Device" width="470" /></a>

はい、Titanium Developerをインスコした当初のRun on Deviceタブはこんな感じで、iOSプログラムに登録しろよーとかAppleから証明書もらってこいよーとか言われてるんですけども、プロビジョニングファイルを作成し終わればほとんどが埋まってしまいます。あとは、最後の項目にダウンロードをしてきたプロビジョニングファイルをUploadするだけです。

Uploadが終われば、Install Now!!!!!!!!!!!!ってことでiTunes経由でアプリがインストールされます。

ほらね、簡単でしょ？

<a title="DSC05392 by t32k, on Flickr" href="http://www.flickr.com/photos/t32k/5707451600/"><img class="fig" title="KitchenShink" src="http://farm4.static.flickr.com/3005/5707451600_1725439671.jpg" alt="KitchenShink" width="470" /></a>

ってことでみんなもれっつたいたん！
