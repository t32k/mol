---
layout: post
title: 色のスピード
categories:
- performance
- translate
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '4616'
  _aioseop_keywords: web performance, color
  _aioseop_description: 3秒間は必ずしも3秒とは限らない。私たちの時間感覚は、一見無関係に思える要因によって大いに歪められており、3秒間を5秒と感じたり、もしくは1秒と感じるのは容易なことだ。最終的に、ユーザーが私たちのサイトをどのくらい速いと感じるかが問題なので、各種統計情報に関係なく、私たちはユーザーの知覚に影響する外的要因について深く理解する必要性がある。
---
<p style="text-align: center;"><a title="Macro of sharpened colored pencils aranged in a circle by Horia Varlan, on Flickr" href="http://www.flickr.com/photos/horiavarlan/4268864706/"><img class="fig aligncenter" src="/static/blog/2010/12/color.jpg" alt="Macro of sharpened colored pencils aranged in a circle" width="470" height="260" /></a><strong> <span style="font-size: x-small;"><span style="color: #888888;">By <a href="http://www.flickr.com/photos/horiavarlan/">Horia Varlan</a></span></span></strong></p>
色とWebパフォーマンスという奇妙な組み合わせの面白い記事を見つけたので紹介をば。

<cite>原文：<a href="http://timkadlec.com/2010/12/the-color-of-speed/">The Color of Speed | TimKadlec.com</a>
投稿日：2010-12-2 by <a href="http://twitter.com/#!/tkadlec">Tim Kadlec</a></cite>

3秒間は必ずしも3秒とは限らない。私たちの時間感覚は、一見無関係に思える要因によって大いに歪められており、3秒間を5秒と感じたり、もしくは1秒と感じるのは容易なことだ。最終的に、ユーザーが私たちのサイトをどのくらい速いと感じるかが問題なので、各種統計情報に関係なく、私たちはユーザーの知覚に影響する外的要因について深く理解する必要性がある。

<!--more-->

そのような1つの要因として色が挙げられる。様々な色相・明度・彩度は人間の体感時間に関わるすべてに影響する。一般的に、ユーザーが待ち時間の間にいかにストレスになっていたか、リラックスしていたのかと関係してくる。リラックスした状態になればなるほど待ち時間は短く感じられる。これは、ストレスを感じているユーザーがまるで遅いサイトと感じている一方で、リラックスしたユーザーは同じサイトだけれども反応が良いと感じる可能性がある。

それで、私たちはリラックした状態を色を使ってどのように引き起こしたらよいのだろうか？まず第一に、ユーザーの最もリラックスした状態を引き出すために青系の色を選ぶことができる。対照的に、黄、赤系の色は刺激を与えるので、ストレスにつながる。特に赤色は逃避や失敗といった感情を引き起こし、さらに強いレベルでのストレスとにつながる。

他の考慮すべきこととして、彩度が挙げられる。低彩度な色を見たユーザーは高彩度を見たユーザーよりもリラックスした状態が観察された。この効果は、コントラストが強い環境（コンピュータ画面のような）において、より顕著になる。

最後に、明度について私たちは考えなければならない、パステルカラー（高明度）はリラックスした状態をもたらすので、低明度（暗い色）な色よりも体感時間を短くすることができる。

これらの知識を使えば、私たちは本質的に速さをほのめかすデザインができ、反応のよい体験をユーザーに提供できる。決して、これはサイトのパフォーマンスをチューニングする作業に置き換わるものではない。しかしながら、もしこれらの知識をパフォーマンス最適化の技術と一緒に利用すれば、実測値と同じくらい速く感じるサイトを作成可能で、ユーザーの体験をより最適化できるだろう。

<span style="color: #888888;">-- 翻訳ここまで --</span>

実験データなどの参照元が明記されてなかったので、鵜呑みにするのはちょっと抵抗ありますが、本文自体も、あくまで色だけで速くできるのではなく、HTTPリクエストを減らすとかそういった基本的なパフォーマンス対策をおこなった上でのさらなる対策として提示していますので、青色にしたからといって万事OKなわけではありませんｗ

色とスピードに関しては、Yahoo!のエンジニアでパフォーマンスについても講演している <a href="http://twitter.com/#!/stoyanstefanov">@stoyanstefanov</a> もブログで以下のようなことを記述しています。
<blockquote>
<h3>White is fast</h3>
Google Reader used to have this blue background on the left hand side menu (where the list of feeds is), but it's now white. Turns out they made a user study to ask people what they think given the two options and nothing else changed in the app. People consistently said that the version with the white background was faster, although it's the same page. How crazy is this?

<span style="font-size: x-small;"><a href="http://www.phpied.com/psychology-of-performance/">Psychology of performance / Stoyan's phpied.com</a></span></blockquote>
Google Readerで青背景から白背景に変更した例を挙げています。なぜ白い色にしたのかというとユーザーが白色のほうが速いと感じたからそうです。青系の色はリラックスさせるのでパフォーマンス的に有効だと翻訳した記事には書いてありましたが、まぁ白色は明度は高いですし、背景以外のバーなど青色基調ですし、理にかなっているかなと思います。

そうでなくても、Googleは全体を通して白地にブルーのイメージがあります。あ、<a href="http://t32k.me/mol/2010/10/facebook-and-flow/">速いと噂の Facebook</a> もそういえば青色基調ですね。彼らはそういった点も気づいているのかもしれませんね。

個人的な考えを述べるのであれば、Webパフォーマンスは数年前と比べて改善されてきています。以前はサイトの応答速度の8秒ルールといったものがありましたが、現在では4秒、3秒といったことが言われおり、どんどん0に近づいてきています。つまり、これ以上ない限界が見えはじめてきた現在では、他のサイトとパフォーマンス（秒数）を競いあっても数百、数十ミリ秒の違いしか出せなくなってきています。そういった面からみれば、こういった人間の心理・知覚から考えて差別化するのも重要なパフォーマンス対策になってくるのかなと考えます。（この辺に関しては、こちらを参照：<a href="http://t32k.me/mol/log/long-life-web-performance-optimization/">心理学から考えるWebパフォーマンス</a>）

そうゆうわけで、Webデザイナーさんは制作しているサイトのブランドイメージにこれらの知識が応用できるのであれば採用すれば良いと思いますよ。（ブランドイメージをねじ曲げてまで対応する必要はないと思いますけど）
