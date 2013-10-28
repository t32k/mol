---
layout: post
title: ソーシャルボタンはお友達さ(・ω
categories:
- javascript
- performance
- translate
tags:
- facebook
- twitter
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '7924'
---
ども、実兄からFacebook友達申請きて承認を見送るt32kです。そんなソーシャル時代ですけどみなさんいかがお過ごしか？みなさんはこうは思わないだろうか？いいね！ボタンなどのソーシャルボタンはいっぱいあるけど、どうゆうふうに実装すればいいのよ！スニペット、コピペでいいの？ってね。そんなこと考えていたら、いい記事があったので翻訳してみたよの巻。

<cite>原文：<a href="http://www.phpied.com/social-button-bffs/">Social button BFFs / Stoyan's phpied.com</a>
投稿日：2011-9-27 by <a href="https://twitter.com/stoyanstefanov">@stoyanstefanov</a></cite>

長すぎる、読んでない：JavaScriptの非同期読み込みはWebアプリのパフォーマンスにおいて重要な問題だ。以降に書かれている内容は一般的なソーシャルボタンに共通する取り扱い方についての記事であり、ソーシャルボタンに残りのコンテンツ読み込みをブロックさせないことを学べるだろう。結局のところ、ユーザーはあなたの<strong>コンテンツを最初</strong>に見たいのであって、それから、そのコンテンツがシェアする価値があるのか決めるのである。

<!--more-->

現在、FacebookはJavaScript SDKを読み込むための新しい非同期スニペットを提供している。そのSDKとは<a href="https://developers.facebook.com/docs/reference/javascript/">とてもパワフルな</a>ソーシャルプラグイン（例：いいね！ボタン）を利用するのために必要なものだ。

これまでもJS SDKは非同期読み込みできたが、最近このパターンがデフォルトになった。そのスニペットは極めてナイスでチクショーな（知ってる、正解！）感じだが、ここではどのようになってるか見てみるとする。（<a href="https://developers.facebook.com/docs/reference/plugins/like/">コードはここから入手</a>）
<pre><code>(function(d, s, id) {
  var js, fjs = d.getElementsByTagName(s)[0];
  if (d.getElementById(id)) {return;}
  js = d.createElement(s); js.id = id;
  js.src = "//connect.facebook.net/en_US/all.js#xfbml=1";
  fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</code></pre>
私の<a href="http://www.jspatterns.com/">JavaScriptパターン</a>からナイスなとこを抜き出してみる。
<ul>
  <li>即時（自己呼び出し）関数なので、グローバル変数を汚さない</li>
  <li>よく使う(<em>document</em>)オブジェクトと文字列（"scripts", "Facebook-jssdk"）はその即時関数の引数として渡される。可読性を保ちながらできる初歩的な縮小化テクニックである</li>
  <li>生成したscriptノードはドキュメントで使用されている最初の<em>script</em>要素を利用することによって追加される。あなたのコードが<em>body load="..."</em>や、img onload、もしくはそれ同様（ぶっ飛んだ方法を私は知っていますが、とりあえずは0.01%くらい寛大に受け止めよう）のパターンで呼び出されない限り、99.99%確実に動作することを保証できる</li>
  <li>追加したノードにはidが割り当てられることで2回同じScriptを読み込むのを防止する（例：ヘッダーや、フッター、記事でいいね！ボタンが使用されているとか）</li>
</ul>
<h2>ソーシャルボタンのJSファイルすべて</h2>
他のソーシャルボタンも存在する。有名なところで<a href="https://twitter.com/about/resources/buttons#tweet">Twitter</a>と<a href="http://www.google.com/intl/en/webmasters/+1/button/index.html">Google +1</a> ボタンだ。これら両方のボタンは、デフォルトかどうか分からないが、各々の設定次第で非同期読み込みが可能だ。

それではなぜすべてうまいことやってけないのか、そしてfacebookの即時関数中に全部収めることがきないのか？私たちはHTMLのバイト数を少しでも削りたいし、余計なscriptタグなんていらないのだ。Google+やTwitterなどのすべてのソーシャルボタンのために新しいscriptノードが必要だ。Google+のスニペットには<em>type</em>や<em>async</em>などの属性を持っているが、実際これらは必要ないのだ。なぜなら<em>type</em>は常に <em>text/javascript</em>だし、<em>async</em>はいつも<em>true</em>だから。加えて今async部分をいじってるのだから。

結果がこれだ。
<pre><code>  &lt;div id="fb-root"&gt;&lt;/div&gt;
  &lt;script&gt;(function(d, s, id) {
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
  }(document, 'script', 'facebook-jssdk'));&lt;/script&gt;</code></pre>
これは3つのボタン・プラグインで必要な3つのJSファイルを読み込んでいる。

追加で、ノードの生成・追加部分は関数でラッピングができ、コードが引き締まった。最終的なスニペットはこれだ。
<pre><code>&lt;div id="fb-root"&gt;&lt;/div&gt;&lt;!-- fb needs this --&gt;
&lt;script&gt;(function(d, s) {
  var js, fjs = d.getElementsByTagName(s)[0], load = function(url, id) {
    if (d.getElementById(id)) {return;}
    js = d.createElement(s); js.src = url; js.id = id;
    fjs.parentNode.insertBefore(js, fjs);
  };
  load('//connect.facebook.net/en_US/all.js#xfbml=1', 'fbjssdk');
  load('https://apis.google.com/js/plusone.js', 'gplus1js');
  load('//platform.twitter.com/widgets.js', 'tweetjs');
}(document, 'script'));&lt;/script&gt;</code></pre>
<h2>ソーシャルボタンのマークアップすべて</h2>
次は実際にウィジェットがレンダリングされ箇所についてアドバイスする。Facebookは&lt;fb:like&gt;のようなXFBMLシンタックスでのスニペット提供をしているが、data-*属性を用いた純粋なHTML(5)のスニペットも提供しており、ラッキーなことに他のボタンもそうだ。

これが例である。
<pre><code>&lt;!-- facebook like --&gt;
&lt;div class="fb-like" data-send="false" data-width="280"&gt;&lt;/div&gt;
&lt;!-- twitter --&gt;
&lt;a class="twitter-share-button" data-count="horizontal"&gt;Tweet&lt;/a&gt;
&lt;!-- g+ --&gt;
&lt;div class="g-plusone" data-size="medium"&gt;&lt;/div&gt;</code></pre>
Google+は<em>g-plusone</em>クラス属性がついた<em>div</em>要素が必須であり、Twitterは<em>twitter-share-buttonク</em>ラス属性の<em>a</em>要素が必須である。Facebookはいいね！なら<em>fb-like</em>クラス属性がついたどの要素を扱でも使用できる（もしくは<em>fb-comments</em>、<em>fb-recommendations</em>、または君の使いたい<a href="https://developers.facebook.com/docs/plugins/">ソーシャルプラグイン</a>名で）

最も重要なことはJSファイルは一回だけ読み込みさえすれば良いことであり、そうすべきだ。読み込めばすべての異なるボタンがレンダリングされる。Facebookのケースにおいても全てのプラグインがレンダリングされる。いいね！ボタンだけでない。JSファイルの容量を考えて効率良く使おう。
<h2>まとめ</h2>
ではこれがソーシャルボタンを読み込むためのベストプラクティスだ。
<ol>
  <li> JSスニペットをページの下部、ちょうど&lt;/body&gt;の直前にコピーする。念の為にね。（Google+はJSファイルの後にマークアップがあった時失敗する）これはまた読み込みのためのJSがひとつにまとまり確認しやくすなっている。スニペットの重複・排除の手間はあるとはいえ。</li>
  <li>適切な設定値をdata-＊属性に付与し、ページの好きなところにボタン・プラグインを撒き散らしちゃいな！</li>
  <li>ソーシャルトラフィックの恩恵に預かっちゃいな！</li>
</ol>
動作に関しては以前の私のブログ <a href="http://phonydev.com/">phonydev.com</a> で確認できる。そうだね、どのボタンもナイスな感じでモバイルでも動いてる。

--　[翻訳ここまで]　--

だいたい、最近のソーシャルボタンのスニペットは非同期化してるから個別の非同期化処理がオーバヘッドする。それが解消できるのは良いかと。あとこのボタンのscriptどこよ？ってこともまとめることでなくなると思うので便利かなと思いました。

てことで、mixiとhatenaも加えた日本語バージョンのサンプル置いておきますね。
<ul>
  <li><strong><a href="http://t32k.github.io/test/social-button-bffs/">Loading Social Buttons JavaScript  </a></strong></li>
</ul>
<div>あとGoogle アナリティクスのスニペットもまとめられるけど、個人的には分けておいてもいいかなと思う（管理的に）。</div>
<div></div>
<div></div>
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873114888/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/51ZoMJ%2BrLhL._SL160_.jpg" alt="JavaScriptパターン ―優れたアプリケーションのための作法" width="125" height="160" border="0" /></a></td>
<td valign="top"><span><span><a href="http://www.amazon.co.jp/JavaScript%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3-%E2%80%95%E5%84%AA%E3%82%8C%E3%81%9F%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E4%BD%9C%E6%B3%95-Stoyan-Stefanov/dp/4873114888%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114888" target="_blank">JavaScriptパターン ―優れたアプリケーションのための作法
</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" /></span></span>Stoyan Stefanov 豊福 剛

オライリージャパン 2011-02-16
売り上げランキング : 16826
<a href="http://www.amazon.co.jp/JavaScript%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3-%E2%80%95%E5%84%AA%E3%82%8C%E3%81%9F%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E3%81%9F%E3%82%81%E3%81%AE%E4%BD%9C%E6%B3%95-Stoyan-Stefanov/dp/4873114888%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4873114888" target="_blank">Amazonで詳しく見る</a> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
