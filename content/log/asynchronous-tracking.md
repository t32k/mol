---
date: 2010-05-28
title: Google Analytics 非同期トラッキングコード再考（2010）
subtitle:
categories: books
excerpt:
ogimage:
---

![](http://t32k.me/static/blog/2010/05/a.jpg)

by [Subharnab](https://www.flickr.com/photos/subharnab/3779676969/)

+ [アナリティクス 日本版 公式ブログ: 成長し続ける Google Analytics のエコシステム](http://analytics-ja.blogspot.ca/2010/05/growing-google-analytics-ecosystem.html)

非同期トラッキングコードが公式に推奨されるようになったので、ようやく重い腰を上げて調べてみました。長文です。


## なぜ、非同期トラッキングコードが推奨されるのか？

今回のトラッキングコードはurcin.js、ga.jsに続く大きな変更となります。非同期トラッキングコードの恩恵を受けるためには、以前のトラッキングコードを使用されている方は、当然変更しなければなりません。しかし、大規模サイトの場合などはアクセス解析担当者とコード実装者は違うことも多く、エンジニアさんにお願いしなければなりません。「え〜、前変えたばっかじゃん！」などと言われるかもしれません。そんな時にアクセス解析担当者はトラッキングコード変更のメリットを提示しなければなりませんね。Analytics 公式ブログでは、非同期トラッキングコードの利点を以下のように説明しています。

> 
1. ブラウザの実行順序改善によるページの読み込み時間高速化
2. データの収集・精度の向上
3. JavaScriptが完全に読み込まれていなかったときの依存性からくるエラーの除去  
― [Google Analytics launches asynchronous tracking - Analytics Blog](http://analytics.blogspot.ca/2009/12/google-analytics-launches-asynchronous.html)

てな感じで3つ挙げられているので、ひとつひとつ確認していきましょう。


## 読み込み時間の高速化

これが、非同期トラッキングコード最大の利点なのではないでしょうか。やはり、Googleのランキングアルゴリズムに読み込む速度が加わった手前、自社サービスがボトルネックとなっていては示しがつきませんしね。

非同期トラッキングコードについて説明していくのですが、まず前提知識としてページの読み込まれ方について解説します。HTTP/1.1の仕様に「ひとつのホスト名（EX: `www.t32k.com`, `img.t32k.com`など）に対して並列ダウンロードできるコンポーネントは数は2つまで」と制限されています。（実際のブラウザ実装は6つとかだけど、IE6,7は2つまで）

![](http://t32k.me/static/blog/2010/05/1.png)

上記のグラフは簡単なモデルですが、すべて同じホスト名から読み込んでいます。まず、HTMLファイルが読み込まれ、画像などのコンポーネントが2個ずつ読み込まれていきます。

このとき、同じホスト名から読み込んでいる外部JavaScriptファイルがページの先頭で読み込まれていた場合はどうなるでしょうか？それを表したのが次のグラフです。

![](http://t32k.me/static/blog/2010/05/2.png)

どうでしょうか。仕様どおりなら「script + img」と並列に読み込まれるはずですが、そうはならずにscriptファイルひとつしか読み込まれていません。つまり、scriptファイルを最初に読み込むでしまうとダウンロード・レンダリングが止まってしまいます。そのため、ハイパフォーマンスWebサイト、高速サイトの実現のための14のルールのひとつ「ルール6：スクリプトは最後に置く」というものがあります。

![](http://t32k.me/static/blog/2010/05/3.png)

このような理由から、非同期以前のトラッキングコードは</body>の直前に置くことが推奨されています。出来る限りページ最下部に置くことでダウンロード・レンダリングを止めないようにしています。上記のグラフのような感じですね。ページを表示するために必要なコンポーネントはscriptの手前ですべて読み込まれているのでこれが最善策なのかなと。

![](http://t32k.me/static/blog/2010/05/4.png)

しかし、非同期トラッキングコードはダウンロードの中断を考えなくてもいいので上記のようなグラフになります。なおかつ、Google Analyticsの解析コードga.jsは、`www.google-analytics.com`から読み込まれていますので、トラッキングコードを挿入したページを読み出すホスト名とは異なるはずなので、ページのレンダリングとは非同期に読む込むことができます。

### async属性に関して

```javascript
ga.type = "text/javascript"; 
ga.async = true;
```

話はちょっと変わりますが、非同期トラッキングコードについて調べていると、HTML5で定義されているasync属性によってこの非同期を実現しているのでasync属性に対応しているFx3.6しか効果がないと書いている人がちらほらいたのですが、それは誤解です。

続・ハイパフォーマンスWebサイトでは、async属性を使わなくてもブラウザの実行をブロックしないスクリプトの読み込みテクニックとして以下の6つを挙げています。

+ XHR eval
+ XHR インジェクション
+ iframe スクリプト
+ Script DOM要素
+ Script Defer
+ document.writeによるSCRIPTタグ書き出し

今回の非同期トラッキングコードではSCRIPT要素をDOMを使って生成することで実現しています。なので、ほとんどのブラウザで非同期で読み込むことが可能です。async属性を記述しているのは明示的に非同期で読み込むことをブラウザに通知するためとGoogle Code Blogには書いてあります。

> HTML5 “async” attribute in this part of the snippet. While it creates the same effect as adding a script element to the DOM, it officially tells browsers that this script can be loaded asynchronously. ― [Google Analytics Launches Asynchronous Tracking - The official Google Code blog](http://googlecode.blogspot.ca/2009/12/google-analytics-launches-asynchronous.html)

まぁ、実際のところどうなん？って感じなので、HTTPWatch(IE6で検証)で、とあるサイトの非同期トラッキングコードの実装の前後を計測したのが以下のウォーターフォールチャートです。

![](http://t32k.me/static/blog/2010/05/5.png)

`</body>`直前に挿入したスタンダードトラッキングコードのチャート

![](http://t32k.me/static/blog/2010/05/6.png)

`</head>`直前に挿入した非同期トラッキングコードのチャート

各コンポーネントの読み込み時間のブレもありますが、おおかた上記チャート図のような読み込まれ方をしています。灰色で強調されている部分がga.jsです。最初のチャート図は以前のように非同期ではないトラッキングコードで読み込んでいますので、ページの表示に必要なコンポーネントをすべて読み込んでからga.jsを読み込み、GIFリクエスト（最後のコンポーネント）をしています。

これが次の非同期トラッキングコードのチャートですと、コンポーネントのダウンロードをブロックしないので早い段階で読み込むことができ、GIFリクエスト（最後のコンポーネント）もページのレンダリングの前に完了しています。結果、ページ全体の読み込み時間は短くなっていますね。（上記の例だと200msぐらい）

## データの収集・精度の向上

パフォーマンス面の理由から最下部にしか置けなかったトラッキングコードですが、非同期で読み込むことができるようになったので、ページの上部におけるようになりました。つまり、それだけGoogle Analyticsを作動させるタイミングを早くすることができます。以前まではページが完全に読み込まれない状態でページ遷移した場合などは記録されないってことも想定されましたがその可能性が低くなったということです。

### トラッキングコードは</head>の直前、<body>の直後？

パフォーマンスを気にすることなく、トラッキングコードは上部に置けるようになったのですが、これどこに置いたらよいの？と疑問があります。ところが、ヘルプの記事や管理画面の注意文によって言っていることがブレていて困りものです。

> headセクションの最後ではなくてbodyセクションの最初です。 調べた限りでは、headセクションに記述するとIE6ではJavascriptの動きに問題が発生することがあるようです。― [Google Analytics非同期トラッキングが標準設定に | 海外SEO情報ブログ](https://www.suzukikenichi.com/blog/google-analytics-asynchronous-tracking-is-now-default/)

上記のブログではbodyセクションの最初って言ってますけど、それよりも何も「問題」ってなによ？って感じで気になったので調べてみました。それを問題にしているところの出典が明記されていないので、よくわかりませんが、たぶんこれが問題じゃないのかなと。

+ [Async snippet causes IE6 to close with "operation aborted" - Google Product Forums](https://productforums.google.com/forum/?hl=en#!category-topic/analytics/asynchronous-tracking-code-snippet/dejkn2pztkU)

IE6でなんかパーシングエラーになるそうです。その解決策としてBest Answerになってるのが、BASE要素をホゲホゲするか、HEAD要素に置いたトラキッングコードをBODY要素に置けばいいぜ！って書いてあります。うん、これっぽい。

んで、これ調べてると他にも関係ありそうな記事を見つけたので紹介。

+ [appendChild vs insertBefore | High Performance Web Sites](http://www.stevesouders.com/blog/2010/05/11/appendchild-vs-insertbefore/)

GoogleでWebパフォーマンスのエバンジェリストしているSteve Soudersさんのブログ記事なんですが、Google Analyticsの非同期トラッキングコードの変遷について解説しています。


```javascript
// 2009年12月段階のベータ版のトラッキングコード
var ga = document.createElement('script');
ga.src = ('https:' == document.location.protocol ?
    'https://ssl' : 'http://www') +
    '.google-analytics.com/ga.js';
ga.setAttribute('async', 'true');
document.documentElement.firstChild.appendChild(ga);
```

```javascript
// 2010年の2月の段階のトラッキングコード
var ga = document.createElement('script');
ga.type = 'text/javascript'; ga.async = true;
ga.src = ('https:' == document.location.protocol ? 
    'https://ssl' : 'http://www') + 
    '.google-analytics.com/ga.js';
var s = document.getElementsByTagName('script')[0];
s.parentNode.insertBefore(ga, s);
```

どこが変わったのですかね。。。まぁちょいちょい微妙に違うのですが、ここでもっとも重要な変更点はSCRIPT要素をDOMで生成した後、ページに挿入するメソッドを、appendChildからinsertBeforeに変更した点です。

なんでこんなことをしたのかとSteve Souders考えるにjQueryで同じような問題があったので参考にしたのではないかと。

> head = document.getElementsByTagName (“head”)[0] || document.documentElement; // Use insertBefore instead of appendChild to circumvent an IE6 bug. // This arises when a base node is used (#2709 and #4378). head.insertBefore(script, head.firstChild);

この#2709の問題ってGoogle Analyticsヘルプでの問題と同じじゃね？つまり、insertBeforeメソッドにすることでIE6のバグは治ったのではないかと僕は推測しました。

んで、もうちょっと調べてみると、ドンピシャな質問がヘルプフォーラムで投げられていました。

+ [Where should Asynchronous code be placed as seen instruction for 2 different places - Google Product Forums](https://productforums.google.com/forum/?hl=en#!category-topic/analytics/asynchronous-tracking-code-snippet/3b5k4HkiMeY)

Q. ヘルプの各記事で</head>の直前、<body>の直後とトラッキングコードの挿入位置が違ってるけど、どっちやねん？

A. 旧バージョンは<body>の直後に置くことでバグ回避してたけど、最新バージョンだったらその問題も起きないねん。ヘルプは今直してるとこやさかい、堪忍して。だから、位置は別にどっちでもええで。

みたいなやりとりですね。2010/5/20の回答なのでこれが最新の情報かな。あれ？答え出た？って感じなんですけど、まだ信用できません。このBest answerのBrian Kuhnって誰？と思ったので調べて見ますと、Twitterで発見。ga.js作ってるGoogleのエンジニアさんじゃないっすか！てか、非同期トラッキングコードリリースの公式ブログ書いてるのこの人じゃないっすか！つか、Twitterでも同じような質問されてるじゃないっすか！

> @tgwilson @BigBryC - Nothing changed. There’s just a couple lingering pages with the old instructions. We’re fixing them. Head is preferred. ― [Brian Kuhn on Twitter](https://twitter.com/briankuhn/status/14340466143)

Brian… あなたにもっと早く出会えていれば….

まぁ、そんなわけで、BODY要素に置かなければならない理由としてのIE6バグはフィックスされている。んで、非同期なのでどこにコードを置いても大丈夫だけど、HEAD要素に置くのが慣例的だし、Brianさんも好みだそうです。データの収集・精度を考えると少しでも上部に置くほうがベター（</head>の直前と<body>の直後じゃ、あんまかわらんけどｗ）なんで</head>の直前で良いのかなと僕は結論づけしました。

それにしても、ヘルプの記事とか修正したら月日記入して欲しいね。。。どっちが最新か分からない＞＜

## 依存性からくるエラーの除去

これまで見てきて非同期ってワンダホー♪って思うのですが、そもそもなぜスクリプトファイルが読み込まれると並列ダウンロードがブロックされるのでしょうか？その理由として、開発者としては上部に置いたコードが先に実行されるという前提の上で実装をしています。もし、A.js、B.jsの順番でHTMLファイル内に読み込んで、非同期のためにB.jsの方が早く読み込みが完了されちゃったとします。B.jsの中にはA.jsで定義されたオブジェクトなど使われているので、当然未定義になってエラーが返される、なんてことが考えられます。例えるなら、jquery.js読み込む前に、jquery-plugin.jsが読み込まれては問題なわけですよ。

なので、非同期で読み込む場合はコードの実行順序を考慮する必要性があります。Google Analyticsの非同期トラッキングコードでは、前半部分がそれに対応した部分になっています。

```javascript
  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-XXXXX-X']);
  _gaq.push(['_trackPageview']);
```
JavaScriptを嗜む程度の自分なのであまり詳しくないですが、このコードを初めて見たとき、なんか見慣れないなと思いました。なんでこうゆう書き方をしているのかなと。Google Code Blogを読む分には、ga.jsが読み込まれていない状態でvar _gaqにはただの配列が代入されて、そのコマンドが配列中に記録されてキュー待ち状態になる。んで、ga.jsが読み込まれると_gaqはオブジェクトになってキュー待ちのコマンドを実行していくという感じです。

まぁ、よく分かりませんが、とりあえず、コードの実行順序を維持するためにこのような書き方になったということが理解できて良かったです。ということで、ga.jsが読み込まれなかったとしてもただの配列の中に蓄えられるだけなのでエラーになる可能性が低くなったということです。

## まとめ

というわけで、非同期トラッキングコードについて、Webデザイナーの自分が背伸びをして調べたわけですが、ほんっと【急募】アクセス解析エンジニアって感じました。