---
date: 2019-07-24
title: がんばらないデザインシステム
subtitle: Material is an adaptable system.
categories: 
    - design
excerpt: Material Designをカスタマイズして利用した話
ogimage: https://t32k.me/mol/images/2019/0723/06.png
---

> **TLDR**: Material Designをカスタマイズして利用した話

[![The Way We Build](/mol/images/2019/0723/01.png)](https://airbnb.design/the-way-we-build/)

最近、**デザインシステム**って言葉よく聞きますよね。airbnbではDLSというデザインシステムを持っていたり、Uberは[Base Web](https://eng.uber.com/introducing-base-web/)というデザインシステムを持っていたり、[アメリカ連邦政府](https://www.catapultsuplex.com/entry/building-a-large-scale-design-system)も持ってたりします。国内のIT企業でもデザインシステムを作成しているとの事例もよく耳にします。

## デザインシステムとは？

[![Design Systems](/mol/images/2019/0723/02.png)](https://blog.prototypr.io/pattern-library-style-guides-design-systems-do-you-need-one-b7857af0f255)

> **デザインシステム**：デザインの基準やドキュメント、原則に加えて、基準を達成するためのUIパターンやコンポーネントなどのツールキットをすべて備えたもの。\
[デザインシステムの定義と作成方法、導入事例 \| UX MILK](https://uxmilk.jp/72387)

では、デザインシステムってのはどういったもんなんでしょうか？これまでも、スタイルガイドやコンポーネントライブラリといったものは聞いたことがありますが、デザインシステムというのはそれらも含めたもう少し大きなモノと個人的に考えています。

「Design Systems」という、まさしくな書籍がありますが、その著者が調べたことによると、デザインシステムというのは以下の4つの要素を含んでいるのではないかと言っています。

<div class="__media"><a href="https://www.amazon.co.jp/dp/4862464122/?tag=warikiru-22" target="_blank" rel="noopener">
<img src="https://images-na.ssl-images-amazon.com/images/I/51s1RuZ1xiL._SX353_BO1,204,203,200_.jpg" alt="" class="__media__image">
<div class="__media__body">
    <div>Design Systems<br>デジタルプロダクトのためのデザインシステム実践ガイド</div>
    <div class="__media__text">アラ・コルマトヴァ (著), 佐藤伸哉  (監修), & 1 その他</div>
    <div>Amazon.co.jpで詳細を見る</div>
</div>
</a></div>

- デザイン原則 / Design Principles
- 認知パターン / Perceptual Patterns
- 機能パターン / Functional Patterns
- 共有言語 / Shared Language

デザイン原則というのはそのシステムのデザイン指針を表した短い言葉ですね、airbnbですと、**Unified**や**Conversational**といったものがデザイン原則として掲げています。

認知パターンというのは、カラーやタイポグラフィといったブランドの認知に必要なものです。機能パターンは、ボタンやタブといったUIコンポーネントを指します。

また共有言語というのは、例えば、そのアプリ・サイト内で一番目立つボタンを何というか？「プライマリーボタン」、「ビックボタン」名前はなんでも良いのですが、それと決めたら、デザイナーだけでなく、エンジニア・ビジネスサイドも同じ言葉で話が通じる状態のことを言います。

そうゆうものを含んだデザインシステムを利用すると何が良いのでしょうか？

- 市場に投入されるまでの時間が短縮される
- プラットフォームや製品をまたいでもUXが一貫する
- バージョン管理の問題が減る
- 協力とコミュニケーションが簡単になる

メリットいっぱいですね。というわけで、弊社でもデザインシステム作りたいです。

## Material Designとは？

正確には上長から「ちょっと、デザインシステム作ってよ」と言われたのですが、調べてみると、UIを実装するためのコードも用意してあったりと、とうていデザイナー１人で作れるようなものではないです。事実、デザインシステムまわりではDevOpsにちなんで[DesignOps](https://www.designbetter.co/designops-handbook)エンジニアなんて職種もあるとか。

それならば、すでにあるものを利用しよう！ということで、Material Designについて説明します。

[![Material Design](/mol/images/2019/0723/03.png)](https://material.io/)

Googleさんが作っているデザインシステムですね。良さそうです。カスタマイズ可能ということで、[Material Theme Editor](https://material.io/tools/theme-editor/)というSketchのプラグインを公式で配布しております。

{{< youtube IaT4wdWTwuo >}}

Themeについては今年のGoogle IOで良いセッションがありました。

![Material Theming: Build Expressively with Material Components 01](/mol/images/2019/0723/04.png)

どうせTheme Editorで作るもんなんて、どれも色違いの金太郎アメみたいなもんでしょ？と思われるかもしれません。たしかに、そういった事例が多くありました。

![Material Theming: Build Expressively with Material Components 02](/mol/images/2019/0723/05.png)

でも、Theme Editorうまく使えば、[上記のような](https://material.io/design/material-studies/about-our-material-studies.html#usage)ユニークなUIのアプリを作成可能です。

![Material Theming: Build Expressively with Material Components 03](/mol/images/2019/0723/06.png)

結局のところ、重要なパラメーターというのは3つしかありません。タイポグラフィとシェイプと色をうまく組み合わせれば、差別化というのは可能なのです。

![Theme Editor](/mol/images/2019/0723/07.png)

もちろん、Sketchのプラグインでこれらのパラメーター変更可能で、変更すると即座に数百のコンポーネントに適用され利用可能です。

![Sketch](/mol/images/2019/0723/08.png)

## Wとは？

というわけで、Material Theme Editorを利用すれば、弊社オリジナルのデザインシステムが作れそうです。

弊社の業務内容的に、既にプロダクションで稼働しているサービスを開発・運用しているわといったわけでなく、さまざまなプロジェクトでPoC検証のモックアップを作ることが多いです。というわけで、このプロトタイプのためのデザインシステムが必要とされています。

ブランドコンセプトなど固まってない、とりあえず動かしてみまひょか？という段階なので、毎回、色をどうするか？とかボタンの形状をどうするか？とか、そうゆうことで迷っていても仕方がないのです。どのPoC検証プロジェクトも同じデザインシステムで作成すれば、前述のようなメリットがあります。

### Design Principles

- 最小表現で作る
- 最短時間で作る
- 最小コストで作る

そうゆうわけで、このプロトタイプのためのデザインシステムの原則というものも弊CXOに考えてもらいました。

はい、この原則をまっとうできるよう、がんばります。

### Perceptual Patterns

弊社では、デザインツールはSketchではなく、Figmaを使用してるので、一回SketchのMaterial Theme Editorで作成したファイルを移行しています。

![Perceptual Patterns](/mol/images/2019/0723/09.png)

認知パターンに関しては、Figmaに[Shared Style](https://help.figma.com/article/187-styles-managing-and-sharing-styles)という機能があるので、これで共有しています。

### Functional Patterns

![Functional Patterns](/mol/images/2019/0723/10.png)

機能パターンに関しては、とりあえずプロジェクト毎に必要になったらコンポーネントを追加していくっていう方向でやっているので今のところ少ないです。元の生成されたSketchファイル見ると分かるのですが、ほんと職人芸のような複雑なコンポーネントになっていて、ちょっと理解できないし、私たちの使用目的からみれば、オーバースペックなので。

## Shared Language

[![Shared Language](/mol/images/2019/0723/11.png)](https://material.io/develop/)

Material Designベースで作成する最大のメリットと言ってもいいのは、そのUIを実装するためのフレームワークが用意されていることです。

![MDC Web 1](/mol/images/2019/0723/12.png)

例えば、Webで言えば、[Material Components for Web](https://github.com/material-components/material-components-web)のJSとCSSを読み込んで、`mdc-button`というclass属性を与えるだけで、マテリアルデザインの見た目のボタンを作成することができます。一行もスタイルを実装するためのCSS書いてません。

![MDC Web 2](/mol/images/2019/0723/13.png)

また、われわれのデザインシステムは青基調としていてフォントもNoto Sans JPを使用しています。この変更に対応をするには、Sassの変数を変更する必要があります。ここでも色とタイポグラフィとシェイプの変数を変えるだけです（実際はもっと多くの変数がありカスタマイズ可能）。

このようなデザイントークンは一つのファイルにまとめて、[Theo](https://github.com/salesforce-ux/theo)というツールで各プラットフォーム向けにエクスポートすることも可能です（FigmaでやってるのでAPIで変更感知して自動ビルドしたい...）。

---

このようにMaterial Designベースのデザインシステムを採用することで、デザイナーもエンジニアも、UIからコードまで一貫した恩恵を得られることができます。

というわけで、取っ掛かり的にはいいんじゃないでしょうか。




