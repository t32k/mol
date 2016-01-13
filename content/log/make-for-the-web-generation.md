---
date: 2015-05-20
title: 【翻訳】Web世代のデベロッパーのためのmake
subtitle: Make for the Web Generation
categories: translation
excerpt: makeなんてしらないおっさん向け。
ogimage: http://t32k.me/mol/images/people/casper_beyer.png
---

<cite class="citation">
![Casper Beyer](/mol/images/people/casper_beyer.png)
Original：[Make for the Web Generation
](http://caspervonb.com/javascript/tools/make-for-the-web-generation/)（<time>2015-02-28</time>）by [Casper Beyer](https://twitter.com/caspervonb)
</cite>

## イントロ

JavaScriptの普及に伴いビルドツールが盛んだ。人気なものをいくつか挙げれば、[grunt](http://gruntjs.com/)、[gulp](http://gulpjs.com/)、[slush](http://slushjs.github.io/#/)、[broccoli](https://github.com/broccolijs/broccoli)や[brunch](http://brunch.io/)などがあるが、結局、名前をつけただけにすぎない。

多かれ少なかれ、これらのツールはファイルコピーからzipファイル作成のようなシンプルなタスク処理でさえ、すべてプラグインに依存しているので、それらのタスクを実行するためにプラグインを必要とするだろう。

これらのツールは理想論的には大きな柔軟性をもたらすものとされているが、実際はUNIXのエコシステムをただ複製しているだけにすぎない。このために君のプロジェクトは早々に、大きな開発依存性のバンドルを持つことであろう、そして、やっているタスクは単なる普通のコピー、バンドルやミニファイだけだ。

## makeの導入

makeはとても古いツールであり、ネイティブ開発畑出身のほとんどのデベロッパーにとって古き良き友であるが、コンピューターサイエンス出身ではない多くのWebデベロッパーにとっては、それを使おうとさえ思いもしないだろう。しかし、だからといって、それはmakeが良いツールではないということを意味していない、事実、最近はあまりにも過小評価されているように思う。

君はすでにUNIXのエコシステムを持っている。パイプ、ストリーム、ユーティリティなどがすべてそこにある。ビルドする必要性のあるのツールのほとんどは、すでにそのエコシステムに存在している。もし、Windowsのような非UNIXのマシンで開発しているのなら、悪いことを言わないから適切なシェルと[gow](https://github.com/bmatzelle/gow/wiki)のようなバンドルをインストールするべきだろう。あるいは、`cmd.exe`も同様に[cmder](http://bliker.github.io/cmder/)のような、よりよいターミナル端末に置き換えべきだろう。

makeは一般的に`Makefile`と呼ばれるファイルで定義、使用し、拡張子は必要ない、大文字に気をつけること。ルールはターゲットと依存するファイルから成り、シェルコマンドも有しており、普通それらはレシピと呼ばれる。

一般的なルールは以下のような感じ。

```shell
ターゲット: 依存するファイル
    レシピ
# 注意！スペースじゃなくてタブ！
```

では、以上の知識を使って簡単な例をやってみよう。依存するファイルである`input.txt`をターゲットである`output.txt`にコピーしたい場合、レシピは以下の様なシンプルなコマンドラインとなるだろう。

```shell
output.txt: input.txt
	cp $< $@
```

とってもシンプルだろう？[cp(1)](http://linux.die.net/man/1/cp)の起動といくつかの[自動変数](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html)である、`$@`はターゲットのファイル名を保持し、`$<`は最初の依存するファイル名を保持する。

では、次はもっと実践的な例をやってみよう。


## コードのコンパイル

Coffeescript、Typescriptや、[babel](https://babeljs.io/)のようなJavaScriptトランスパイラーは最近では普通に使われているので、モダンなJavaScriptから現在のブラウザで解釈できるようなスクリプトにコンパイルする必要がある。

このルールを定義するには、`src`ディレクトリにあるファイルを変換し、トランスパイルしたファイルを`lib`ディレクトリに保存することだ。


```shell
# まず、JavaScriptコンパイラを変数として割り当てる
# この場合babelで、厳密には必要ないが
# あったほうがメンテナンス性が少し良くなるだろう
JC            = babel

# looseトランスパイルを有効にする
JCFLAGS       = --loose

# 次にsrcディレクトリからソースとなるファイルを見つける
SRC           = $(shell find src -name "*.js")

# それから取得した文字列を置き換え、
# ソースディレクトリとライブラリディレクトリでマップする
LIB           = $(SRC:src/%.js=lib/%.js)

# 最後に、ソースからライブラリにコンバートするルールを定義する
# これはコンパイラをそのオプションとその依存ファイルで起動させるためである
# ようやく定義したルールで、ターゲットを出力する
$(LIB): $(SRC)
  mkdir -p $(@D)
  $(JC) $(JCFLAGS) $< -o $@
```

すべてbashスクリプトに似ていると思う、 `$(VARIABLE)` は変数を展開し、`$(@D)` は別の自動変数で、ターゲットファイル名のディレクトリ部分を保持する。


##  コードのバンドル

Browserify、Webpackまたは単なるコンキャットもまたブラウザ環境にコードをディストリビュートするためには必要な作業と言える。このため、すべてのソースファイルを依存ファイルとし、１つのターゲットを持ち、それらをバンドラーに渡すレシピを持つルールを定義しなければならない。


```shell
# 以前と同様に、バンドラーを変数として持つ
BUNDLE        = browserify

# 加えて、起動フラグも設定する
# これは変数を使って簡単にする例である
# すでに変数を定義してあるので、
# babelとbabelify transformで同じフラグを共有したい
BUNDLEFLAGS   = --transform babelify [$(JCFLAGS)]

# 次にバンドルファイル名を定義する
DIST          = dist.js

# ようやく、ルールを定義する、要は全てのを依存ファイルを
# バンドラーに渡し、ターゲットに出力する
# 既にコンパイルしたライブラリファイルがあるが
# コンパイラーはよくヘルパーを生成するので、
# 一般的にこの成果物はいくぶんか大きいファイルになる
$(DIST): $(SRC)
  $(BUNDLE) $(BUNDLEFLAGS) -o $@ $^
```

## コードの最適化

ミニファイと不必要なコードの除去もまた一般的なビルドステップだ。今回のケースの場合、以前に定義したバンドルターゲットを依存ファイルとしてuglifyするだけだ。あとはミニファイしていないバンドル名をもとにミニファイしたバンドル名を置換するだけだ。

```shell
DIST_MIN            = dist.min.js

# ミニファイツールとしてuglifyjsを使用
MIN                 = uglifyjs

# 今のところ、フラッグは必要としない
MINFLAGS            = 

# このルールはとてもシンプルである
# １つのターゲットと依存ファイルををオプティマイザーに通すだけだ
$(DIST_MIN): $(DIST)
  $(MIN) $(MINFLAGS) $< -o $@
```

## ビルドクリーン

makeは`.PHONY`と呼ばれる[特別なターゲット](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html)を持っており、この依存ファイルは偽りのターゲットとみなされる。`make`は、その名前のファイルが存在しているかどうか、最終更新時刻がどうかに関わらず、無条件にこのレシピを実行する。これはファイルが生成されたかどうかに関係なくスクリプトを実行したいケースで役立つだろう。ビルドをクリーンしたい場合の例は以下。

```shell
clean:
  rm $(LIB)
  rm $(DIST)
  rm $(DIST_MIN)
```

## まとめ

makeは難しいためか少し不当な評価をされているように思えるが、実際はシェルスクリプトとたいして変わりはない。私の考えでは、シンタックスはとても明解で簡潔であり、ストリームであり、パイプであり`unix`と呼ばれる大きなエコシステムとの大きな相互運用性も手に入る。make万歳！Makefileを書こう！

+ [この記事のサンプルコードはこちら](https://gist.github.com/caspervonb/d2f4ea03c8166eef7d01)

記事に対する意見はご自由に[@caspervonb on Twitter](http://twitter.com/caspervonb)に。

***

私はWebデザイナー出身なので、おっさんだけどmakeを知らない方のおっさん。そうゆう人も多いのではないかな。まぁプロジェクトメンバーによってビルドツールを選べば良いと思うけど、makeも憶えておいて損はないと思う、ってじっちゃんが言ってた。

#### 関連エントリ

+ [Grunt/Gulpで憔悴したおっさんの話 - MOL](/mol/log/npm-run-script/)