---
date: 2021-04-21
title: Webフォント読み込み戦略（2021年）
subtitle: Avoid invisible text during font loading
excerpt: 目標をセンターに入れて、display=swap...
ogimage: https://t32k.me/mol/images/2021/0421/02.png?v2
categories: 
    - css
    - development
---

# Preload web fonts

前回、といっても2年前だが、[display=swapとはなにか](/mol/log/font-display-swap/)で、Google Fontsを読み込むときはURLパラメータに `display=swap` をつけるといいよと言った。というわけで、それ以降、『目標をセンターに入れて、display=swap...』と盲目的に考えるようになってた。

おさらいとして `display=swap` では、まず代替フォントを表示し、Webフォントをダウンロードしたら、随時スワップするという挙動になる。この場合、代替フォントからWebフォントへ切り替わる **FOUT (flash of unstyled text)** が起こってしまう。こんな感じ↓

![](/mol/images/2021/0421/00.png?v2)
出典：[font\-face descriptor playground](https://codepen.io/simonjhearne/pen/rNMGJyr)

まぁ何も表示されないよりかは良いかと思うわけだが、時は流れ、最近ではWebの指標として、[Web Vitals](https://web.dev/vitals/)というものがある。その中の[CLS](https://web.dev/cls/)（Cumulative Layout Shift）では、レイアウトの安定性というのも評価する。つまり、代替フォントからWebフォントへ切り替わる際のレイアウトのズレ・ちらつきが、このCLSを下げてしまう原因になる。

![](/mol/images/2021/0421/01.png?v2)
出典：[Fontastic web performance \- Speaker Deck](https://speakerdeck.com/notwaldorf/fontastic-web-performance?slide=74)

ということで、今回紹介する `font-display: optional` の場合はどうなるかだが、100msのブロック期までにWebフォントを取得できたらWebフォントを表示する、できなかったら代替フォントを表示するという分かりやすい挙動。

この場合、FOUTはないが、最初に100msのブロック期があるので不可視テキストが表示される **FOIT(Flash of Invisible Text)** が起こってしまう。

![](/mol/images/2021/0421/02.png?v2)

出典：[Prevent layout shifting and flashes of invisible text \(FOIT\) by preloading optional fonts](https://web.dev/preload-optional-fonts/)

と思っていたら、Chrome 83で改善が行われ、`<link rel="preload">` と一緒に使うことで、ブロック期に不可視テキストを表示せず、というかレンダリング自体をブロックして、100ms後に一気に表示することでレイアウトのカタツキを無くすことにしているようだ。


```html
 <!-- HTML -->
 <link rel="preload" href="NotoSansJP-Regular.woff2" as="font" type="font/woff2" crossorigin />
```


```css
/* CSS */
@font-face {
  font-family: 'Noto Sans JP';
  font-style: normal;
  font-weight: 400;
  src: local('Noto Sans JP'), url(NotoSansJP-Regular.woff2) format('woff2');
  font-display: optional;
}
```

こんな感じに、fontファイルをpreloadして、optional設定すれば、レイアウトジャンクなしにWebフォントを読み込める。

# Google Fonts

Google Fontsから読み込む場合の最善手については、CSS Wizardryさんが詳解な説明をしているので下記を読んでほしい。

- [The Fastest Google Fonts – CSS Wizardry – Web Performance Optimisation](https://csswizardry.com/2020/05/the-fastest-google-fonts/)

```HTML
<link rel="preconnect"
      href="https://fonts.gstatic.com"
      crossorigin />

<link rel="preload"
      as="style"
      href="$CSS&display=swap" />

<link rel="stylesheet"
      href="$CSS&display=swap"
      media="print" onload="this.media='all'" />
```

長いので要点は上のように設定すればよい。`$CSS` のところに自分の読み込みたいフォントのURLが当たる。まず最初に、woffファイルなどの配信元である`fonts.gstatic.com`に事前に接続しておく。

そいで、 `display=swap`でスタイルシートをpreloadしておく。

そいで、最後にGoogle Fontsのスタイルシートを設定するのだが、見慣れない記述がある。

```html
media="print" onload="this.media='all'"
```

ちょっまっ！印刷用CSSになってんじゃん！と思うじゃん。それでいい。ブラウザはこのCSSを印刷メディアのCSSだと理解して、現在のレンダリングと無関係に読み込み始める。これが狙いだ。そして読み込み終わったら現在のメディアに適用するといったことをしている。

- [The Simplest Way to Load CSS Asynchronously | Filament Group, Inc.](https://www.filamentgroup.com/lab/load-css-simpler/) 

これが一番簡単に非同期でCSSを読み込めるハックっぽい。`display=optional`ではないのは、この読み込み方と相性が悪いためだそうだ。

![](/mol/images/2021/0421/03.png)

というわけで、本ブログでもNoto Sans JPを読み込んでいたので、CSS Wizardryさんのやり方で読み込んだら大幅にPeformanceが改善した。これはCLS改善というよりCSSの非同期読み込みによる改善が大きな要因だ。CLS自体は`0.004 -> 0`になったので、まぁ、うん。。。

結局、色々調べた結果、t32kにはWebフォントは早すぎると感じたので、本ブログでのNoto Sans JPの読み込みを辞めた。うん、スッキリ。お後がよろしいようで。

### 参考資料

- [Prevent layout shifting and flashes of invisible text \(FOIT\) by preloading optional fonts](https://web.dev/preload-optional-fonts/)
- [Ensure text remains visible during webfont load](https://web.dev/font-display/)
- [Avoid invisible text during font loading](https://web.dev/avoid-invisible-text/)
- [Optimize WebFont loading and rendering](https://web.dev/optimize-webfont-loading/)
- [Reduce WebFont Size](https://web.dev/reduce-webfont-size/)
- [Web Font のメトリクス上書きによる CLS の改善 \| blog\.jxck\.io](https://blog.jxck.io/entries/2021-02-25/font-metrics-override.html)
- [WebFont の WOFF2 対応によるサイズ最適化 \| blog\.jxck\.io](https://blog.jxck.io/entries/2018-02-13/web-font-woff2.html)