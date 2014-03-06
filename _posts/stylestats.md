---
layout: post
title: StyleStats
subtitle: スタイルシートの統計情報を出力するNode Package
categories: development
excerpt: ""
---
スタイルシートの統計情報を出力するNode Packageを作った。Node.js 0.10以上が必要で、CLIだとこんな感じの情報を出力してくれる。

```
$ npm install -g stylestats
$ stylestats path/to/stylesheet.css
StyleStats!
┌───────────────────────────┬───────────────┐
│ Size                      │ 498.0B        │
├───────────────────────────┼───────────────┤
│ Rules                     │ 8             │
├───────────────────────────┼───────────────┤
│ Selectors                 │ 11            │
├───────────────────────────┼───────────────┤
│ Simplicity                │ 72.73%        │
├───────────────────────────┼───────────────┤
│ Lowest Cohesion           │ 6             │
├───────────────────────────┼───────────────┤
│ Lowest Cohesion Selecotor │ hr            │
├───────────────────────────┼───────────────┤
│ Total Unique Font Sizes   │ 5             │
├───────────────────────────┼───────────────┤
│ Unique Font Size          │ 10px          │
│                           │ 12px          │
│                           │ 14px          │
│                           │ 16px          │
│                           │ 18px          │
├───────────────────────────┼───────────────┤
│ Total Unique Colors       │ 2             │
├───────────────────────────┼───────────────┤
│ Unique Color              │ #333          │
│                           │ #CCC          │
├───────────────────────────┼───────────────┤
│ Id Selectors              │ 1             │
├───────────────────────────┼───────────────┤
│ Important Keywords        │ 1             │
├───────────────────────────┼───────────────┤
│ Media Queries             │ 1             │
├───────────────────────────┼───────────────┤
│ Properties Count          │ font-size: 5  │
│                           │ margin: 4     │
│                           │ padding: 3    │
│                           │ color: 2      │
│                           │ display: 1    │
│                           │ height: 1     │
│                           │ border: 1     │
│                           │ border-top: 1 │
└───────────────────────────┴───────────────┘
```

## なんで作ったの？

そもそも論の話、HTML/CSSを書く人って私のようにデザイナー上がりだったり、私のようにプログラミング的バックグラウンドが無かったりする人が多い。そんもんだから、Sassなどのような多少なりともプログラミング的知識の必要となるCSSプリプロセッサを使うと、お盆の帰省ラッシュのようなCSSが吐出される結果になる。

CSSは[レンダリングをブロックする](/mol/log/sprite-image-vs-inline-image/)ので、CSSファイルってゆうのは1byteでも軽くしなければならないと感じている。もっと言えば、バックエンドがAkamaiとかに大金を払って得たスピード分をフロントエンドのHTMLのマークアップの仕方１つで消し飛ばすことも可能なわけだ。

なわけで、フロントエンド、特にHTML/CSSコーディングってのはパフォーマンス的にとても重要だと思っているが、前述のとおり、この分野には優秀な人材が少ない。デキる人はみんなJavaScriptとかバックエンドとかネイティブアプリ書くほうに行っちゃう。だもんで、そうゆう分野にはテスト系のツールであったりコード解析のツールが一杯あって、みんなそうゆうのを使ってちゃんとしたプログラミングを書いている（のはず）。

+ [CSS Architecture | en.ja Article](http://article.enja.io/articles/css-architecture.html)
+ [Code smells in CSS | en.ja Article](http://article.enja.io/articles/code-smells-in-css.html)
+ [About HTML semantics and front-end architecture | en.ja Article](http://article.enja.io/articles/about-html-semantics-and-front-end-architecture.html)
+ [Rules · stubbornella/csslint Wiki](https://github.com/stubbornella/csslint/wiki/Rules)

最近、CSSのテストも増えてきたけどまだまだ足りないというか成熟していないと思う。というわけでなんかそうゆう方向でコントリビュートできないかと思い作った。

## 指標の意味

単純にファイルサイズだけを見ていても、そのCSSが良いCSSなのか悪いCSSなのかよくわからないし、そのほかのもスタイル情報も追加した。

![](http://i.imgur.com/DlCfWNw.png)

### Simplicity

個人的に気に入ってるのがこの指標。単純に`Rules/Selectors`で割ったものをパーセンテージにしたものだ。要は1つのルールに1つのセレクタが対応していたほうが良いって意味。想定としているのはSassの@extendとかで継承しまくってたら、この数値は低くくなる傾向がある。



### Lowest Cohesion


## Jenkinsとの統合

> You can't improve what you can't measure!

