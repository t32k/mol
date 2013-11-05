---
layout: post
title: WebPagetest in 5 minutes
subtitle: Frontrend x Chrome Tech Talk Night Extended
categories: performnace
status: publish
type: post
excerpt: "10/30にCAで行われたFrontrend x Chrome Tech Talk Night ExtendedでWebPagetestでライトニングトークしてきたのでメモしておく。"
cover_image: /2013/11-06-cover.jpg
---

<script async class="speakerdeck-embed" data-id="2194dea0233401314f283ee30ec95e6c" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>

+ [WebPagetest in 5 minutes // Vimeo](https://vimeo.com/78323495)
+ [WebPagetest in 5 minutes // Speaker Deck](https://speakerdeck.com/t32k/webpagetest-in-5-minutes)

## WebPagetest

2013年10月30日にサイバーエージェントで行われた[Frontrend x Chrome Tech Talk Night Extended](http://frontrend.github.io/events/chrome/)でWebPagetestでライトニングトークしてきたのでメモしておく。

公式サイトにはAddyやJake、Paulの動画も既に公開されている。しかも通訳付きなので参加できなかった方もぜひ見てほしい。

さて、今回紹介する[WebPagetest](http://www.webpagetest.org/)だが、いまいち日本で人気のないようだから紹介してみる。

私の仕事はWebパフォーマンス改善のタスクを主な業務としている。弊社がリリースしているWebアプリで遅いことが確認されるとその原因を調査する。その時に使うツールがChromeの拡張機能の[PageSpeed Insights](https://chrome.google.com/webstore/detail/pagespeed-insights-by-goo/gplegfbjlmmehdoakndmohflojccocli)と、WebPagetestだ。PageSpeedはサクッと調べたい時に使い、WebPagetestを腰を据えてじっくり調べたい時に使う。今回紹介するのはWebPagetestのほうだ。

+ [WebPagetest - Website Performance and Optimization Test](http://www.webpagetest.org/)

WebPagetestを使うには上記のサイトから、調べたいページのURLを入力して『START TEST』のボタンを押すだけだ。しばらくするとテスト結果画面が表示されるのでここからボトルネックを見つける。さまざまなオプションがあるが基本的な使い方はこの通りである。

WebPagetestはPageSpeed(DevTools)に似たような機能も提供しているが、多くの機能がある。First ByteやStart Render、DOM Elementsなどといった指標を取得することも可能であれば、Waterfall View、Connection View、FilmstripやScripted Testといったことも可能である。ここでは全部紹介しきれないのでWebPagetestの最も素晴らしい機能と言っても過言ではない__Speed Index__について紹介する。

## Speed Index

Speed Indexは、端的に言えば体感速度を指標化したようなものだ。

+ [Speed Index - WebPagetest Documentation](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index)

詳しくは上記のドキュメントを読んでもらいたい。簡単に説明するとページのVisual Progressというのがあって、文字通りページがどれだけ描画されているかの進捗度である。スライドのA：青とB：赤のVisual Progressだと、どっちが良いかは自明だろう。どちらも12秒ほどの読み込み時間がかかっているが、青のほうは、1秒の段階で90%ほど描画が完了しているのに対して、赤のほうは11秒くらいまで20%未満のVisual Progressだ。当然、青のほうが体感速度的には早いと感じるであろう。

Speed Indexというのはこの単位時間辺りのVisual Completeしていない度合いの総和である。つまり、Speed Indexは小さい方はがよりよいということである。

![](/mol/images/2013/11-06-fig.png)

上記の数式の意味は、0秒から読み込みが完了するまでのミリセカンド毎に、1からVisual Completeをひいたものを足した総和ということを意味している。

これにより、同じ読み込み時間であってもSpeed Indexを見ればどちらが良いのか判断できるようになる。

## Let's Improve Performance

ということで、試しにこれらのツールを使ってパフォーマンスを改善していく。改善対象サイトは[t32k.me](http://t32k.me/)、私のポートフォリオサイト。このページの改善前のPageSpeed Scoreは80点（ちなみに、PageSpeed Insightsの言語設定を日本語にしているとScoreが出ない）。このページのどこが重いのか、軽く見てみるとページ下部にソーシャルウィジェットを発見したので、これを取り除いてみることにする。

ソーシャルウィジェットを取り除いた改善後のPageSpeed Scoreは93点。やったね、たえちゃん！ってことで素晴らしい改善結果だ。

しかし、改善前後のWebPagetestの結果を見てみよう。Visual Progressはほぼ変わっていないし、Speed Indexはほぼおなじの3105だorz...

ここで言いたいことは、決してソーシャルウィジェットを取り除くことが意味のないことだということではない。事実、ソーシャルウィジェットを読み込んでいる方は当然、総読み込み時間は読み込んでいないものより長くなる。しかし、__体感速度__の改善という意味では効果のないことかもしれない。

> Speed is the second biggest engagement driver on the internet - just after perceived speed.  - [@maccaw](https://twitter.com/maccaw/status/380385677390516224)


この辺りの話題は最近のWeb Performance界隈ではホットな話題だ。PageSpeedで最低限のアドバイス（gzipしろとか）を達成した場合、次はどうすればいいのか？体感速度をどう速めるのか？そしてどうやってそれを計測するのか？


ちょうど[Velocity NY 2013で似たような話題を取り扱っていたセッション](http://velocityconf.com/velocityny2013/public/schedule/detail/31344)があった。そこでSpeed Indexはもちろん紹介されていたし、UserTimingでキーとなるビジュアルを設定し、そのレンダリング速度を計測するといった方法（この場合コンテキスト依存になるので自動化できない..）や、Microsoftの[PPT](http://programming.oreilly.com/2013/10/page-phase-time.html)（パワーポイントではない、Page Phaze Time）といった新しい概念もでてきている。要チェックやで！

[Paulのセッション](http://frontrend.github.io/events/chrome/#paul)の最後のほうで、Speed Indexは1000以下にするのは理想だとか言ってたような気がするけど、無理じゃね？

## Private Instance for Ameba

あ、そうそうWebPagetestはWebサービスとして使用するのが一般的だが、[オープンソース](https://github.com/WPO-Foundation/webpagetest)として公開されていて、自社のネットワーク上に[プライベートインスタンス](https://sites.google.com/a/webpagetest.org/docs/private-instances)を置くことも可能だ。なので、UIとかいじりまくりだぜ、ひゃっほーい♪

我々はWebPagetestを使いテストを自動的に実行し、各種指標を収集するといったことをやっていきたいと考えている。開発中だお(´・ω・｀)