---
date: 2018-08-23
title: AfterEffects-Bodymovin-Lottie-Vueを使ってみる
subtitle: 
categories: 
    - development
excerpt: After EffectsでBodymovinでちょちょいのちょいですよ！
ogimage: https://t32k.me//mol/images/2018/0824-00.png
---

最近、[Vue.js](https://jp.vuejs.org/)を触っている。そんで、UIデザインは外注していて、アニメーションの納品はどうしますか？と聞かれたので、聞きかじった程度の知識で「After EffectsでBodymovinでちょちょいのちょいですよ！」とテキトーに答えてしまって、後に引けない感じになったので実際に触ってみることにした。

## After Effects

ご存知の通り、Adobe製品。モーショングラフィックとか作るときに用いるツール。Adobe Premiere Proというのもあるが、こちらは動画編集メインで、今回のような込みいった短めのアニメーションなど制作するのはAfter Effectsが適している。

かくゆう、私も大学生の頃、VJというものに興味があり、本ツール（v5.5くらいかな？）使い、いろいろモーショングラフィックを作成していたものだ。そして今回一万と二千年ぶりにAfter Effects開いて触ってみる。

![](/mol/images/2018/0824-00.png)

せっかくなので、会社のロゴアニメーションを作ってみた。画面構成的にはコンポジションって箱を作ってそんなかでワチャワチャ下のタイムラインで動かす。右にエフェクトがあるのでイケイケにする。

要は、レイヤーごとにタイムラインで各オブジェクトを操作できるので込み入ったアニメーションも作りやすいということ。

![](/mol/images/2018/0824-01.gif)

- [アフターエフェクトでPS4の文字が描かれる文字書きアニメーションの作り方 \- YouTube](https://www.youtube.com/watch?v=GpwyPFR_ryc)

で、できたのがドーン！上記のYouTubeを見ながら簡単にできた。あと上記の画像はアニGIFなんだけど、After Effectsから直でアニメーションGIF書き出せないのね。書き出したかったら、[GifGun](https://www.flashbackj.com/aescripts/gifgun/)というAEスクリプトを購入しなければならない。

だもんで、まずはMOV（動画）で書き出して、それをPhotoshopで開いてアニメーションGIFに書き出す（めんどくさ）。

## Bodymovin

アニGIFに書き出しては旧態依然の体たらくぶりなので、今回はBodymovinを使用してみる。

- [Bodymovin](https://www.adobeexchange.com/creativecloud.details.12557.html)

BodymovinはAfter Effectsのスクリプトで、これをインストールすると作成した動画をJSON形式で保存することができる。いろいろインストール方法はあるみたいだが、僕はAdobeストアからインストールすればCreative Cloud Desktop Appが勝手にやってくれた。

![](/mol/images/2018/0824-02.png)

んで、インスコが終わったらメニューの `ウィンドウ > 拡張機能 > Bodymovin` を開くと上記のようなパネルが出てくる。保存先のパスを設定して、Renderボタンを押そう。

![](/mol/images/2018/0824-03.png)

たぶん、そのままだとエラーが出るので、環境設定から**スクリプトによるファイルへの書き込みとネットワークへのアクセスを許可**にチェック入れとこう。

```
{"v":"5.1.16","fr":29.9700012207031,"ip":0,"op":90.0000036657751,"w":1280,"h":720,"nm":"Logo Animation","ddd":0,"assets":[{"id":"image_0","w":1280,"h":720,"u":"","p":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABQAAAALQCAYAAADPfd1WAAAgAEl...
```

そうすると、こういったJSONファイルができるので、各クライアントに実装するエンジニアさんに渡そう！

## Lottie Web

JSONファイル自体はただの文字列なので、これをアニメーションとして、Webブラウザ上で動かしたい。そうするためにはLottieというライブラリを使用してJSONをパースする必要がある。

- [Render After Effects animations natively on Web, Android and iOS, and React Native\.](https://github.com/airbnb/lottie-web)

ちょっとややこしかったのだけど、ちょっと前まではこのLottieのライブラリ名も[bodymovin.js](https://cdnjs.com/libraries/bodymovin)と言ってたらしくて、bodymovinがごっちゃになってた。

- [chenqingspring/vue\-lottie: Render After Effects animations on Vue based on Bodymovin](https://github.com/chenqingspring/vue-lottie)

VueアプリでこのLottieを使いたいので、vue-lottieという便利なラッパーがあるので使用する。

![](/mol/images/2018/0824-04.gif)

まぁー、ドキュメント通りやればできた。なんか、アニメーションのタイミングがバラバラだけど（たぶんAEの作り方が悪いのだと思う）、力尽きた。一応、再生できてるので良い。

- [LottieFiles \- Free animation files build for Lottie, Bodymovin](https://www.lottiefiles.com/)

今回はロゴアニメーションで、まぁよくわからない使い道だけど、LottieFilesというサイトには実用的なアイコンアニメーションがいっぱいある。しかもJSONファイルで落とせるのですく使える。またアニGIFと違い、Lottieは再生と停止がコントロールできるので、用法用量を守って正しく使えばアプリのルック・アンド・フィールの向上につながるのではないだろうか。

というわけで、あやふやな知識だったけどすっきりした。今後はAfter Effectsも触っていきたい。