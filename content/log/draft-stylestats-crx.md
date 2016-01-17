---
date: 2016-01-20
title: StyleStatsのChrome拡張機能ができました
subtitle: StyleStats Chrome Extension
categories: develop
excerpt:
ogimage: 
draft: true
---

![StyleStats Chrome拡張機能](http://i.imgur.com/EJSI1qU.gif)

[StyleStats](https://github.com/t32k/stylestats)のChrome拡張を作った。

+ [stylestats/stylestats-chrome-extension](https://github.com/stylestats/stylestats-chrome-extension)

StyleStatsはCSSを解析してスタイルの各種指標を表示してくれるnpmだ。それを簡単にChrome拡張から利用できるようにした。調べたいページで右上のボタンを押すと新規タブで結果が出る。実に簡単だ。

## これまでの流れ

### CLI

```shell
$ npm install -g stylestats
```

[npm](https://www.npmjs.com/package/stylestats)からインストールしてコマンドラインで使うのが一番やれることが多い。ローカルのファイルも解析できるし、それこそProgrammaticallyに自分でハックして、独自のレポートとかもできる。まぁ黒い画面に不慣れ人はちょっとあれかもしれない。

### Web

そうゆうわけで、もっとライトに使ってもらおうとWeb版も作った。CLIと違って、`Unique Font Families`、　`Unique Colors` がプレビューできたり、円グラフやタイムラインチャートなどグラフ機能を充実している。一つ一つのテスト結果にパーマリンクができるので、CSSといえどデータを残したくないって人はアレかもしれない。

### CRX

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

`background-cover`的なことを`img`要素に対して直接できる

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

色丸は`span`の`background-color`で指定してあるのだけど、`.circle { background-color:currentcolor }`で現在のその要素のcolorプロパティを指定できる。


## Chrome Extension API

### chrome.tabs

```js
chrome.tabs.captureVisibleTab(screenshotUrl => {})
```

これでキャプチャ取れる！Phantom.jsなんて使わなくてもいい！

### chrome.runtime

アイコンをクリックしたらcontent scriptを動かすとか。そんでcontent scriptの結果をbackground.jsに返すとか。

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

## 課題感

・エラーハンドリング
・`window.print()`使えないのかよ！印刷綺麗に！
・なんかもっとデザインに役に立つ情報とは？
