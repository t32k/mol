---
date: 2016-08-30
title: Google Analytics トラッキング スニペット再考（2016）
categories: 
    - analytics
excerpt: 最近、またGoogleアナリティクスの面倒を見ている。で、GAのドキュメントを見ていたら最近のイケてるトラッキングスニペットはこれだぜ！みたいなこと書いてあった。やれやれ、またかと思い、筆をとったのです。
---

最近、またGoogleアナリティクスの面倒を見ている。で、GAのドキュメントを見ていたら最近のイケてるトラッキングスニペットはこれだぜ！みたいなこと書いてあった。やれやれ、またかと思い、筆をとったのです。

トラッキングスニペットの移り変わり激しいもので、最近だとこうゆうのが一般的だろう。

```html
<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','//www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXX-Y', 'auto');
ga('send', 'pageview');
</script>
```


最近のおすすめはこれだとか。

```html
<script>
window.ga=window.ga||function(){(ga.q=ga.q||[]).push(arguments)};ga.l=+new Date
ga('create', 'UA-XXXXX-Y', 'auto');
ga('send', 'pageview');
</script>
<script async src='//www.google-analytics.com/analytics.js'></script>
```

まぁやってることは、最初のスニペットはインラインJavaScriptでscript要素をインジェクトし、そこでanalytics.jsを読み込んでいる。なぜかそうするのかというと、それは非同期読み込みのためなのだけど、後者のスニペットはその処理をすべて`async`属性が担っているので、とってもすっきり。

非同期読み込みの利点は過去の記事を参照。

- [Google Analytics トラッキング スニペット再考（2010）](/mol/log/asynchronous-tracking/)
- [Google Analytics トラッキング スニペット再考（2012）](/mol/log/defer-parsing-of-google-analytics/)

[![](/mol/images/2016/0830-00.png)](http://caniuse.com/#search=async)

`async`属性の対応状況なのだけど、IE9以前とかを気にしなくてよいのなら、このスニペットに置き換えて良いかなと思う。

個人的に、2つのトラッキングスニペットは記述の仕方が違うだけで。やってることは同じなんだろうと考えていたのだけど、実はそうではないらしい。

> 上記の JavaScript トラッキング スニペットにより、すべてのブラウザでスクリプトが確実に読み込まれ、非同期的に実行されますが、最新のブラウザでは、スクリプトをプリロードできないという欠点があります。この問題の対策として、次のような代替の非同期トラッキング スニペットを使用することで、最新ブラウザでのパフォーマンスをわずかに向上させることができます - [サイトに analytics.js を追加する | ウェブ向けアナリティクス](https://developers.google.com/analytics/devguides/collection/analyticsjs/?hl=ja)


『**わずかに向上させる**』ってどうゆうことだってばよ？、『**プリロード**』ってなによ？と思い、また筆をとってしまったのです。

ググったら、myakuraが書いてた。

> script async を使えば、非同期で読み込まれるし、プリロードスキャナの恩恵にも預かれるとのこと。- [script asyncでJavaScriptの非同期読み込みを \- fragmentary](http://myakura.hatenablog.com/entry/2014/10/14/061713)


## PreloadScanner

『プリロードスキャナ』ってなによ！

<div class="fluid"><iframe src="https://www.youtube.com/embed/-GWWQ9jKgxA" frameborder="0" allowfullscreen></iframe></div>

わかりやすいYouTubeがあった。

本来、ブラウザはscript要素を見つけるとDOMの構築をやめ、読み込み・実行が終わるまで待つ。JavaScriptでDOMを変更することができるからね。つまり後続のリソースの読み込みは本来ブロックされるはずだ。しかし、現在のブラウザではJavaScript+CSSのように並列に読み込みが可能である。

[![](/mol/images/2016/0830-01.png)](http://www.browserscope.org/?category=network&v=top)

これがPreloadScannerの仕事らしい。PreloadScannerは副次的なパーサーみたいなもので、メインのパーサがscript要素を見つけてパースを止めると、PreloadScannerが実行され後続のリソースを見つけ読み込む。こいつのすごいところは、画像よりもCSS/JSを先に読み込みなどの優先度もつけてくれるところ。

では、普通にscript要素を読みこめばいいじゃないか！と思われるが、DOMの構築はブロックされているので、レンダリングが完了する時間が遅くなるからダメ！

では、Script要素をインジェクトするやり方でもいいジャマイカ！と思われるが、それだどCSSOM（CSSオブジェクトモデル）の構築をまたなけばならない。なぜならJavaScriptでスタイルの変更を許容しているから、JavaScriptはCSSがどうゆう状態か知らなければならない。これがasync属性だとCSSOMの構築を待たなくても良い。この部分、GAのスニペットで言う『**わずかな向上**』ということだろう。個人的には最近のWebアプリの見た目はリッチになってきてCSSのファイルサイズも増えてるので、やっておいて損はないと思う。

またscript要素をインジェクトするやり方だと、リソースのパスはインラインJavaScriptの中にある。これだとPreloadScannerさんが見つけれらない。なので、描画に関係ないJavaScriptなら、`async`属性で読みこめば、『**プリロード**』の恩恵を受けられるということだ。PreloadScannerの実装自体は2008年ごろwebkitで実装されているので、そんなに新しい技術でもない。頭もすっきりした。

ブラウザさんに敬礼！ブラウザさんに身を委ねよ！

## 参考

- [Script\-injected "async scripts" considered harmful \- igvita\.com](https://www.igvita.com/2014/05/20/script-injected-async-scripts-considered-harmful/)
- [How the Browser Pre\-loader Makes Pages Load Faster \- Andy Davies](http://andydavies.me/blog/2013/10/22/how-the-browser-pre-loader-makes-pages-load-faster/)
- [Optimizing Page Loading in the Web Browser \| WebKit](https://webkit.org/blog/166/optimizing-page-loading-in-web-browser/)
- [JavaScript のインタラクティブ機能を追加する \| Web Fundamentals](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript?hl=ja)
- [オブジェクト モデルを構築する \| Web Fundamentals](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model?hl=ja)