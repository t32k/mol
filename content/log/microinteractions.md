---
date: 2016-07-04
title: マイクロインタラクション事始め以前
subtitle: Microinteractions
categories: 
    - slides
excerpt: 先日、とある社内勉強会にて発表する機会があったので書き残しておく。要は、最近のフロントエンド開発の流れに疲れて、もうちょっと違う方向で頑張ろうと思った話
ogimage: http://t32k.me/mol/images/2016/0704-00.png
---

<small>（アニGIFあるのでちょっと重いです...）</small>

[![](/mol/images/2016/0704-00.png)](http://t32k.me/slides/2016/microinteractions/)

- [マイクロインタラクション事始め以前 @Yahoo!Japan 2016.07.04](http://t32k.me/slides/2016/microinteractions/)　　

先日、とある社内勉強会にて発表する機会があったので書き残しておく。要は最近のフロントエンド開発の流れに疲れて、もうちょっと違う方向で頑張ろうと思った話。

## 葛藤

Kaizen Platform, Inc. フロントエンドデベロッパーのt32kです。皆さん、ご存知かもしれませんが、Kaizen PlatformはA/Bテストツールを提供しています。そのA/Bテストのデザイン案も国内外約2千名のグロースハッカーと呼ばれる方々から、クラウドソーシングで調達することができます。なので、自社内にデザイナー抱えてなくてもA/Bテストが実行可能です。

グロースハッカーの登録自体は無料ですので、デザイナーの方はぜひ登録してもらうと、コンバージョン率の高いデザインとはどうゆうものなのかとか勉強になってよいかと思います。いろいろな企業からオファーという形でA/Bデザイン案が募集されています。

- [グロースハッカー | Kaizen Platform, Inc.](https://kaizenplatform.com/ja/about_growth_hacker.html)

私はそのKAIZEN DASHBOARDと呼ばれる、A/Bテストのレポート・オファー募集などの画面を作っています。2015年の夏にリニューアルしたので、フロントエンドの開発環境は以下の通り、若干、最新とは言えない状況です。

- Angular.js v1.x
- Jade/Slim
- SCSS
- CoffeeScript
- webpack/Gulp

このまま未来永劫、同じ開発環境でいくとは限らないので、順次アップデートしていかなければならないのですが、フロントエンドの流れに若干疲れました(´・ω・｀)。疲れることに定評のあるt32kですが、以前にもビルドツールで消耗した記事を書きました。

- [Grunt/Gulpで憔悴したおっさんの話 - MOL](http://t32k.me/mol/log/npm-run-script/)

今回はSPAのJSフレームワークに関してです。現在Angular v1.xを使っていますが、これをv2.0にするのか、それともReactなのか、それとも他のSPAフレームワークに置き換えることが目下の課題です。

そもそも、最近ではSPA必要なの？問題が話題となっていました。そのアンサー記事のなかで下記の一文に個人的に同意できました。

> ちゃんとしたWebアプリケーションのUIを考えたらSPAにならざるを得ないということが多い
 ― [SPAである価値 - nobkzのブログ](http://nobkz.hatenadiary.jp/entry/2016/06/02/005114)
 
皆がスマホを持ちネイティブアプリが普通に使われている現在、当然ユーザーはその使い心地やルック&フィールをWebアプリにも求めることでしょう。そのような中で、SSR（サーバーサイドレンダリング）でページ単位でリクエストしていると、ページ間遷移時のトランジションエフェクトが適用できなかったりします。

そういった面から、KAIZEN DASHBOARDを振り返ってみると、toBのビジネスのためか、なにか硬い印象をもつザ・ギョーム・アプリケーションになっています。SPAで作っているので基本的にはAPIのデータのやりとりだけでページを軽快に切り替えることができるはずですが、やはりキャッシュ制御は難しく、理想には程遠いモッサリ感です。さらには複雑なフロントエンド開発で疲労困憊な状態です。

このような状況でフロントエンドエンジニアとしてユーザーに価値を提供できているのか？と疑問を持つようになりました。両方SPAである、AngularからReactに作り変えて何の意味があるのか。それよりもSPAの良さを引き出す努力をすべきなのではないかという思いが強くなってきました。

## 光明

SPAのメリット、つまりネイティブアプリのような操作感とはどのようなものか？インタラクションデザインの研究者である渡邊恵太氏は、iPhoneの使いやすさに関してこう評しています。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4861009383/warikiru-22/ref=nosim/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/41AgS62PXgL._SL160_.jpg" alt="融けるデザイン ―ハード×ソフト×ネット時代の新たな設計論" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4861009383/warikiru-22/ref=nosim/" name="azlinklink" target="_blank">融けるデザイン</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2016.7.6</div></div><div class="azlink-detail">渡邊恵太<br />ビー・エヌ・エヌ新社<br />売り上げランキング: 56189<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4861009383/warikiru-22/ref=nosim/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

> 指とグラフィックとの高い動きの連動性が道具的存在となり、自己帰属感ををもたらす。そしてその結果、道具としての透明性を得るためだ

道具が道具として意識されず、身体の拡張のような状態になっていると言っています。このような状態は、他の言葉でも表せることが可能かと思います。フローとは、完全に集中してのめり込んでいる状態のことをいいます。ユーザーがこのような状態になっているとき、アプリケーションに対する評価は高いものとなっています。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4790714799/warikiru-22/ref=nosim/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/41GrqvZVxsL._SL160_.jpg" alt="フロー体験入門―楽しみと創造の心理学" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4790714799/warikiru-22/ref=nosim/" name="azlinklink" target="_blank">フロー体験入門</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2016.7.6</div></div><div class="azlink-detail">M.チクセントミハイ,大森 弘<br />世界思想社<br />売り上げランキング: 11959<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4790714799/warikiru-22/ref=nosim/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

では、このようなフローをどのように起こさせるのでしょう。フローを構成する要素としてはいくつかありますが、ここでは2点を挙げます。

- 直接的で即座な反応(活動の過程における成功と失敗が明確で、行動が必要に応じて調節される)
- 状況や活動を自分で制御している感覚

このことから私は以下のように目標を設定しました。

『トリガーに対するフィードバックの**プロセス**を表示することで、ユーザーの理解を促進する。適切で即座なフィードバックを返すことでユーザーをフロー（に近い）状態にさせる』

この目標に対して、フロントエンドエンジニアとしてモーションやインタラクションをデザインについて考える必要がありました。ただ、一から考えるのは大変なので、GoogleのMaterial Designを参考にしました。[Material Designはモーションに関しても詳細なガイドライン](https://material.google.com/motion/material-motion.html)があるので、大変参考になります。

- **Meaningful transitions** 意味のあるトランジションを心がけよう
- **Visual continuity** ビジュアルの一貫性に気をつけよう
- **Delightful details** 遊び心もあればいいよね！


## 実装

![](http://t32k.me/slides/2016/microinteractions/img/animation.png)

まずはじめに、汎用アニメーションを定義したCSSをいくつか用意しました。このCSSを動かしたい要素に対して指定するだけで、その要素の状態が変化したときにfadeやzoomといったアニメーションが作動します。これを実現しているのはAngularの[ngAnimate](https://docs.angularjs.org/api/ngAnimate)という機能を使っているからです。これは、ng-showやng-hideディレクティブが指定されている要素のモデルに変更があった場合、A
ngular側で、`.ng-enter`や`.ng-leave`などのアニメーションのフックとなるCSSクラスを自動的に付与してくれるので事前にアニメーションを定義できるのです。同様な機能はReactやVue.jsにもあるので利用可能です。

Build In-Outは表示・非表示になるものに対して。Actionはアニメーション後もその場に残るものに対して適用するのがよいでしょう。ちなみに、個人的にアニメーションが定義しているCSSに関しては`a-`というプレフィックスをつけてグルーピングしています。

Durationに関しては、あまり長い時間を指定すると体感速度を遅く感じさせてしまう危険性があります。Material Designではデバイスの解像度にもよりますが150ms~375msくらいが適切だと記述してあります。

ngAnimateを使ったサンプルをCodePenにあげときましたので、いろいろいじってみるとよいです。

- [ngAnimation](http://codepen.io/t32k/pen/obroxj)
- [ngAnimation playground](http://codepen.io/t32k/pen/KzKLKL)

#### デザイン案いいね！アニメーション

![](http://t32k.me/slides/2016/microinteractions/img/mm_like.gif)

さて、実際の実践例ですが、まずはじめに作ったのが、デザイン案いいね！アニメーションです。
これは、グロースハッカーさんが作ったデザイン案に対して、他の人がいいね！をつけれる機能です。まぁ作ったと言っても、イージングを少しいじった程度です。アニメーションなどに気にも留めていなかったら、いいね！機能実装タスクなんてものは、この場合、ハートの色をグレーからピンクに変えただけで終わっていたでしょう。これでなにか劇的に変わるといったものではないですが、このようなDelightful detailsの積み重ねが大事だと考えています。
 
#### 同オファー複数デザイン案の展開トランジション

![](http://t32k.me/slides/2016/microinteractions/img/mm_expand.gif)

いいね！のアニメーションが同僚に好評で、調子に乗ったt32kが、次にやったのが同オファー複数デザイン案の展開トランジションです。これは同じオファーでグロースハッカーさんが複数デザイン案を投稿した場合、たいていそのデザイン案は色違いやキャッチコピーの違いだけであまりビジュアル的差分がないので、一番改善率が高いものだけ表示して他はまとめているといった状態です。これをもし、トランジション無しに他のデザイン案が展開されたら、パッと見、いったいどこまで同じオファーグループのデザイン案か分かりにくい状態だったかと思います。これはMeaningful transitions意識したもので、代表デザイン案のカード（左）から`.a-compress-right`で出てくることで同グループであることを理解させたいためでした。

#### ディレクション割り当てインタラクション

![](http://t32k.me/slides/2016/microinteractions/img/mm_direction.gif)

トランジションやアニメーションに慣れてきたので、今度はそれらを組み合わせることで、ちょっとしたマイクロインタラクション的なものを実装できるようになりました。ディレクション割り当てインタラクションはオファーに対してグロースハッカーではなくディレクターをアサインする機能です。従来の方法でこの機能を実装すれば、『ディレクションをアサインする』ボタンを置き、そのボタンを押すとモーダル画面が展開され、ユーザー一覧からアサインさせるといったのが普通です。現にそのような手法はDashboardでも多く使われています。ただそれだと、モードの切替のコストも高いですし、手順も多いです。今回のインタラクションはトリガーとそれのフィードバックも近いところで発生しており、Visual continuityもあり直感的なインタラクションになってるかと思います。

## 共有

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116597/warikiru-22/ref=nosim/" name="azlinklink" target="_blank"><img src="http://ecx.images-amazon.com/images/I/51LgvWft-IL._SL160_.jpg" alt="マイクロインタラクション ―UI/UXデザインの神が宿る細部" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116597/warikiru-22/ref=nosim/" name="azlinklink" target="_blank">マイクロインタラクション<br>UI/UXデザインの神が宿る細部</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2016.7.6</div></div><div class="azlink-detail">Dan Saffer,武舎 広幸,武舎 るみ<br />オライリージャパン<br />売り上げランキング: 60411<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4873116597/warikiru-22/ref=nosim/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

実装したら他の同僚に共有しましょう。共有するときに、動きやモノに名前が決まっていると説明しやすいです。例えば、先ほどのインタラクションも、トリガーをクリックすると絞り込みフォームが`.a-compress-right`で出てきて、次にユーザーリストが`.a-compress-bottom`で出現。ユーザーをクリックすると`.a-move-right`でremoveされ、`.a-fade`でディレクションとして出現する。といった感じで表現できます。

私はデザイナー上がりのフロントエンドエンジニアでこのようなインタラクションやモーションに関して疎くないのですが、エンジニア上がりのフロントエンドエンジニアと一緒に作業するときはこういった取り決めがあるとスムーズに進むことでしょう。またデザイナーも必ずしもコードがかけたりインタラクションに造詣があるといったこともないので、みんなで作っていく姿勢が大事かと思います。

最後になりましたが、あまり大げさに捉えることなく、できることから、小さなところから手を付けて行くのが良いかと思います。そういった小さな、つまりマイクロインタラクションの集合が使いやすいアプリケーションとなりユーザーに価値を提供できるのではないかと考えています。

ありがとうございましたm(_ _)m

あ、あと、インタラクションとかもできちゃうフロントエンドエンジニアを弊社では募集しております。よろっしゃお願いしすm(_ _)m

- [Kaizen Platform, Inc. - Frontend Engineer/ フロントエンドエンジニア](https://jobs.lever.co/kaizenplatform/8a4371bd-8a4f-465c-81b1-8a28b9851a48)

--- 

今回アニメーションGIFを載せたかったので、KeynoteやめてHTMLスライドを使用した。使ったのはTalkie。PDF化まで名古屋人によるもの。あーなごやか。

- [ahomu/Talkie: Simple slide presentation library.](https://github.com/ahomu/Talkie)
- [TalkieのスライドをPDF化するツール作った | ブログ :: Web notes.log](http://blog.wnotes.net/blog/article/talkie-slide-to-pdf-tool)
