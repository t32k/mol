---
date: 2009-08-15
title: TextMateをProcessingのエディタ代わりにする
categories: design
---

<img src="http://lh5.ggpht.com/_1drnogi3vdg/SnrLKtoIT3I/AAAAAAAAAgc/3Q5un_J7fSU/pt.png" alt="" />
<a href="http://warikiru.blogspot.com/2009/08/iamas-openhouse-2009.html">IAMASのオープンキャンパス</a>に行って以来、<a href="http://processing.org/download/index.html">Processing</a>をちょいちょい触っている。が、この標準のエディタ、文字は小さいしコードの補完機能もない。

<img src="http://lh3.ggpht.com/_1drnogi3vdg/SoaiX-oRdpI/AAAAAAAAAhI/uc9llrJvJEc/editor.png" alt="" />
<h3>高機能テキストエディタ：TextMate</h3>
てことで、形から入る男：t32kなので、なんか良いエディタはないものかと探してたら<a href="http://macromates.com/">TextMate</a>なるものを見つけた。TextMate自体、Processingどうこうゆう前から素晴らしいエディタというのは耳にしていたので、JavaScriptでも使えるし5000円ぐらいするけど、エイヤ！の勢いで買ってしまった。

早速、TextMateを使ってみる。TextMateは補完機能がハンパねぇと聞いていたので、どれほどのものかと期待していたが補完されない。。。　Aptanaみたいにfun..と入力したら勝手に補完するコードをリストアップして提示してくれるのかと思ったら、これはどうやらTabキーなど押さなきゃいけないらしい。

<img src="http://lh6.ggpht.com/_1drnogi3vdg/Sn6SuzlosVI/AAAAAAAAAgk/uAjYAKfhJU0/t1.png9" alt="" />
funと入力してTabキーを押すと（JavaScriptの場合）

<img src="http://lh5.ggpht.com/_1drnogi3vdg/Sn6SvKAOAsI/AAAAAAAAAgo/wUsO7qFc1jA/t2.png" alt="" />
補完されたコードが表示される。
自動補完よりもこっちの方が慣れたら速いのかもね。

<img src="http://lh6.ggpht.com/_1drnogi3vdg/SoaiYGy_mVI/AAAAAAAAAhM/e4DQ_GSWDU4/sc.png" alt="" />
<span style="font-style: italic; color: #666666; font-size: 85%;">JavaScriptのBundle例</span>
<h3>GetBundleをインストール</h3>
てことで、TextMateの使い方も大体分かったのでProcessingでも使えるようにする。ネットで調べてみると、情報はあることはあるが散見していて内容も少し古かったりするので、以下の情報は僕の環境で動いた方法を紹介する。
<ul>
	<li>Mac OS X <span style="font-style: italic;">10.5.8</span></li>
	<li>TextMate <span style="font-style: italic;">1.5.8</span></li>
	<li>Processing <span style="font-style: italic;">1.0.5</span></li>
</ul>
まず、TextMateでProcessingを有意義に使うにはProcessing用のBundle(ショートカットなどの設定)をインストールしなければならない。このBundleのインストールがややこいので簡単にインストールできるBundle、<span style="font-weight: bold;">GetBundle</span>をまずインストールする。

ターミナルを開いて以下のコマンドを打ち込む。
<pre><span style="color: #999999;">$ </span>mkdir Library/Application\ Support/TextMate/Bundles
<span style="color: #999999;">$ </span>cd Library/Application\ Support/TextMate/Bundles
<span style="color: #999999;">$ </span>svn co http://svn.textmate.org/trunk/Bundles/GetBundle.tmbundle/</pre>
ターミナルとかよくわからんので合ってるかどうかわからないけど説明すると、mkdirでBundlesのディレクトリを作成して、<span style="font-weight: bold;">cd</span>でそのディレクトリに移動、<span style="font-weight: bold;">svn co</span>でSubversionからGetBundleをCheckOut(ダウンロード)してインストール完了。たぶんこんな感じｗ

そしてTextMateを再起動させると、BundlesメニューにGetBundleの項目が表示されるので、そこのInstall Bundleを選択！

で動かなかった場合、
Bundles &gt; Bundle Editor &gt; Show Bundle Editor &gt; GetBundle &gt; Install BundleのBASE_URL部分を以下に変更。
<pre>BASE_URL=http://svn.textmate.org/trunk/</pre>
<img src="http://lh4.ggpht.com/_1drnogi3vdg/SoWQhyEn9XI/AAAAAAAAAgw/IIk_x0lpycU/base.png" alt="" />
<span style="font-family: monospace;">
</span>で、再度Install Bundleを選択すると、このようなウィンドウが表示され好きなBundleを選択するだけでインストールできる。
<img src="http://lh6.ggpht.com/_1drnogi3vdg/SoaiXxtQINI/AAAAAAAAAhE/izQJmsdpf7A/choose.png" alt="" />
<h3>ProcessingのBundleをインストール</h3>
ProcessingのBundleをインストールして、Bundles &gt; Bundle Editor &gt; Show Bundle Editor &gt; Processing &gt; Run in ProcessingのCommands部分を以下に書き換え
<pre>osascript  &lt;&lt;EOF
tell application "Processing" to run
tell application "Processing" to activate
tell application "Processing" to open POSIX file "${TM_FILEPATH}"
delay 1
tell application "System Events" to tell process "Processing"

keystroke "r" using command down
end tell
EOF</pre>
<img src="http://lh5.ggpht.com/_1drnogi3vdg/SoWQhx3IxtI/AAAAAAAAAg4/hEepORHoY7w/pro.png" alt="" />
<span style="font-family: monospace;">
</span>これで設定完了♪
TextMateで適当にProcessingのコードを打ち込んでCtrl + Rを押すとProcessingが立ち上がります。

<span style="font-size: 85%;">参考サイト
</span>
<ul>
	<li><span style="font-size: 85%;"><a href="http://mialweb.ddo.jp/jam/?p=69">Jam’s Blog » TextMate</a></span></li>
	<li><span style="font-size: 85%;"><a href="http://blog.wozozo.jp/archives/144">TextMateでProcessing - ヲゾゾ wozozo ウンコプログラマー 〜綺麗なお姉さん〜</a></span></li>
</ul>
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/Textmate-Power-Editing-Pragmatic-Programmers/dp/097873923X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D097873923X" target="_blank"><img src="http://ecx.images-amazon.com/images/I/41hpiWi3FxL._SL160_.jpg" border="0" alt="Textmate: Power Editing for the Mac (Pragmatic Programmers)" /></a></td>
<td valign="top"><span style="font-size: 85%;"><a href="http://www.amazon.co.jp/Textmate-Power-Editing-Pragmatic-Programmers/dp/097873923X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D097873923X" target="_blank">Textmate: Power Editing for the Mac (Pragmatic Programmers)</a><img src="http://www.blogger.com/%27http://www.assoc-amazon.jp/e/ir?t=" border="0" alt="''" width="1" height="1" /></span>

Pragmatic Bookshelf  2007-02
売り上げランキング : 30287

<a href="http://www.amazon.co.jp/Textmate-Power-Editing-Pragmatic-Programmers/dp/097873923X%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D097873923X" target="_blank">Amazonで詳しく見る</a><span style="font-size: 85%;"> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>