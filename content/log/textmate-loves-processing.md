---
date: 2009-08-15
title: TextMateをProcessingのエディタ代わりにする
subtitle: The Missing Editor for Mac OS X
categories: 
    - development
excerpt: IAMASのオープンキャンパスに行って以来、Processingをちょいちょい触っている。が、この標準のエディタ、文字は小さいしコードの補完機能もない。
---

IAMASのオープンキャンパスに行って以来、[Processing](https://processing.org/)をちょいちょい触っている。が、この標準のエディタ、文字は小さいしコードの補完機能もない。

## 高機能テキストエディタ：TextMate

てことで、形から入る男：t32kなので、なんか良いエディタはないものかと探してたら[TextMate](https://macromates.com/)なるものを見つけた。TextMate自体、Processingどうこうゆう前から素晴らしいエディタというのは耳にしていたので、JavaScript書くときでも使えるし5000円ぐらいするけど、エイヤ！の勢いで買ってしまった。

早速、TextMateを使ってみる。TextMateは補完機能がハンパねぇと聞いていたので、どれほどのものかと期待していたが補完されない...Aptanaみたいにfun..と入力したら勝手に補完するコードをリストアップして提示してくれるのかと思ったら、これはどうやらTabキーなど押さなきゃいけないらしい。

funと入力してTabキーを押すと（JavaScriptの場合）

補完されたコードが表示される。 自動補完よりもこっちの方が慣れたら速いのかもね。


## GetBundleをインストール

てことで、TextMateの使い方も大体分かったのでProcessingでも使えるようにする。ネットで調べてみると、情報はあることはあるが散見していて内容も少し古かったりするので、以下の情報は僕の環境で動いた方法を紹介する。

- Mac OS X 10.5.8
- TextMate 1.5.8
- Processing 1.0.5

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

```bash
BASE_URL=http://svn.textmate.org/trunk/
```

再度Install Bundleを選択すると、このようなウィンドウが表示され好きなBundleを選択するだけでインストールできる。 

## ProcessingのBundleをインストール

ProcessingのBundleをインストールして、Bundles > Bundle Editor > Show Bundle Editor > Processing > Run in ProcessingのCommands部分を以下に書き換え。

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