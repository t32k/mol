---
date: 2019-05-17
title: display=swapとはなにか
subtitle: Google Fonts is Adding font-display
categories: 
    - css
excerpt: 最近はCSSもなにもコードを書いていないので、世間に疎くて困るのでリハビリする
ogimage: https://t32k.me/mol/images/2019/0517-01.png
---

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Shipped! <a href="https://twitter.com/googlefonts?ref_src=twsrc%5Etfw">@GoogleFonts</a> now let&#39;s you control web font loading using `font-display`. Say hello to the `display` parameter 🎉<br><br>What&#39;s font-display? <a href="https://t.co/Q7RDeESwkm">https://t.co/Q7RDeESwkm</a> <a href="https://t.co/sn27ySza1B">pic.twitter.com/sn27ySza1B</a></p>&mdash; Addy Osmani (@addyosmani) <a href="https://twitter.com/addyosmani/status/1128548064287952896?ref_src=twsrc%5Etfw">May 15, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Google I/0 2019に参加してきたのだが、Google Fontsが`font-display: swap;`に対応するとかで盛り上がってるのを横目で見てた（5/15の時点で対応済とのこと）。

最近はCSSもなにもコードを書いていないので、世間に疎くて困るのでリハビリする。

![](/mol/images/2019/0517-00.png)
図出典：[Font-display playground](https://font-display.glitch.me/)

例えば、`Roboto`のフォントがローカルシステムにないとき、ブラウザはテキストを不可視代替フォントで描画する（つまり何も読めない）。これを**ブロック期**という。

次に**スワップ期**という
ローカルにある代替フォントで描画する段階に移るのだが、テキストが何も表示されない状態が見えてしまうので、これを**FOIT(Flash of Invisible Text)**という。

`Roboto`が読み込まれていれば、すぐさまそのフォントにスワップするという算段だ。
またこのとき、代替フォントからWebフォントに切り替わるので、**FOUT(Flash of Unstyled Text)**という現象が起きる。

また、もしWebフォントが読み込みに失敗すれば、それは**失敗期**という段階で、そのまま代替フォントを使用する。

[![](/mol/images/2019/0517-01.png)](https://caniuse.com/#search=font-display)

この段階をコントロールするのが、`font-diplay`プロパティで、`@font-face`内に記述する。Linkタグで読みこむGoogle Fontsはこの部分の記述をカスタマイズできなかったが、今回の発表の`display=swap`のようにURLパラメーターで指定できるようになった。

```
https://fonts.googleapis.com/css?family=Roboto&display=swap

@font-face {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  font-display: swap;
  src: local('Roboto')....
}
```

では、`font-diplay`を指定しなかった場合は、どうなっていたのだろうか。それは`auto`となり、各ブラウザの挙動に任せられるのだが、下記のような状況とのこと。

![](/mol/images/2019/0517-02.png)

図出典：[ウェブフォントの最適化 | Web Fundamentals | Google Developers ](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/webfont-optimization?hl=ja)

大方のブラウザは3秒をタイムアウトに設定している。つまり、Webフォントの読み込みに3秒以上かかれば、テキストが表示されない状態（ブロック期）が3秒も続くということだ。

これでは文章が読めなくて困るので、`font-display: swap;`にすることで、ブロック期を0秒にできる。ブロック期がない最初からスワップ期なので、ローカルにある代替フォントで表示してくれる。つまり、読める、読めるぞ、文章が！

だいたいの場合において、この指定はよいと思う。特に当ブログでは日本語フォントである`Noto Sans JP`をGoogle Fontsから読み込んでいるので、ダウンロードに多くの時間を必要とするだろう。

ただ、代替フォントからWebフォントに切り替わるときのFOUTのちらつきはいかんせん起きてしまう。FOUTが嫌な場合は`font-display: optional;`を指定するのも良いだろう。これを指定すると非常に短いブロック期（ほとんどの場合100ms以下が推奨）の後に、スワップ期が0秒になる。つまり、100msくらいでWebフォントを読み込めなければ、そのまま代替フォントで表示したままになる。まぁ、FOITを最小限に防ぎつつ、Webフォントがあればよいといった感じかな。

```
https://fonts.googleapis.com/css?family=Roboto&display=optional

@font-face {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  font-display: optional;
  src: local('Roboto')....
}
```

もちろん、Google Fontsのパラメータを`optional`に変更すれば対応してくれる。

そんなわけで、良いリハビリになった( ˘ω˘)






