---
date: 2012-10-17
title: CSScomb
subtitle: Makes your code beautiful
categories: 
    - development
excerpt: うららかに晴れた秋の日、みなさんいかがお過ごしか？こんちわ @t32k だ。
ogimage: https://t32k.me/mol/images/2012/10-17-csscomb.png
---

![](/mol/images/2012/10-17-csscomb.png)

うららかに晴れた秋の日、みなさんいかがお過ごしか？こんちわ@t32kだ。

今日は[CSScomb](http://csscomb.com/)ってツールの紹介だよ。タネマキであった[こもりさん](https://twitter.com/cipher)のSublime Text2勉強会のときに知ったんだけど、 まぁCSSプロパティを綺麗にソートしてくれるって代物だ。大まかな機能はこんな感じ。

+ CSSプロパティのソート
+ ソート順は設定可能
+ style要素、style属性もパース
+ スタイルシートのフォーマットは変更しない
+ CSS2,3,4も完全にサポート


[オンラインからでも使える](http://csscomb.com/online/)し、Sublime Textだけじゃなくてメジャーなテキストエディタだったら、たいていの[プラグインは用意されている](https://github.com/csscomb)んだ。

便利なものがあるなーと思ったけども、Sassファイルでこのツールを実行すると、[その時はバグっていて](https://twitter.com/t32k/statuses/224069764396498944)、単純にプロパティ順を綺麗にさせるためだけなのに、そんな致命的なバグの危険性（CSSが壊れる）とかマジ勘弁！などと思ったけど、あれから3ヶ月、俺もCSScombも成長したんだ。その話を聞いてくれ。

## SassとCSScomb

まずは、Sass文法をうまく理解していなかった点。Tests を見てくれ。見てごらん綺麗な緑色してんだろ。これテストに合格してるんだぜ…ってことで、Sass関連のテストも今じゃパスしてる様子。@includeが消えたりするバグも僕の方でも確認できていない。YOSHI 合格だ。

ちょっとReal Filesでwarningがあるみたいだけど、Sassのパーシャルファイルとか見通しのよいファイル単位でCSScombしてあげれば問題があってもすぐ気づけるからまぁそこまでも気にしなくてもいいかなと思っている。

## gzipとCSScomb

次に、CSSプロパティのソートは自己満足か？ってこと。基本コードは綺麗なほうがいいに決まってるけどそれがユーザーに対してなんかしらのメリットがないと、どーも後押しが弱いなって感じです。順番ぐらいそこまでひどくない限り、特に問題になることもないと思う（よっぽど書き散らかしたときは別だけど）。そう思ってた時代も僕にはありました。まずはこちらをご覧いただきたい。2

+ [gzip圧縮のしくみ · t32k/speed](https://github.com/t32k/speed/blob/master/articles/gzip.md)

gzipってテキストファイルとかを圧縮する技術なんですが、これサーバー側の設定をちょいちょいとするだけの割りにはなかなかナイスーな効果を発揮してくれるパフォーマンス対策のひとつでもあります。

これの仕組みなんですけど、要は同じような文字列を探してひとまとめとして考えるみたいなんですね。参照リンクの例ではそれぞれ別のhnタグと全部同じのdivタグの場合だと未圧縮の状態ではhnタグのほうが少ないバイト数ですが、gzip圧縮するとdivタグのほうが少ないバイト数になるんですね。divのまとまりがひとつとしてみなされてるみたいな感じですかね。

これはHTMLの例ですが、CSSの場合も同じような文字列がでてきますよね。たいていどのセレクタもmarginとかpaddingとかwidthとか含んでいます。こーいったプロパティの順番がセレクタごとにバラバラだったら同じような文字列としてカウントされないのでgzip圧縮効率も悪いんじゃねーの？って話です。

試しに、Apple Storeのbase.cssで実験してみましょう。別にApple StoreのCSSが汚いって言ってるわけじゃなくてある程度分量があったから良いサンプルかなと思ったのです。

![](/static/blog/2012/10/b4.png)

素のbase.cssとCSScombをかけた奴。もともとminifyされてるから綺麗になったかどうかわかんないけど多分ソートされたのでしょう。なぜかCombしたほうがファイルサイズが大きくなってますが、重要なのはgzipされた状態でのサイズです。

![](/static/blog/2012/10/a5.png)

はい、これをgzipコマンドにかけてみるとどーでしょう！わお、400バイトほど軽くなってるじゃないですか！うそーまじー！！

はい。

gzip圧縮を想定してない場合意味ないとか、たった400バイトとか…そういった意見もあるかもしれないけど、ボタン1発でできるのならやったほうがいいよねと僕は思います。別に毎回やる必要もないし、ほんとデプロイの時に最後のひと手間かけてやるだけなんでみなさんもどーですかね。まさしくお出かけ前のCombですね。