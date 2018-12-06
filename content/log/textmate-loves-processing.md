---
date: 2009-08-15
title: TextMateをProcessingのエディタ代わりにする
subtitle: The Missing Editor for Mac OS X
categories: 
    - development
excerpt: IAMASのオープンキャンパスに行って以来、Processingをちょいちょい触っている。が、この標準のエディタ、文字は小さいしコードの補完機能もない。
ogimage: http://lh5.ggpht.com/_1drnogi3vdg/SnrLKtoIT3I/AAAAAAAAAgc/3Q5un_J7fSU/pt.png
---

![](http://lh5.ggpht.com/_1drnogi3vdg/SnrLKtoIT3I/AAAAAAAAAgc/3Q5un_J7fSU/pt.png)

IAMASのオープンキャンパスに行って以来、[Processing](https://processing.org/)をちょいちょい触っている。が、この標準のエディタ、文字は小さいしコードの補完機能もない。

## 高機能テキストエディタ：TextMate

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/097873923X/warikiru-22/" name="azlinklink" target="_blank"><img src="https://images-na.ssl-images-amazon.com/images/I/41hpiWi3FxL._SL160_.jpg" alt="Textmate: Power Editing for the Mac (Pragmatic Programmers)" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/097873923X/warikiru-22/" name="azlinklink" target="_blank">Textmate: Power Editing for the Mac</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2015.3.23</div></div><div class="azlink-detail">James Edward, II Gray<br />Pragmatic Bookshelf<br />売り上げランキング: 264049<br /></div><div class="azlink-review" style="margin-top:10px;margin-bottom:10px"></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/097873923X/warikiru-22/" target="_blank">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

てことで、形から入る男：t32kなので、なんか良いエディタはないものかと探してたら[TextMate](https://macromates.com/)なるものを見つけた。TextMate自体、Processingどうこうゆう前から素晴らしいエディタというのは耳にしていたので、JavaScript書くときでも使えるし5000円ぐらいするけど、エイヤ！の勢いで買ってしまった。

早速、TextMateを使ってみる。TextMateは補完機能がハンパねぇと聞いていたので、どれほどのものかと期待していたが補完されない...Aptanaみたいにfun..と入力したら勝手に補完するコードをリストアップして提示してくれるのかと思ったら、これはどうやらTabキーなど押さなきゃいけないらしい。

![](http://lh6.ggpht.com/_1drnogi3vdg/Sn6SuzlosVI/AAAAAAAAAgk/uAjYAKfhJU0/t1.png9)

funと入力してTabキーを押すと（JavaScriptの場合）

![](http://lh5.ggpht.com/_1drnogi3vdg/Sn6SvKAOAsI/AAAAAAAAAgo/wUsO7qFc1jA/t2.png)

補完されたコードが表示される。 自動補完よりもこっちの方が慣れたら速いのかもね。


## GetBundleをインストール

てことで、TextMateの使い方も大体分かったのでProcessingでも使えるようにする。ネットで調べてみると、情報はあることはあるが散見していて内容も少し古かったりするので、以下の情報は僕の環境で動いた方法を紹介する。

+ Mac OS X 10.5.8
+ TextMate 1.5.8
+ Processing 1.0.5

まず、TextMateでProcessingを有意義に使うにはProcessing用のBundle(ショートカットなどの設定)をインストールしなければならない。このBundleのインストールがややこいので簡単にインストールできるBundle、__GetBundle__をまずインストールする。

ターミナルを開いて以下のコマンドを打ち込む。

```shell
$ mkdir Library/Application\ Support/TextMate/Bundles
$ cd Library/Application\ Support/TextMate/Bundles
$ svn co http://svn.textmate.org/trunk/Bundles/GetBundle.tmbundle/
```

ターミナルとかよくわからんので合ってるかどうかわからないけど説明すると、mkdirでBundlesのディレクトリを作成して、cdでそのディレクトリに移動、svn coでSubversionからGetBundleをCheckOut(ダウンロード)してインストール完了。たぶんそんな感じ。

そしてTextMateを再起動させると、BundlesメニューにGetBundleの項目が表示されるので、そこのInstall Bundleを選択！

で動かなかった場合、 `Bundles` > `Bundle Editor` > `Show Bundle Editor` > `GetBundle`> `Install Bundle`のBASE_URL部分を以下に変更。

![](http://lh4.ggpht.com/_1drnogi3vdg/SoWQhyEn9XI/AAAAAAAAAgw/IIk_x0lpycU/base.png)

```bash
BASE_URL=http://svn.textmate.org/trunk/
```

再度Install Bundleを選択すると、このようなウィンドウが表示され好きなBundleを選択するだけでインストールできる。 

## ProcessingのBundleをインストール

ProcessingのBundleをインストールして、Bundles > Bundle Editor > Show Bundle Editor > Processing > Run in ProcessingのCommands部分を以下に書き換え。

![](http://lh5.ggpht.com/_1drnogi3vdg/SoWQhx3IxtI/AAAAAAAAAg4/hEepORHoY7w/pro.png)

```bash
osascript  <<EOF
tell application “Processing” to run
tell application “Processing” to activate
tell application “Processing” to open POSIX file “${TM_FILEPATH}”
delay 1
tell application “System Events” to tell process “Processing”

keystroke “r” using command down
end tell
EOF
```

これで設定完了。TextMateで適当にProcessingのコードを打ち込んで`Ctrl` + `R`を押すとProcessingが立ち上がる。