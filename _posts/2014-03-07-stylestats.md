---
layout: post
title: StyleStats
subtitle: スタイルシートの統計情報を出力するNode Package
cover_image: /2014/03-07-cover.jpg
categories: development
excerpt: "スタイルシートの統計情報を出力するNode Packageを作った。Node.js 0.10以上が必要で、CLIだとこんな感じの情報を出力してくれる。"
---

[![](https://github-camo.global.ssl.fastly.net/84b33de130aae5ae27d571c5aa7e4970fc426be8/687474703a2f2f692e696d6775722e636f6d2f38316b4b6e78482e706e67)](https://github.com/t32k/stylestats)
スタイルシートの統計情報を出力するNode Packageを作った。

+ __[t32k/stylestats](https://github.com/t32k/stylestats)__

Node.js 0.10以上が必要で、CLIだとこんな感じの情報を出力してくれる。

```
$ npm install -g stylestats
$ stylestats path/to/stylesheet.css
StyleStats!
┌──────────────────────────┬───────────────┐
│ Size                     │ 498.0B        │
├──────────────────────────┼───────────────┤
│ Rules                    │ 7             │
├──────────────────────────┼───────────────┤
│ Selectors                │ 11            │
├──────────────────────────┼───────────────┤
│ Simplicity               │ 63.64%        │
├──────────────────────────┼───────────────┤
│ Lowest Cohesion          │ 6             │
├──────────────────────────┼───────────────┤
│ Lowest Cohesion Selector │ hr            │
├──────────────────────────┼───────────────┤
│ Total Unique Font Sizes  │ 3             │
├──────────────────────────┼───────────────┤
│ Unique Font Size         │ 10px          │
│                          │ 12px          │
│                          │ 18px          │
├──────────────────────────┼───────────────┤
│ Total Unique Colors      │ 1             │
├──────────────────────────┼───────────────┤
│ Unique Color             │ #333          │
├──────────────────────────┼───────────────┤
│ Id Selectors             │ 1             │
├──────────────────────────┼───────────────┤
│ Universal Selectors      │ 0             │
├──────────────────────────┼───────────────┤
│ Important Keywords       │ 1             │
├──────────────────────────┼───────────────┤
│ Media Queries            │ 1             │
├──────────────────────────┼───────────────┤
│ Properties Count         │ font-size: 5  │
│                          │ margin: 4     │
│                          │ padding: 3    │
│                          │ color: 2      │
│                          │ display: 1    │
└──────────────────────────┴───────────────┘
```

## なんで作ったの？

そもそも論の話、HTML/CSSを書く人って私のようにデザイナー上がりだったり、私のようにプログラミング的バックグラウンドが無かったりする人が多い。そんもんだから、Sassなどのような多少なりともプログラミング的知識の必要となるCSSプリプロセッサを使うと、お盆の帰省ラッシュのようなCSSが吐出される結果になる。

[CSSはレンダリングをブロックする](/mol/log/sprite-image-vs-inline-image/)ので、CSSファイルってゆうのは1byteでも軽くしなければならないと感じている。もっと言えば、バックエンドがAkamaiとかに大金を払って得たスピード分をフロントエンドのHTMLのマークアップの仕方１つで消し飛ばすことも可能なわけだ。

なわけで、フロントエンド、特にHTML/CSSコーディングってのはパフォーマンス的にとても重要だと思っているが、前述のとおり、この分野には優秀な人材が少ない。デキる人はみんなJavaScriptとかバックエンドとかネイティブアプリ書くほうに行っちゃう。だもんで、そうゆう分野にはテスト系のツールであったりコード解析のツールが一杯あって、みんなそうゆうのを使ってちゃんとしたプログラミングを書いている（はず）。

CSSをちゃんとプログラミングするために下記の資料を読んどくと良い。

+ [CSS Architecture | en.ja Article](http://article.enja.io/articles/css-architecture.html)
+ [Code smells in CSS | en.ja Article](http://article.enja.io/articles/code-smells-in-css.html)
+ [SOLID CSS | en.ja Article](http://article.enja.io/articles/solidcss.html)
+ [About HTML semantics and front-end architecture | en.ja Article](http://article.enja.io/articles/about-html-semantics-and-front-end-architecture.html)
+ [Rules · stubbornella/csslint Wiki](https://github.com/stubbornella/csslint/wiki/Rules)

また最近、CSSのテストも増えてきたけどまだまだ足りないというか成熟していないと思う。というわけでなんかそうゆう方向でコントリビュートできないかと思い作った。

## 指標の意味

単純にファイルサイズだけを見ていても、そのCSSが良いCSSなのか悪いCSSなのかよくわからないし、そのほかのもスタイル情報も追加した。

![](http://i.imgur.com/DlCfWNw.png)

### Simplicity

個人的に気に入ってるのがこの指標。単純に`Rules/Selectors`で割ったものをパーセンテージにしたものを僕が勝手にSimplicityと言っている。要は1つのルールに1つのセレクタが対応していたほうが良いって意味。想定としているのはSassの`@extend`とかで継承しまくってたら、この数値は低くくなる傾向がある。個人的には何度も言ってるけど、Webアプリのような複雑大規模なものをコーディングするのであれば。HTML側で責任をもって`<div class="button button-alpha">`のようにマルチクラスでやれば良いと思う。あと、reset.cssとかでもSimplicityは低くなるけど、そこはしかたがないかなと思ってる。

### Lowest Cohesion

Lowest Cohesionは、SOLID CSSのSingle Responsibility Principle / 単一責任の原則に由来してて、一つのルールセットにあまりいろいろなスタイルを詰め過ぎないほうがいい。そのルール内で一番宣言数が多いセレクタと宣言数を返す。

> 凝集度（ぎょうしゅうど、コヒージョン、cohesion）とは、情報工学においてモジュール内のソースコードが特定の機能を提供すべく如何に協調しているかを表す度合いである。IPAが実施する情報処理技術者試験では、強度(きょうど、ストレングス、strength)という言葉が使われる。凝集度は順序尺度の一種であり、「凝集度が高い」とか「凝集度が低い」といった言い方で使われる。凝集度の高いモジュールは、堅牢性、信頼性、再利用性、読みやすさなどの点で好ましく、凝集度の低いモジュールは保守/評価/再利用/読解が難しいため好ましくないとされる。

+ [凝集度 - Wikipedia](http://ja.wikipedia.org/wiki/%E5%87%9D%E9%9B%86%E5%BA%A6)

### Properties Count

どのプロパティがどれだけ宣言されているのか、デフォルトではTop10まで出力してくれます。これの意図は、何回も呼ばれるプロパティなら、それまとめてClassにして使えよ、何回も同じこと書くなよ、とのこと。全部見たかったら、`{"propertiesCount": 1000}`といった設定JSONファイルを一緒に読み込ませればよい。

## Jenkinsとの統合

[Plot with Jenkins · t32k/stylestats Wiki](https://github.com/t32k/stylestats/wiki/Plot-with-Jenkins)

あとCLIだと、CSVで結果を出力できるので、それをJenkinsのPlot Pluginを使ってプロットさせることができる。なので、@extendとか失敗してセレクタとか爆発的に増えたとかあったら、このグラフを見ればよいと思う。

![1c0cwgo.png (750×450)](http://i.imgur.com/1c0cwgo.png)

File Sizeの変遷

![kF0CLWt.png (750×450)](http://i.imgur.com/kF0CLWt.png)

Style Infoの変遷

あと、GitHubへのPushをトリガにビルドを実行させればファイルサイズの変遷とか分かるよね。たいしてビルドに時間かからないし、[CloudBees](http://www.cloudbees.com/)を使えば無料の範囲で記録できるよね。

ちゃんと記録しとけば、リファクタリングの成果もちゃんと報告できるよね！

そんなわけで、__You can't improve what you can't measure!__

