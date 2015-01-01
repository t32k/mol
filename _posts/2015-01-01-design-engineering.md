---
layout: post
title: 【翻訳】デザインエンジニアリング
subtitle: DESIGN ENGINEERING
categories: translation
excerpt: Design Engineering - Snook.ca
---

[SMACSS](https://smacss.com/ja)の提唱者であるJonathan Snook氏、翻訳にあたっては氏の同意を得ている。

<cite class="citation">
![Jonathan Snook](/mol/images/people/jonathan_snook.jpg)
原文：[Design Engineering](http://snook.ca/archives/opinion/design-engineering)（<time>2014-11-25</time>）by [Jonathan Snook](http://snook.ca/about/)
</cite>

> フロントエンド開発はJavaScriptだけではない。フロントエンド開発は人種のるつぼのようにデザインとディベロプメントの技術が融合したものである。それはアクセシブルなUIを実装するためであり、Web標準を受け入れるものである。— [Matt Hill](https://twitter.com/matthillco/status/480986847473303552)


Shopify Adminの開発に関して言えば、最近まで2つの専門職、つまりデザイナーとエンジニアを受け入れていた。しかしながら、今では3つめの専門職があり、that has had a tough time finding a solid home:フロントエンドデベロッパーである。フロントエンドデベロッパーのスキルというのはさまざまであり、エンジニアリング、デザインどちらにも融合している。クオリティの高いフロントエンドコードをフロントエンドデベロッパーの助けもなしに書けるデザイナーを雇えて、私達は非常にラッキーだった。

フロントエンドデベロッパーの精鋭チームの作り方の講演に関してはいくつかの反論がある。『もし彼らがデベロッパーであるのなら、そのとき彼らはエンジニアチームに所属している。』つまり逆を言えば、バックエンドデベロッパーはフロントエンドデベロッパーでもあるということである。Shopifyは彼らデベロッパーに対してフルスタックであることを期待している。しかし、フロントエンド開発が開発であるのなら、なぜ私達はデザイナーにもそれを求めないのか？

私達は__フロントエンド開発__と__バックエンド開発__という用語を使うが、人はフロントエンドデベロッパーが開発を始める段階とバックエンドデベロッパーが開発を終える段階をよく勘違いしていることが問題だ。

開発プロセスを考えてみれば、そこには3つの段階、デザイン（Design）、デザイン実装（Design Implementation）、アプリケーション開発（Application Development）が存在する。

![Spectrum of Application Development](/mol/images/2015/0105-01.png)

## デザイン

デザイナーは多くのツールを使い、彼らはデザインがどのように実装されているか理解すべきだが、HTML/CSS、JavaScriptを使って彼ら自身のデザインを実装する必要はない（ちょうど印刷デザイナーに印刷を任せる必要がないのと同じようにだ。なぜなら私達はプリンターを持っているから）。デザイナーが複数のデザインの試行錯誤に集中できる、もしくはデザイン的問題に本格的に取り組むことができることはアドバンテージであり、結果としてデザイン実装（デザインをプロダクト前段階のHTML/CSSに落としこむこと）に集中する必要性はない。

デザイナーはコードの書き方を知るべきと私は強く信じているが、組織の拡大によっては専門性を高める必要もあると述べたい。

## アプリケーション開発

アプリケーション開発とはインターフェースとサービングを最良の方法で繋げることである。私達はクライアントサイドMVCもしくはサーバーサイドレンダリングを使うべきか？キャッシュもしくはストレージシステムとは何か？データモデルとは何か？これらのタイプの関心はHTTPの境界線を超えて問題を抱えており、どちらか片方だけで考えるべきことではない。

複数ブラウザでのCSSプロパティのレンダリングと、複数のインプット、マウス、キーボード、ジェスチャーまたはスクリーンリーダーでアクセシブルでありつつ、複数の携帯端末、タブレット、またはデスクトップでベストな実装の仕方を理解することよりもOOPとプロトタイプ継承を理解することは異なるスキルセットを必要とする。

## デザイン実装

Implementing a design means writing HTML and CSS (and some JavaScript) and ensuring that the design holds up under the various design constraints: different browsers, different dimensions, different resolutions, and different interaction methods (mouse, keyboard, gestures, screen readers). It also can mean building out prototypes for UX validation. These people are design-minded but not necessarily designers. These people are technically-minded but not necessarily developers.

デザインを実装することはHTML/CSSといくぶんかのJavaScriptを書くことを意味し、
People in this role provide a great bridge between design and engineering. I’ve often called these people the “arbiters of design”. They inform design of possibilities and constraints and help ensure that designers build a consistent and usable interface for as many users as possible. They help codify the design work. They have a developer mindset with concerns about render performance and load times and can work with engineering to build out a performant front-end.



## 役割

It’s important that we have generalists that can bleed across these lines and specialists that can go deep in each of these sections. Up until a short while ago, we were not doing enough to foster the practice of design implementation within Shopify Admin. This has been affecting our designers’ ability to focus on design and affecting our ability to hire people due to our expectation of requiring generalists over specialists.

## 彼らをなんと呼べばいいのか？

“Could front-end translate as being design engineering?” — Dan Donald
We debated on what this role should be called. Design Implementorsfelt less than impressive. We almost settled on Design Engineers but it sounded a little too “Disney”.

We also already had a well-established team of front-end developers in Toronto focused on Shopify.com and other growth projects. Their needs were a little different than ours since their front-end developers bled more into backend development.


We also already had a well-established team of front-end developers in Toronto focused on Shopify.com and other growth projects. Their needs were a little different than ours since their front-end developers bled more into backend development.