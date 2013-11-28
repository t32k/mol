---
layout: post
title: peerDependency
categories: nodejs
status: publish
type: post
excerpt: "暮らし、安心、魔鎖狩あん♪"
---
grunt@0.4くらいから、package.jsonに`peerDependency`というキーを見かけるようになった。[Plugins - Grunt](http://gruntjs.com/plugins)でも
peerDependencyが指定されているプラグインに関しては、Grunt Version ~0.4.0のように出るので意味分かんないけど、とりあえず指定してた。

+ [Peer Dependencies](http://blog.nodejs.org/2013/02/07/peer-dependencies/)

で、コレ読んだら理解した。

```
├── request@2.12.0
└─┬ some-other-library@1.2.3
  └── request@1.9.9
```

例えば、こうゆう依存関係の状態があったとき、some-other-libraryのパッケージはrequestパッケージの2.x系で動作しなくても、自身が内包しているrequest@1.9.9を参照するので特に問題ない。これは現状の`dependency`で表現できる。

しかし、パッケージの中にはhostパッケージと呼ばれるものが登場してきた。例えてゆうなら、jQueryとjQueryプラグインのようなもので、あるjQueryプラグインがjQuey@1.xでしか動作しなければ、当然のごとくjQuey@2.xをhost側で読み込んでいたらこのプラグインは動かない。

これはクライアントサイドの話だが、これと同様のことがGruntとそのプラグインの関係にも当てはまる。あるgruntプラグインはgrunt@0.3.xで動かないけど、grunt@0.4.xでhostされていたら動くって場合は、こう表現する。

```
{
  "name": "grunt-hoge",
  "peerDependencies": {
    "grunt": "0.4.x"
    // "grunt": "~0.4.0"でも同義
  }
}
```

![dependenciespeerとDependencies](/mol/images/2013/11-28-fig.png)

今は0.4.xで落ち着いてるからとくに必要のない感じだけど、たぶんこれから0.5.xとかリリースされて0.4.xと混在した時に、peerDependenciesを指定しておくと以下の様なエラー表示してくれる。

```
npm ERR! peerinvalid The package flatiron does not satisfy its siblings' peerDependencies requirements!
npm ERR! peerinvalid Peer flatiron-cli-config@0.1.3 wants flatiron@~0.1.9
npm ERR! peerinvalid Peer flatiron-cli-users@0.1.4 wants flatiron@~0.3.0
```

ちなみに、peerDependenciesが指定されたgruntプラグインを`npm install`するとpeerDependenciesに指定したgrunt（パッケージ）も一緒に落ちてくる。

---

あ、そうそう、Gruntについては今週土曜の[HTML5カンファレンス](http://events.html5j.org/conference/2013/11/sessions)でも喋るよ。セッションはデザイナーさんとか、はじめてGruntを触るような人向けに喋るからpeerDependenciesとか気になる人は来なくていいよ！魔鎖狩投げたい人はahomuの方に行ってください。でも、人が来ないと寂しいので来てください。でも魔鎖狩こわいので来ないでください。でも来て（ry。。。