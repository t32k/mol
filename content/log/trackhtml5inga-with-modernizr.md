---
date: 2010-12-02
title: ModernizrでHTML5時代のWeb技術をトラッッキング
subtitle: JavaScript Advent Calendar 2010
categories: 
    - analytics
excerpt: こうゆうおもしろい催し事があるみたいなので僕からは便利なJSライブラリの紹介をばしたいと思います。
ogimage: /static/blog/2010/12/newt.jpg
---

> JavaScript Advent Calendar 2010 : ATND 2010年12月1日から25日まで、毎日違う人が JavaScript にまつわるブログ記事を書く企画です。 参加表明した順番が日付（12月◯日）となります。

## What is Modernizr?

まずはタイトルにもある [Modernizr](http://modernizr.com/) ですが、これはHTML5時代のWeb技術、最近では「NEWT」、New Exciting Web Technologies （HTML5、CSS3、SVG、XHR2、Geolocation… などの技術総称）と呼ばれている技術がブラウザで実装されているか検出してくれるライブラリです。最近、開発者のPaul Irishさんが来日してその存在を知りました。

Modernizr を読み込んだページにアクセスすると自動的にHTML要素のclass属性に対応状況がこん感じで記述される具合です。

![Google Chrome 7.0.517.44](/static/blog/2010/12/chrome.png)

機能が実装されていばその機能名、実装されていなければno-が頭につく感じですね。おおもとのHTML要素にclass属性がついたので、

```css
.borderradius .hoge div {
 /* border-radiusのプロパティを記述 */
}
.no-borderradius .hoge div {
 /* border-radiusに対応していないから画像で再現する記述とか */
}
```

こんな感じで子孫セレクタを使って実装状況に合わせたスタイルを記述することができます。

```javascript
if (Modernizr.localstorage){
  // localstorage 使う！使う！
} else {
  // 代替手段として Cookie 使ったりとか
}
```

もちろんJavaScriptからもこんな感じで分岐処理することも可能です。


## Track HTML5 in Google Analytics

この非常に便利な Modernizr を利用して、Google Analytics のレポート上でも確認できるようにしてくれるのが [trackHTML5inGA](https://github.com/smeranda/trackHTML5inGA) です。Modernizr で検出したプロパティをカスタム変数（デフォルトではスロット#5を使用する）で取り込んで Google Analytics に渡す感じでしょうか。

使い方はModernizrとtrackHTML5inGA をダウンロードしてきて任意のサーバーにアップして以下のコードをGATC（Google Analytics Tracking Code）の後にでも挿入しておきましょう。（※非同期版トラッキングコードのみに対応）

```javascript
<script type=“text/javascript”>
   // トッラッキングしたいプロパティを記述
   featuresToTrack = [‘video’,‘audio’];
   (function(d, t) {
     var s=d.createElement(t),x=d.getElementsByTagName(t)[0];
     s.async=1;s.src=‘js/trackHTML5inGA.js’;
     x.parentNode.insertBefore(s,x);
   })(document, ‘script’);
</script>
```

上記のfeaturesToTrackの部分にトラッキングしたいプロパティ（40種類くらいトラッキングできるプロパティはあるけど、GAの仕様上、配列内に記述できる文字列は55byte以内に納めなければならない）を記述することで、GAのレポートのユーザー > カスタム変数 に HTML5 の項目できているのでクリックすると、任意のプロパティを実装しているブラウザのセッション数などがわかります。もちろん、コンバージョンを設定すれば、実装機能別の成果を確認することができます。

![](/static/blog/2010/12/customvar.png)

これをうまく使えば、CSS3アニメーションを使ったバリバリインタラクティブ登録フォームを作成してその成果を確かめたり、application cacheを大いに活用すればパフォーマンス的に良くなるわけですからapplication cacheを実装していないセグメントと比べてどのくらい成果が違うかなど確認できるかなど使い方はあなた次第！

単一のプロパティであれば、カスタムセグメントでブラウザのバージョンごとの実装状況を調べて自力でセグメント分けすればいいのですが、これが複数のプロパティ（ex. border-radiusかつCSS AnimationsかつGeolocation APIを実装しているブラウザとか）を対象とするとややこしくなるので、やはりそういう点ではこのtrackHTML5inGAを使うメリットがあるのではないでしょうか。

そういうわけで、Modernizr と trackHTML5inGA の紹介でした。