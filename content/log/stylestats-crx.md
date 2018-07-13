---
date: 2016-02-01
title: StyleStatsのChrome拡張機能を作った
categories: 
    - css
    - development
excerpt: StyleStatsはCSSを解析してスタイルの各種指標を表示してくれるnpmだ。それを簡単にChrome拡張から利用できるようにした。調べたいページで右上のボタンを押すと新規タブで結果が出る。実に簡単だ。
ogimage: https://t32k.me/mol/images/2016/0120-01.png
---

[![StyleStats Chrome拡張機能](/mol/images/2016/0120-00.gif)](https://chrome.google.com/webstore/detail/stylestats/lgbcioahebkgkdiljpgcdaghejijioki)

StyleStatsのChrome拡張を作った。

+ **[StyleStats - Chrome ウェブストア](https://chrome.google.com/webstore/detail/stylestats/lgbcioahebkgkdiljpgcdaghejijioki)**

[StyleStats](https://github.com/t32k/stylestats)はCSSを解析してスタイルの各種指標を表示してくれるnpmだ。それを簡単にChrome拡張から利用できるようにした。調べたいページで右上のボタンを押すと新規タブで結果が出る。実に簡単だ。

## これまでの流れ

### CLI

![Commandline](/mol/images/2016/0120-00.png)

```shell
$ npm install -g stylestats
```

[npm](https://www.npmjs.com/package/stylestats)からインストールしてコマンドラインで使うのが一番やれることが多い。ローカルのファイルも解析できるし、それこそProgrammaticallyに自分でハックして、独自のレポートとかもできる。まぁ黒い画面に不慣れ人はちょっとあれかもしれない。

### Web

![StyleStats.org](/mol/images/2016/0120-01.png)

そうゆうわけで、もっとライトに使ってもらおうとWeb版も作った。CLIと違って、`Unique Font Families`、　`Unique Colors` がプレビューできたり、円グラフやタイムラインチャートなどグラフ機能を充実している。一つ一つのテスト結果にパーマリンクができるので、CSSといえどデータを残したくないって人はアレかもしれない。

あとParse.comがサービスを終了するということで、StyleStatsのWebもがっつりテスト結果保存に使用していたので、寝耳に水だった。まぁ1年あることだし、BaaS自体やめて普通にMongoDBとか使ってみるのも良いかもしれない。Herokuでやってることだし。

### CRX

![Chrome Extension](/mol/images/2016/0120-02.png)

そうゆうわけで、ライトに使えつつサーバーにデータを預けたくないって人向けにChrome拡張を今回作った。`Unique Font Sizes`もプレビュー可能になった。


## 使った技術とか

### ES2015

当たり前だけど、Chrome拡張なのでクロスブラウザ対応は気にしなくてよいし、現時点でChromeが対応しているESの機能ならBabelしなくてもそのまま使える。バベる環境作るのめんどいし、楽だよね。

### Promise + Fetch API + Arrow functions 

```js
Promise.all(links.map(link =>
  fetch(link.href, {mode: 'cors'}).then(response => response.text())
))
.then(texts => {});
```

ということで、`<link rel="stylesheet" href="/stylesheet.css">`要素を見つけてきてリモートのスタイルシートをGETするような処理も、Promiseできるのでコールバック地獄にならない。Fetch API使えるので`XMLHttpRequest`みたいな煩雑な記述もしなくてもいい。そもそもアロー関数でタイプ数自体も少なくて済む。この処理をES3/5で普通に書けば20~30行くらいなるんじゃないかな。

### Let + Const

あとまぁ特にそこまで便利になるわけでもないけど、一応`let`とか`const`とかも使っといた。

## CSS3

### object-fit


```css
.screenshot img {
  object-fit: cover;
  object-position: top;
}
```

`background-size`的なことを`img`要素に対して直接指定できるようなもの。解析したページのキャプチャ画像が今回追加されたが、ページ自体があんまり縦長になるもいやなので、最初は背景画像にして`background-size:cover`的なことをしたが、これだと印刷したときに表示されないので、そういえば`object-fit`があったのを思い出した。今のところIEではサポートされていない。

### currentColor

```hbs
<ul>
  {{#each body.uniqueColors}}
  <li style="color:{{this}}">
    <span class="circle"></span>{{this}}
  </li>
  {{/each}}
</ul>
```

`Unique Colors`の色丸の部分は`span`の`background-color`で指定してあるのだけど、`.circle { background-color:　currentColor; }`で、現在のその要素のcolorプロパティを指定できる。`currentColor`キーワードが使えないと、`<span style="background-color:{{this}}"></span>`みたいな感じで`span`の方にも指定しなきゃいけないというダルいことになる。`currentColor`自体は、IE9以上で使えるので、そこまで最新技術ってことでもないけど良い使い道が見つかって嬉しかったのだ。


## Chrome Extension API

### chrome.tabs

```js
chrome.tabs.captureVisibleTab(screenshotUrl => {})
```

これでキャプチャ取れる！簡単！Phantom.jsなんて使わなくてもいい！

### chrome.runtime

アイコンをクリックしたらcontent scriptを動かすとか。そんでcontent scriptの結果をbackground.jsに返すとか。[Message Passing](https://developer.chrome.com/extensions/messaging)というやつだ。いつも忘れるのでメモっとく。

```background.js
// これでcontent.jsに送信
chrome.browserAction.onClicked.addListener(tab => {
	chrome.tabs.query({active: true, currentWindow: true}, tabs => {
		let activeTab = tabs[0];
		chrome.tabs.sendMessage(activeTab.id, {'message': 'clicked'});
	});
});
// これで受ける
chrome.runtime.onMessage.addListener((request, sender, sendResponse) => {})
```

```content.js
// これで受けて
chrome.runtime.onMessage.addListener(analyzeCSS);
// これでbackground.jsに送信
chrome.runtime.sendMessage({error: false, meta: meta, body: result});
```

## Material Design Lite

+ [Material Design Lite](http://www.getmdl.io/)

使ったと言えないほど、ほぼ既存のテンプレートをいじっただけだ。基本BEMっぽいかんじでクラス属性を付与していくのだけど、`mdl-color-text--grey-500`こうゆう長いユーティリティのクラス属性とかもバンバンつけていく感じで、クラス属性値の見通しがあんまりだなと思った。まぁ、独自の接頭辞とかつけて名前空間区切ったりして汎用性を考慮しなければならないCSSライブラリの宿命か。