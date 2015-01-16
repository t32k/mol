---
date: 2012-08-06
title: 【翻訳】ソーシャルボタンはお友達さ！
subtitle: Social button BFFs
excerpt: Social button BFFs / Stoyan's phpied.com
---

ども、実兄からFacebook友達申請きて承認を見送るt32kです。そんなソーシャル時代ですけどみなさんいかがお過ごしか？みなさんはこうは思わないだろうか？いいね！ボタンなどのソーシャルボタンはいっぱいあるけど、どうゆうふうに実装すればいいのよ！スニペット、コピペでいいの？ってね。そんなこと考えていたら、いい記事があったので翻訳してみたよの巻。

<cite class="citation">
![](/mol/images/people/stoyan_stefanov.jpg)
原文：[Social button BFFs](http://www.phpied.com/social-button-bffs/)（<time>2011-09-27</time>）by [Stoyan Stefanov](http://www.phpied.com/bio/)
</cite>

TL;DR:JavaScriptの非同期読み込みはWebアプリのパフォーマンスにおいて重要な問題だ。以降に書かれている内容は一般的なソーシャルボタンに共通する取り扱い方についての記事であり、ソーシャルボタンに残りのコンテンツ読み込みをブロックさせないことを学べるだろう。結局のところ、ユーザーはあなたの __コンテンツを最初__  に見たいのであって、それから、そのコンテンツがシェアする価値があるのか決めるのである。

現在、FacebookはJavaScript SDKを読み込むための新しい非同期スニペットを提供している。そのSDKとは<a href="https://developers.facebook.com/docs/reference/javascript/">とてもパワフルな</a>ソーシャルプラグイン（例：いいね！ボタン）を利用するのために必要なものだ。

これまでもJS SDKは非同期読み込みできたが、最近このパターンがデフォルトになった。そのスニペットは極めてナイスでチクショーな（知ってる、正解！）感じだが、ここではどのようになってるか見てみるとする。（<a href="https://developers.facebook.com/docs/reference/plugins/like/">コードはここから入手</a>）

```javascript
(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) {return;}
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/en_US/all.js#xfbml=1";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));
```

私の<a href="http://www.jspatterns.com/">JavaScriptパターン</a>からナイスなとこを抜き出してみる。

+ 即時（自己呼び出し）関数なので、グローバル変数を汚さない
+ よく使う( `document`)オブジェクトと文字列（"scripts", "Facebook-jssdk"）はその即時関数の引数として渡される。可読性を保ちながらできる初歩的な縮小化テクニックである
+ 生成したscriptノードはドキュメントで使用されている最初の `script`要素を利用することによって追加される。あなたのコードが `body load="..."`や、img onload、もしくはそれ同様（ぶっ飛んだ方法を私は知っていますが、とりあえずは0.01%くらい寛大に受け止めよう）のパターンで呼び出されない限り、99.99%確実に動作することを保証できる
+ 追加したノードにはidが割り当てられることで2回同じScriptを読み込むのを防止する（例：ヘッダーや、フッター、記事でいいね！ボタンが使用されているとか）

## ソーシャルボタンのJSファイルすべて

他のソーシャルボタンも存在する。有名なところで<a href="https://twitter.com/about/resources/buttons#tweet">Twitter</a>と<a href="http://www.google.com/intl/en/webmasters/+1/button/index.html">Google +1</a> ボタンだ。これら両方のボタンは、デフォルトかどうか分からないが、各々の設定次第で非同期読み込みが可能だ。

それではなぜすべてうまいことやってけないのか、そしてfacebookの即時関数中に全部収めることがきないのか？私たちはHTMLのバイト数を少しでも削りたいし、余計なscriptタグなんていらないのだ。Google+やTwitterなどのすべてのソーシャルボタンのために新しいscriptノードが必要だ。Google+のスニペットには `type`や `async`などの属性を持っているが、実際これらは必要ないのだ。なぜなら `type`は常に  `text/javascript`だし、 `async`はいつも `true`だから。加えて今async部分をいじってるのだから。

結果がこれだ。

```html
<div id="fb-root"></div>
<script>
    (function(d, s, id) {
    // fb + common
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) {return;}
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/en_US/all.js#xfbml=1";
    fjs.parentNode.insertBefore(js, fjs);
    // +1
    js = d.createElement(s);
    js.src = 'https://apis.google.com/js/plusone.js';
    fjs.parentNode.insertBefore(js, fjs);
    // tweet
    js = d.createElement(s);
    js.src = '//platform.twitter.com/widgets.js';
    fjs.parentNode.insertBefore(js, fjs);
    }(document, 'script', 'facebook-jssdk'));
</script>
```

これは3つのボタン・プラグインで必要な3つのJSファイルを読み込んでいる。

追加で、ノードの生成・追加部分は関数でラッピングができ、コードが引き締まった。最終的なスニペットはこれだ。

```html
<div id="fb-root"></div><!-- fb needs this -->
<script>
    (function(d, s) {
        var js, fjs = d.getElementsByTagName(s)[0], load = function(url, id) {
        if (d.getElementById(id)) {return;}
        js = d.createElement(s); js.src = url; js.id = id;
        fjs.parentNode.insertBefore(js, fjs);
        };
        load('//connect.facebook.net/en_US/all.js#xfbml=1', 'fbjssdk');
        load('https://apis.google.com/js/plusone.js', 'gplus1js');
        load('//platform.twitter.com/widgets.js', 'tweetjs');
    }(document, 'script'));
</script>
```

## ソーシャルボタンのマークアップすべて

次は実際にウィジェットがレンダリングされ箇所についてアドバイスする。Facebookは&lt;fb:like&gt;のようなXFBMLシンタックスでのスニペット提供をしているが、data-*属性を用いた純粋なHTML(5)のスニペットも提供しており、ラッキーなことに他のボタンもそうだ。

これが例である。

```html
<!-- facebook like -->
<div class="fb-like" data-send="false" data-width="280"></div>
<!-- twitter -->
<a class="twitter-share-button" data-count="horizontal">Tweet</a>
<!-- g+ -->
<div class="g-plusone" data-size="medium"></div>
```

Google+は `g-plusone`クラス属性がついた `div`要素が必須であり、Twitterは `twitter-share-buttonク`ラス属性の `a`要素が必須である。Facebookはいいね！なら `fb-like`クラス属性がついたどの要素を扱でも使用できる（もしくは `fb-comments`、 `fb-recommendations`、または君の使いたい<a href="https://developers.facebook.com/docs/plugins/">ソーシャルプラグイン</a>名で）

最も重要なことはJSファイルは一回だけ読み込みさえすれば良いことであり、そうすべきだ。読み込めばすべての異なるボタンがレンダリングされる。Facebookのケースにおいても全てのプラグインがレンダリングされる。いいね！ボタンだけでない。JSファイルの容量を考えて効率良く使おう。

## まとめ

ではこれがソーシャルボタンを読み込むためのベストプラクティスだ。

1. JSスニペットをページの下部、ちょうど&lt;/body&gt;の直前にコピーする。念の為にね。（Google+はJSファイルの後にマークアップがあった時失敗する）これはまた読み込みのためのJSがひとつにまとまり確認しやくすなっている。スニペットの重複・排除の手間はあるとはいえ。
2. 適切な設定値をdata-＊属性に付与し、ページの好きなところにボタン・プラグインを撒き散らしちゃいな！
3. ソーシャルトラフィックの恩恵に預かっちゃいな！

動作に関しては以前の私のブログ <a href="http://phonydev.com/">phonydev.com</a> で確認できる。そうだね、どのボタンもナイスな感じでモバイルでも動いてる。

***

だいたい、最近のソーシャルボタンのスニペットは非同期化してるから個別の非同期化処理がオーバヘッドする。それが解消できるのは良いかと。あとこのボタンのscriptどこよ？ってこともまとめることでなくなると思うので便利かなと思いました。てことで、mixiとhatenaも加えた日本語バージョンのサンプル置いておきますね。

+ [Loading Social Buttons JavaScript](https://dl.dropboxusercontent.com/u/356242/test/loading_social_button/index.html)

あとGoogle アナリティクスのスニペットもまとめられるけど、個人的には分けておいてもいいかなと思う（管理的に）。
