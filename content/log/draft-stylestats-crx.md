---
date: 2016-01-19
title: StyleStats Chrome拡張機能ができました
subtitle: 
categories: develop
excerpt:
ogimage: 
draft: true
---

# つくったもの

![StyleStats Chrome拡張機能](http://i.imgur.com/EJSI1qU.gif)


[StyleStats](https://github.com/t32k/stylestats)のChrome Extensionを作りました。

+ [stylestats/stylestats-chrome-extension](https://github.com/stylestats/stylestats-chrome-extension)

StyleStatsは僕が作っているOSSで、CSSを解析して指標を表示してくれるnpmです。それを簡単にChrome拡張から利用できるようにしました。調べたいページで右上のボタンを押すと新規タブで結果が出ます。

なので、CSS解析ツールとしてのStyleStatsをもっとデザインよりにする必要がありました。ということで、今回の拡張は`color`や`font-family`、`font-size`のプレビュー表示を主役な感じにしました。

### CLI

![これまで](https://kaizen.qiita.com/files/0f9fb514-d47e-c3e7-1dff-902d9a9d664a.png)

これはシステマティックすぎる。

### Web

![ウェブ](https://kaizen.qiita.com/files/3f9ec6ec-d0f8-3882-f03f-648ef9531ede.png)

いくぶんかユーザーフレンドリーなインターフェースになったけど、Webにアクセスするのめんどくさい。

### Chrome拡張

![キタコレ！](https://kaizen.qiita.com/files/54a5f3eb-112a-4af8-fd81-6cbca03a2b0a.png)


```
　　　　, - - ､
　　＜（　　　 `､　ヽ　 '　'　`,-‐､
　　　　/⌒　　￣＼＼从/, | 刃
　　　 /　.ｲ　　　　l |　 ' ; 　|　.|
　　　/ ./ |　　　　 | | ∴`　|　 |
　　 / ./　 |　　　　| .|/Wヽ |　 |＿∧
　　/ ./　　|　　　　|　|､'　` |　 |´Д｀）__ 　　イヤッッホォォォオオォオウ！
　⊂､Ｊ　 （　　 i.　 !__）　; :　|　　　　^ﾑ　〕
　 !　 !!　　|　 .||　 |　!! '　　　|　　　　|.i　.|
　 :　 :: 　 .|　 .| |　 |　:: 　　　 |　　 　 |!　 |
　　　　　 )　 ）　)　 ）　/￣｀ヽ　　　 | `‐´!
　　　　　.|　 |　 |　 |　 |＼　"ﾍ､._　　| !　 :
　　　　　|　 |　　|　 |.　! ; !＼　 l|　　| .;
　　　　 .|　 |.　　 |　 |ヾ从 /, | / |.　 | .
　　　　 |＼__）　 |＼__) ､ ` 　`'.　|.　 |
　　　　 !　 ! !　　!　!　!!;　''　 　　 |　 |
　 　 　 :　 : :　　 :　:／/W ＼ 　　|　 |
　　　　　　　 　 　 '　 ;　 ,　　`　､ |　 !
　　　　　　　　　　　 　 　 　 　 　 !__/
　　　　　　　　　　　　　　　　　　 !　! !
　　　　　　　　　　　　　　　　　　 :　: :
```


# なにを得たの？

> そこはヘブン(*´ω｀*)！

当たり前だけど、Chrome拡張なのでクロスブラウザ対応を気にしなくてよいし、Angular.jsもいないので、のびのびできました。しかもBabelならなくてもいい！

## ES2015

### arrow function + promise + fetch

```js
Promise.all(links.map(link =>
  fetch(link.href, {mode: 'cors'}).then(response => response.text())
))
.then(texts => {});
```

`<link rel="stylesheet">`要素を見つけて、リモートのスタイルシートをGETしてるけど、Promiseできるのでコールバック地獄にならない、Fetch API使えるのでXMLHTTPRequestみたいな煩雑な記述しなくてもいい、アロー関数でタイプ数も少なくて済む。この記述とか普通にES3/5で書けば20~30行くらいになるだろう。

### let + const

あと、自己満だけど`let`とか`const`とか。

## CSS3

### object-fit

`background-cover`的なことを`img`要素に対して直接できる

### currentColor

![Screen Shot 2016-01-15 at 15.08.30.png](https://kaizen.qiita.com/files/3a979a13-ca51-128e-7fe9-ab21a7f90db3.png)

```html
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
