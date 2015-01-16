---
date: 2012-10-18
title: CSSOとgrunt-csso
categories: css
---
<a href="http://css.github.com/csso/"><img class="aligncenter size-full fig" title="CSSO" src="/static/blog/2012/10/csso.png" alt="" width="520" height="260" /></a>

読書の秋、ご勉学の方はいかがでしょうか。 I'm your <a href="https://twitter.com/t32k">@t32k.</a>

今日は__<a href="http://css.github.com/csso/">CSSO (CSS Optimizer) – A CSS minimizer unlike others</a>__の紹介だ。<a href="http://t32k.me/mol/log/csscomb/">前回のCSSComb</a>は単純にプロパティのソートをしてくれるものだったが、今回のはminimizerだ。

普段はSassの:compressed出力で最後デプロイしてるんだけど、もっとマシなものはないかなーと特には探してはないけど、<a href="https://twitter.com/cssradar">@cssradar</a>パイセンがCSSOがいいって言ったとか言わないとかあったので調べてみた。

ちなみにSassの:compressedはこんな感じで出力しているらしい。
<blockquote>Compressed style takes up the minimum amount of space possible, having no whitespace except that necessary to separate selectors and a newline at the end of the file. It also includes some other minor compressions, such as choosing the smallest representation for colors. It’s not meant to be human-readable.
<p style="text-align: right;"><a href="http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#id17 ">http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#id17 </a></p>
</blockquote>
改行とか空白とか色の値変換ですかね。まぁ特にそんな凝ったことはしてない模様。

## CSSOとYUI Compressor

CSSのminimizerとして有名というか古くからあるのは<a href="https://github.com/yui/yuicompressor">YUI Compressor</a>ですね。JavaScriptのminimizerとして有名ですがCSSも縮小化できます。んで、それよりもCSSOは良いってゆうもんだから、どのへんがいいのよ？と思って、CSSOの縮小化ルールを試してみた。

ちなみに、YUI Compressor's CSS minifierのルールに関しては<a href="http://developer.yahoo.com/yui/compressor/css.html">ここに書いてあった</a>。

どちらもオンラインで試せるデモツールがあったので、 <a href="https://github.com/css/csso/blob/master/MANUAL.en.md">CSSOのマニュアル</a>に書いてあるサンプルを両方のツール試してみた。

+ __YUI Compressor DEMO: <a href="http://tools.w3clubs.com/cssmin/">http://tools.w3clubs.com/cssmin/</a>__
+ __CSSO DEMO: <a href="http://css.github.com/csso/csso.html">http://css.github.com/csso/csso.html</a>__

ちなみに訳してみた。

+ <a href="https://github.com/css/csso/blob/master/docs/description/description.ja.md">csso/docs/description/description.ja.md at master · css/csso · GitHub </a>


### 基本的な変換

+ ホワイトスペースの削除
+ 最後尾の ';' の削除
+ コメントの削除
+ __不正な @charset と @import 宣言の削除__
+ __color プロパティの縮小化__
+ __ゼロの縮小化__
+ __複数行文字列の縮小化__
+ __font-weight プロパティの縮小化__


### 構造的な最適化

+ __同一セレクタブロックのマージ__
+ __ブロック内の同一プロパティのマージ__
+ __上書きされたプロパティの削除__
+ __上書きされたショートハンドプロパティの削除__
+ __繰り返されているプロパティの削除__
+ __ブロックの部分的なマージ__
+ __ブロックの部分的な分割__
+ __空のルールセット、ルールの削除__
+ __margin と padding プロパティの縮小化__

太字になっているのがCSSOでできて、YUI Comoressorでは縮小化できなかったもの。colorプロパティの縮小化はYUIも一部できるとこはあったのですが、CSSOのほうが優秀でした。

CSSOが他のminimizerとどのへんがunlikeなのかというと、上の対応表を見てもらうと分かるように__構造的な最適化（Structural optimization）__が出来るということですね。他のminimizerは基本的にホワイトスペースの削除といったものがベースですが、CSSOはそれだけでなくスタイルブロックのマージや分割といったアグレッシブなこともしてくれます。

さて、ほんとにこのCSSOはイケてるのか試してみましょう。

このブログのCSSをminifyしてみた結果が以下。

+ [http://t32k.me/mol/wp-content/themes/quickchic/style.css](http://t32k.me/mol/wp-content/themes/quickchic/style.css)

<p style="text-align: center;"><a href="/static/blog/2012/10/filesize.png"><img class="aligncenter  fig" title="Size" src="/static/blog/2012/10/filesize.png" alt="" width="500" height="225" /></a></p>
元が14Kあるのに対して、CSSOでmiifyしたほうが8,979 byteで、YUIの9,342 byteよりも400byteほど軽くなっています。うん、素敵！

## grunt-csso

んで、CSSOはCSSCombみたいにテキストエディタでのプラグインが配布されていない、くまったです(･ω･)。毎回コマンドライン打つのもめんぞい。そんなところに最近、<a href="http://havelog.ayumusato.com/develop/others/e495-grunt_initialize.html">同僚さんがgruntエバンジェリスト</a>なので、ついついそそのかされて<a href="https://npmjs.org/package/grunt-csso">grunt-csso</a>なるものを作ってみました。これで、Gruntfile(grunt.js)に設定しておけば、簡単にminifyできますね。
