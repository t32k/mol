---
date: 2011-03-29
title: iOS Developer Programに登録!!!!
categories: 
    - development
---

![](/static/blog/2011/03/activationcode.png)

有料プログラム的な意味でってことです。初めに言っておきますが、これかなりの無理ゲーですわ...

せっかく、Titanium MobileでiPhone App制作するんだから、iPhoneっぽいことしたいよねってことでカメラ使いたい！カメラ使いたい！そうゆうわけで、カメラの動作はiOSシュミレーター上ではできませんから、iOS Developer Programの有料登録をして、作ったアプリを実機に転送できるようにしてもらわないといけません。たったそれだけの願いです。たったそれだけのためにかれこれ2週間はかかりました。

基本的に実機に転送する手順は以下の2つの記事を見てもらえればたぶん大丈夫だとおもう。

	- <a href="http://gihyo.jp/dev/serial/01/iphone/0009">目指せ！iPhoneアプリ開発エキスパート：第9回　デバイスでアプリを動かす｜gihyo.jp </a>
	- <a href="http://kentaro-shimizu.com/lecture/iphone/step3.html">iPhoneアプリを実機で動かす | iPhoneアプリ</a>

問題なのは登録です！
> な…　何を言ってるのか　わからねーと思うが
おれも何をされたのかわからなかった…

ってことで、ここから登録してみるよ。

	- <a href="http://developer.apple.com/jp/programs/ios/">iOS Developer Program - Apple Developer</a>


## 1順目

無料のApple Developerは以前に登録していたので
> Existing Apple Developer

I'm registered as a developer with Apple and would like to enroll in a paid Apple Developer Program.

を選んで individualで登録。AppleStoreでiOS DeveloperProgramを購入して、Activation Codeが記載されたメールをもらう。そこからActivation Codeが認証されて、晴れてDeveloperProgramに登録となるのですが、なんせ、いかにも、はたまた、どうしてか、Activation Code認証の時にエラーになります。

で、ちょっとググッてみるとこんな記事が。
> ※エラーが発生し、アクティベーションできない可能性大。ほとんどの場合、アカウント情報の文字化けが原因なのでADCのサポートにメールでアクティベーションできない旨を連絡する（リージョンを日本語にすれば日本語のメールで問題なし）
<span style="font-size: x-small;"><a href="http://ameblo.jp/mbdev/entry-10186919672.html"> iPhone Developer Programへの参加｜iPhone 開発雑記帳</a></span>

なんとまぁー。たしかに、最初にDeveloper登録したときに漢字で入力してた！急いでManage Accountで英語表記に直すが、肝心の氏名の部分が修正できない！あれ？詰んだ？

ということで、エラーはあいかわらず出るので、エラーが出たときに案内されるところからヘルプミーする。日本語で送っても大丈夫そうなので問題ない。

1週間経過しても、メール帰ってこない。（3週間くらいしたら返答来ました！）

## 2順目

待ちきれなかったので、今度は新規アカウント作成し最初から英語で全部入力する。お！なんかいけそうな感じ。iOS DeveloperProgramを購入して、再度Activation Codeのメールを待つ。

恐る恐る、Activation Codeを入力するとまたエラー
> **We are unable to activate your Apple Developer Programmembership.**
We are unable to activate your Apple Developer Programmembership because we are unable to successfully verifyyour identity. Please contact us and reference EnrollmentID# xxxxxxx  for further assistance.

でも今度は、エラーの内容違う。なんかお前の身元が認証できないみたいなこと言ってるのね。iOS Developer Centerにも公的な証明書のコピーをアメリカにFAXしてくれみたいなこと書いてある。そんな言われたってアメリカにFAXなんてちょっと。。ねぇ。めんどくさすぎますよね。

	- <a href="http://d.hatena.ne.jp/thata/20100404/1270370400">iPhone Developer Programへの入会がProgram Activation On Holdで完了しない件 - ちくわプログラマにっき</a>

でも、ここ見たら問い合わせしたらFax送らずに済むみたい。でも前回のメールの返答もないしな。とりあえず、「Fax送らずに済む方法を教えてください」って問い合わせのメールも送っておく。

## 3順目

ちょっと時間的に余裕がなくなってきたので、自分なりに推測してみる。身元が認証できないのはクレジットの個人情報が日本語なのに対して（iOS Developer Programはクレジット支払いで購入）、AppleのDeveloperに登録した情報は英語だから認証できないのでは？と思ったので、氏名以外を日本語に修正して再度購入してみる！Activation来る！エラー！！！ orz.............

もう、待ってられないので、電話してみる。

	- **<a href="http://developer.apple.com/jp/contact/phone.html">Worldwide Telephone Support - Apple Developer</a> **

アジアパシフィック/日本の言語に日本語って書いてあるから大丈夫だろうと思い、TEL！案外待たされずでた！

おれ：用件伝える！

あぽー：Apple ID 教えて！

あぽー：修正しといたよ！

おれ：ハヤッ！！

ってことで無事Activation Codeが認証されました。あとは、最初にあげた２つの記事見ながら実機に転送するだけす。

## 結論

Activation Codeでつまづいたら、すぐにコールコール♪ 絶対エラー起きる無理ゲーみたいなもんですから。

[追記] Activation Codeが認証されなくてもActivation Codeが発行された時点でクレジット課金されます。なので、今回僕は3回発行したので3万円請求されましたが、サポートセンターに電話すればキャンセル（返金）してくれます。
