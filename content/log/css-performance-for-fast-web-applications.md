---
date: 2009-12-04
title: 高速ウェブアプリのためのCSSパフォーマンス
subtitle: CSS Performance for Fast Web Applications
categories: 
    - development
excerpt: 3000以上にも昇る大規模サイトの最適化に携わって来た Nicole Sullivan は、現在 Yahoo! のパフォーマンスエンジニアと最適化のエバンジェリストとして国内外のセミナーで講演。Webサイトに関する研究だけでなく、プロジェクト管理もこなすマルチタスクなリーダーシップを発揮。フロントエンドエンジニアとしての高いスキルを持つ。
ogimage: https://c1.staticflickr.com/3/2714/4103194252_f450e74618_b.jpg
---

<a href="https://www.flickr.com/photos/t32k/4103194252" title="Nicole Sullivan by Koji Ishimoto, on Flickr"><img src="https://c1.staticflickr.com/3/2714/4103194252_f450e74618_b.jpg" alt="Nicole Sullivan"></a>


+ [Web Directions East | カンファレンス：11月13日（金）](http://east.webdirections.org/wde/2009/program/)


## Nicole Sullivan（ニコール・サリバン）

3000以上にも昇る大規模サイトの最適化に携わって来た Nicole Sullivan は、現在 Yahoo! のパフォーマンスエンジニアと最適化のエバンジェリストとして国内外のセミナーで講演。Webサイトに関する研究だけでなく、プロジェクト管理もこなすマルチタスクなリーダーシップを発揮。フロントエンドエンジニアとしての高いスキルを持つ。

+ [Stubbornella](http://www.stubbornella.org/content/)
+ [Nicole Sullivan (@stubbornella) | Twitter](https://twitter.com/stubbornella)
+ [Nicole Sullivan presentations | SlideShare](http://www.slideshare.net/stubbornella)


## 高速ウェブアプリのためのCSSパフォーマンス

### UNDERSTANDING THE CASCADE

デフォルトのスタイルがブラウザ毎で存在しそれは全て違う YUIのrecet.cssを使うと良い

クラスの順序に違いはない プロパティと値の順序 スペルミスはエラーにならない（無視されるだけ）

```css
color: red,
colour: blue
```

スタイルの順序

```css
.foo {color: red;}
.foo {color: blue;}
```

この場合、blueが勝つ

```html
<link rel="stylesheet" href="styles.css">
<link rel="stylesheet" href="moreStyles.css">
```

+ この場合、moreStyles.cssの方が勝つ
+ 同じ詳細度なら最後に出てきた方が勝つ
+ 詳細度は速く計算される必要がある

IDとクラス

```css
#nav p {color: red }
.nav p {color: blue }
```

INLINE STYLES

```html
<p style="color: green;">My page</p>
```

!IMPORTANT

```css
p { color: red !important; }
```

```html
<p style="color: green;">My page</p>
```

この場合、redになる

継承

```css
body { font-size: 18px; }
```

```html
<body>
  <p>This text is 18px.</p>
</body>
```

P要素も18pxになる

うまくいかなかったらスパゲッティコードになってしまう

CSS IS AWESOME

コードは脆い、人が変われば壊されてしまう、熟練度が必要、コードの再利用はほとんどない、人の書いたコードは信用しない、ファイルサイズが増大していく、修正を繰り返していけばどんどん増える

### HOW TO ARCHITECT GOOD CSS?

Object Oriented CSS

プロパティではなくセレクタに注目する

用語の使い方に注意する（ex.クラスって何よ？）

+ [Home · stubbornella/oocss Wiki](https://github.com/stubbornella/oocss/wiki)

見出しについて デベロッパーじゃデザインの意味が分からない

再利用はパフォーマンスに良い

冗長性は避ける 似たようなものはまとめろ

ロケーションの依存性を避ける

```css
#weatherModule h3{color:red;}
#tabs h3{color:blue}
```

本当に必要なのか考える

+ [Reflows & Repaints: CSS Performance making your JavaScript slow? | Stubbornella](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)

CSSパフォーマンスで重要なのはCSSファイルのサイズとHTTPリクエスト数 リフローとレンダリング時間は大した問題ではない


+ Toggle classes as low in the dom tree as possible
+ Avoid setting multiple inline styles
+ Apply animations to elements that are position fixed or absolute
+ Trade smoothness for speed
+ Avoid tables for date
+ Avoid JavaScript expressions in the CSS (IE only)

### Apply programming best practices to style sheets

デフォルト値を設定する

```css
×　#tabs h3{color:blue}
```

クラスに構造を定義する

```css
×　div.error{…}
```

要素にスタイル付けしない

```css
×　p{..}
```

同じ詳細度にする

セレクタによるハックは控えめに

```css
×　.ie .mod .hd{…}　→　.mod .hd{_zoom:1;}
```

ロケーションによる詳細度の指定は避ける

```css
×　.sidebar ul{…}
×　.header ul {…}
```

過度に特定なクラス名は避ける

```css
×　.niXcolesDucatiMonster620{…}
```

シングルトンは避ける（IDは避ける）

```css
×　#myUniqueIdentifier{…}
```

ミックスインを使う

```html
○ class="media" class="media extended"
```
カプセル化 オブジェクトのサブノードにアクセスさせない

## セッション感想

前半はCSSの基礎的なことでだったので、エンジニアさんにCSSを説明するときに便利だと思った。全体としてはOO（オブジェクト指向）CSS入門のようなセッションで、複数人でのコーディング、修正の多い大規模サイト運用において、どのようにCSSのパフォーマンスを発揮していくのかといった内容だった。

まさしく大規模サイトにOOCSSは最適だと思う。ただ、OOCSSを導入するにあたっては既存のCSSでマークアップしたページとの兼ね合いを考えると難しいものがある。CSS自体、スパゲッティコード（ごちゃごちゃになったコード）化しやすい傾向もあって、使用していない/しているコードの把握、CSSのコードを設計するために現在どのようなデザインエレメントが存在するのか調査・カタログ化、デザイン部内のコーディングルールの周知などを既存のコードを運用しつつ考えれば、かなりのリソースが割かれるのは確実だ。

逆に、Webデザイナー1人で管理できるレベル程度の小規模サイトではOOCSSのメリットはあまり享受できないかもしれない。いや、でも修正に修正重ねていったら使わないコードが増えていくのかもしれない。

結局、OOCSSの理念としてCSSコード量をむやみに増やさないというところに重きが置いてあるのかなと理解した。
