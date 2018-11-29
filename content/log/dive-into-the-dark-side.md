---
date: 2018-11-30
title: Dive into the dark side
subtitle: I am your father.
categories: 
    - development
excerpt: 流行りに乗ってダークモードというものを私もやってみんとてするなり
ogimage: https://t32k.me/mol/images/2018/1130-00.png
---

![](/mol/images/2018/1130-00.png)

昔フロントレンドで、環境光の明るさによってCSS変えられたらおもしろいよね的なことを@simuraiが彼の作った[Atomのテーマ](http://simurai.com/projects/2016/01/01/duotone-themes)を解説しながら言っていた。環境光については@girlie_macが2014年に記事を書いていたので、CSSスゴイ！ほえー！と思ってた。

- [HTML5で実現できる！環境光に合わせたレスポンシブなUI | HTML5Experts.jp](https://html5experts.jp/girlie_mac/4558/)

media feature `luminosity`は`light-level`に名前を変えたが今も実装の気配なさそうだ。一方で、2018年、macOS Mojaveがリリースされ、ダークモードが利用できるようになった。自分も流行りに乗って自宅のMacで利用している。

- [Paul Miller — Using dark mode in CSS with MacOS Mojave](https://paulmillr.com/posts/using-dark-mode-in-css/)

そして、どうやらSafari Tech Preview 68からダークモードかどうかをCSS上検知できるようになってるらしい。

```
/* Text and background color for light mode */
body {
  color: black;
}

/* Text and background color for dark mode */
@media (prefers-color-scheme: dark) {
  body {
    color: white;
    background-color: black;
  }
}
```

環境光の変化に比べたら明示的だが、よりResponsiveなUIについて考える機会ができた。

- [prefers\-color\-scheme を用いた Dark Mode 対応と User Preference Media Features \| blog\.jxck\.io](https://blog.jxck.io/entries/2018-11-10/dark-mode-via-prefers-color-scheme.html)

ちなみに、`prefers-color-scheme`はMediaQueries Lv5のUser Preference Media Featuresという仕様らしい、カラースキームの他にも。コントラストの強弱、アニメーションの動きを減らすなどのユーザー設定をCSSから検知できる未来がくるかもしれない。その人のコンテキストに応じたデザインを今後考える必要性がある。


## 考慮すべきこと

個人的に、なにかをデザインするとき黒基調を選択した憶えがない。うまくやれば高級感・エレガンスさを醸し出せるが、下手を放けば、たちまちアングラ・いかがわしい感じになってしまうので難しい。そんなもので、あまりダークテーマについて考えたことがなかったからだ

- [Dark Side of UI. Benefits of Dark Background – UX Planet](https://uxplanet.org/dark-side-of-ui-benefits-of-dark-background-12f560bf7165)

上記の記事によれば、感情的な側面において、暗い色は一般的に優雅さやミステリーさを想起させる。またときには、エレガンスさ、フォーマルさ、荘厳・一流といったものをイメージさせる。それゆえ、多くの世界的なブランドは、モノトーンなプレゼンテーションを多用し、消費者にそれを知らせる。ゆえに、UIにおいてもこのような効果は期待できる。

[2009年のプロブロガー向けの投票](https://problogger.com/light-or-dark-blog-backgrounds-poll-results/)だが、ほぼ半数がライトテーマを好み、10%がダークテーマがブログデザインにおいて良いと答えた。また36%のユーザーはコンテンツ次第だとも答えている。

また、[Richard H. HallとPatrick Hannaの調査](http://lite.mst.edu/media/research/ctel/documents/LITE-2003-04.pdf)によれば、ポジティブテキスト（明るい背景で暗いテキスト）が、可読性のパフォーマンスが高いことが判明した。一方で、ネガティブテキスト（暗い背景で明るいテキスト）でも十分なコントラストがあれば、ポジティブテキストと同じくらい効率になる。

- [ブログのダークモード対応とその他リファクタリングなど - wadackel.me](https://blog.wadackel.me/2018/improve-design-and-refactor/)

コントラストにおいては、[WCAG 2.0](https://waic.jp/docs/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)によると`4.5 : 1` のコントラスト比があればよいらしいので、本ブログでもリンクの色を修正した。



## 実装

というわけで、ぼくも自分のブログをダークモード対応してみる。

[![](/mol/images/2018/1130-01.png)](https://caniuse.com/#search=custom%20properties)

当然だが、ライトモードとダークモードで２つの色のセットがある、セレクタ毎にそれらを指定していくのは大変苦労する。気づいたら2018年末、カスタムプロパティがほとんどのブラウザで対応している。やった！ということで、基本CSSでの色指定はカスタムプロパティを使用しモードの切替時に変数を上書きすることで、楽に管理できる。

- [Dark theme in a day – Marcin Wichary](https://medium.com/@mwichary/dark-theme-in-a-day-3518dde2955a)

上記のブログ主はHSL、色相（Hue）、彩度（Saturation）、輝度（Lightness)で色を管理している。色相を変数化することで、ダークモードでも複数のカラーパターンを実装している。なるほど、頭が良い。

しかし、私のブログは基本モノトーンなので、`#ddd`とか`#eee`といった似たようなグレーが無駄に多くあった。まず、それらを6種類のグレーに整理した。

また、[Material Design](https://material.io/design/color/text-legibility.html#legibility-standards)でも実装されているように、透明度を使ってグレーの濃淡を表現することにした。`#000000` は真っ黒だが、白地(`#FFFFFF`)の背景で、それの不透明度を60%にしたら、`#666666`相当のグレーを表現できる。

このようにベースとなる色と不透明度を変数を使って別途管理したいのだけど、16進数だと使い勝手が悪い。`#00000060`のようなアルファ値を含んだ[#rrggbbaa](https://caniuse.com/#feat=css-rrggbbaa)をサポートしているブラウザも増えているが、`"#000000"　+ "60"`のように文字列結合をCSSファイルで実現するのは難しい。

```
html {
  color: rgba(var(--rgb-surface), var(--alpha-600));
  background: rgb(var(--rgb-background));
}
```

ということで、rgba関数であれば上記のように色と不透明度を別々にvar関数を展開できて便利。

![](/mol/images/2018/1130-04.png)

このように色指定を変数と不透明度を利用することで、ダークモード時は、`--rgb-surface`の黒(0, 0, 0)を白(255, 255, 255)にするだけでほぼほぼ対応できる。

![](/mol/images/2018/1130-02.png)

あとは背景の色とかアクセントカラーとかを、お好みにあわせて変えるだけなので、カスタムプロパティ最高かよと思いました（小並感）。

![](/mol/images/2018/1130-03.gif)

今はSafari Technology Preview 68+だけの対応だけど、通常のSafariやChromeがサポートするようになったときに、購読してるブログがダークモード対応してたら、おっ！っとなるかもしれない。知らんけど( ˘ω˘)

