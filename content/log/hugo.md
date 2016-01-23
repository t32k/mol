---
date: 2015-01-16T09:44:52-08:00
title: JekyllからHugoへ
subtitle: Hugo - A fast and modern static website engine
excerpt: JelyllからHugoにブログシステムを移行しました。
categories: 
    - blog
ogimage: /mol/images/2015/0115-00.png
---

これまでJekyllを使ってブログを書いてたけど[Hugo](http://gohugo.io/)に移行したという話。[Frontend Weekly Vol.0](/mol/log/frontend-weekly/)で知ったんだけど、これ見ていいなーって思ったのでやってみた。

+ [OctopressからHugoへ移行した | SOTA](http://deeeet.com/writing/2014/12/25/hugo/)


## これまでのブログ遍歴

+ __Blogger__  
　Webサービスを使うのはよいことだ。最初にはてなを使ってたら僕の人生変わってたかもしれない。
+ __WordPress + さくらサーバー__  
　僕は若かった。いったい誰が僕のことを責めれようか。いや誰もいない。
+ __Jekyll + GitHub Pages__  
　マークダウン最高w
+ __Hugo + GitHub Pages__  
　イマココ


## Jekyllのいやなところ

__遅い！__コレに尽きる。上記のように、7年ほどブログを続けていると記事数が450くらいになってた。`jekyll serve --watch`して、記事を変更しても体感的に10秒くらいで更新されるような状態だった。ほんの少しスタイル確認したいだけなのに何秒も待たされるのは本当にイライラする。限界だ。

あと、これは別にJekyllのせいじゃないけど、[僕の使ってたテーマ](http://incorporated.sendtoinc.com/)がRuby 1.9固定だったので、なんでブログ書く度にRubyのバージョンを変えなきゃいけないのか、本当にイライラする。限界だ。

## Hugoのすきなところ

[![Hugo](/mol/images/2015/0115-01.png)](http://gohugo.io/)

__速い！__コレに尽きる。ほぼリアルタイムで更新されるんじゃないかくらい速い。`hugo server --watch`したら、デフォルトでLiveReloadで更新されるのも地味に便利である。移行にあたって必要のない記事を捨てた結果、240記事になった。__0.2秒__未満で生成される。

```shell
$ time hugo
0 draft content
0 future content
240 pages created
0 tags created
12 categories created
in 119 ms

real	0m0.172s
user	0m0.367s
sys	0m0.108s
```

対して、同記事数の生成でJekyllは__2.5秒__!!  
Hugoとくらべて14倍時間がかかってる。

```shell
$ time jekyll build
Configuration file: _config.yml
            Source: .
       Destination: ./_site
      Generating...
                    done.
 Auto-regeneration: disabled. Use --watch to enable.

real	0m2.458s
user	0m1.826s
sys	0m0.323s
```

そんなわけで、やっぱりGolang製は速いなと。HugoはGoで書かれているけどHugoを使う分には別にGoを勉強する必要はない。`brew install hugo`でインストールして、Jekyllのようにマークダウンを書いていくだけだ。テンプレートの記法もJekyllに似てるので問題ない。

+ [Introduction to Hugo](http://gohugo.io/overview/introduction/)

あと、[Jekyllからの移行方法](http://gohugo.io/tutorials/migrate-from-jekyll/)も丁寧に記載されてるし、masterにPushするだけであとは[Wreckerでgh-pagesにPushしてくれるビルドステップ](http://gohugo.io/tutorials/automated-deployments/)も用意されているので非常に楽である。

問題はJekyllのような生態系が育ってないこと、痒いところに手が届かいない感じだろうか。まぁしかし、それって本当に痒かったのかと開き直れば問題ない。男は黙って記事を書くのみ。トライ&エラーを繰り返せば良いものができる。そのためにスピードは重要なのだ。

+ [t32k/mol](https://github.com/t32k/mol)

みなさんもよかったらどうぞ。
