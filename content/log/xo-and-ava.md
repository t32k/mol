---
date: 2017-01-04
title: xoとavaでお手軽リント・テスト環境構築
categories: 
    - development
excerpt: できるかぎり開発環境構築に手間を取らず、アプリケーションのコードに集中したいものですな(˘ω˘)
ogimage: https://t32k.me/mol/images/2017/0104-01.png
---

元旦に[StyleStats v7.0](https://github.com/t32k/stylestats/releases/tag/v7.0.0)をリリースした。めでたいことだ（知らんけど）。バージョンアップ作業は例のごとく依存するnpm modulesをアップデートして終わりというのがt32kの伝家の宝刀だが、せっかくなので今回はES6に書き換えようと思った。

しかし、それも`function`をアロー関数に変更するぐらいだろうと、タカをくくっていたが、書き出してみると、[1000ch君パイセン](https://1000ch.net/)の~~煽り~~意識高いレビューコメントのおかげで、いろいろ勉強させてもらった、多謝( ˘ω˘)！

## ESLint

![ESlint](/mol/images/2017/0104-00.png)

- [ESLint \- Pluggable JavaScript linter](http://eslint.org/)

アロー関数に変更するだけってのもあれだから、ちゃんとESlintもES6用の設定にカスタマイズしようと思い必死こいて`.eslintrc`とにらめっこしていた。といっても下記の記事を参考にしただけだが。

- [ESLint 最初の一歩 \- Qiita](http://qiita.com/mysticatea/items/f523dab04a25f617c87d)

ESlintの仰せのままにコードを書き換えていく。書き終えたところで助言。

> .eslintrcメンテしていくのつらいから、xo使ったらどうですか？

タシ蟹！設定項目いっぱいあってめんどくさいです！しかし、xoってなんぞ( ˘ω˘)？

## xo: JavaScript happiness style linter

![xo](/mol/images/2017/0104-01.png)

- [sindresorhus/xo: ❤️ JavaScript happiness style linter](https://github.com/sindresorhus/xo)

いっぱいnpm作ってるかの有名な[sindresorhus](https://github.com/sindresorhus)氏のリンター。内部的にはESlintを使っていて、氏が思うESlintの設定でリントしてくれるというもの。なるほど検索しづらい！

僕みたいな、あまりJSにこだわりがない三等兵にとっては、こうゆう業界の先いってる人の考えを真似て従うのは性に合ってる。というかリントの設定で時間つぶしたくないもんね。

似たようなもので[feross/standard](https://github.com/feross/standard)がある。この圧倒的な名前の王道感のおかげが、こっちのほうが有名だ。ただこっちは**セミコロンなし**が既定のルールとなっている。さきほど、こだわりはないと言ったが、こだわりがないからこそ小さい頃に『JSはセミコロンを必ずつけろ！』と教わって生きてきたので敷かれたレールから外れるのがこわい。そうゆう人も多いのか、[Flet/semistandard](https://github.com/Flet/semistandard)というリンターもある。さっそくスタンダード分裂してんじゃねーか！と思ったのはいざ知らず。

xoのほうはセミコロンつけるな！とは言わないしログもきれい( ˘ω˘) ただ、デフォルトでインデントはタブというルールがある。これが気に食わない人は`package.json`に`xo`のフィールドを作って設定を変更できる。その他のいくつかの設定も`package.json`から変更できる。

```json
{
  "name": "awesome-package",
  "xo": {
    "spacce": true
  }
}
```

またスペース派だったけど、今回からタブ派に切り替えようかしらって思った人は`xo --fix`ですぐに対応できる。今まで使ってたESlintの設定よりもチョイ厳し目だが、全体的に納得感あるので気に入っている。

## ava: Futuristic JavaScript test runner

![ava](/mol/images/2017/0104-02.jpg)

- [avajs/ava: Futuristic JavaScript test runner](https://github.com/avajs/ava)

xoのドキュメントを読んでいるとavaという単語が目につく。同じsindresorhus氏作のテストランナーだ。自分で未来的って言っちゃうほどなんだから、新しい仕様が採用されているのだろうと思い、せっかくなのでxoと一緒にこっちも採用してみた。1000ch君パイセンも最近使ってると言ってたし。

以前までは[Mocha](https://mochajs.org/)を使用していたが、非同期のテストがしづらいというか、よくわかんないままやってた。avaはテストの実行自体も非同期にやってくれて早い。またPromiseをサポートしているので、`done()`とかいちいち呼び出さなくてもいい。

```js
test('Promiseを返す関数のテスト', t => {
    return somePromise().then(result => {
        t.is(result, 'おんなじあたい');
    });
});
```

ちょうど、`StyleStats#parse()`もPromiseを返すように変更したのでだいぶ楽に書けるようになった。と思っていたが、xoとavaを併用していると、上記のテストは『Async/Awaitを使えよー！』とxoに怒られる( ˘ω˘)

```js
test('Promiseを返す関数のテスト', async t => {
    const result = await somePromise();
    t.is(result, 'おんなじあたい');
});
```

言われたとおりにしたら、さらに見やすくなって感動した。

あとは、Mochaを使ってると`describe`や`it`といったグローバル変数を使うはめになって、ESlintで『そんなもん宣言されてないやんけ！』と怒られて、テストファイルだけ、その変数を除外するとかゆうめんどくさいことからも開放されてよい( ˘ω˘)

### nyc: the Istanbul command line interface

avaでコードのカバレッジを取るにあたって、[istanbul](https://github.com/gotwarlost/istanbul)は使えなくて、代わりにサブプロセスの[nyc](https://github.com/istanbuljs/nyc)というのを使うのだが、なんしかうまくいかない。

- [ava/code\-coverage\.md at master · avajs/ava](https://github.com/avajs/ava/blob/master/docs/recipes/code-coverage.md)

同じ設定・コードなのに、うまくいく時といかない時がある。よくわからないので寝て待つことにする。

## まとめ

最初のセットアップも`xo --init`、`ava --init`で出来るので楽ちんである。あとなんとかrcファイルもルートディレクトリに貯まらないのもいい（package.jsonは肥大化するが許容範囲だと思う...）。できるかぎり開発環境構築に手間を取らず、アプリケーションのコードに集中したいものですな( ˘ω˘)
