---
layout: post
title: MacBook Pro’13 Mid 2012 のメモリ交換して16GBにした
status: publish
type: post
published: true
---
<iframe src="https://www.flickr.com/photos/t32k/8644568837/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

今日は表題のとおり、MBP13の2012Midのメモリ交換したよ。BTOのとき、16GBが選択できなくててっきり認識しないのかと思ってたけど普通に認識するみたいだ。

![](/static/blog/2013/04/s1.png)

交換前のMyBookのスペック。

![](/static/blog/2013/04/s2.png)

4GB×2の8GB. まぁそこまでメモリ不足に悩んでないけどAdobe CSとかVMを一緒に立ち上げてるとなかなか重い気がするのと、1万未満で16GBが買えるということなので買ってみた（やつ↓）
<table border="0" cellpadding="5">
<tbody>
<tr>
<td colspan="2"><a href="http://www.amazon.co.jp/%E3%82%B7%E3%83%AA%E3%82%B3%E3%83%B3%E3%83%91%E3%83%AF%E3%83%BC-%E3%83%A1%E3%83%A2%E3%83%AA%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB-DDR3-1600-PC3-12800-SP016GBSTU160N22/dp/B0094P98FK%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3DB0094P98FK" target="_top">シリコンパワー メモリモジュール 204Pin SO-DIMM DDR3-1600(PC3-12800) 8GB×2枚組 SP016GBSTU160N22</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" /></td>
</tr>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/%E3%82%B7%E3%83%AA%E3%82%B3%E3%83%B3%E3%83%91%E3%83%AF%E3%83%BC-%E3%83%A1%E3%83%A2%E3%83%AA%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB-DDR3-1600-PC3-12800-SP016GBSTU160N22/dp/B0094P98FK%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3DB0094P98FK" target="_top"><img src="http://ecx.images-amazon.com/images/I/51ghxIR7QoL._SL160_.jpg" alt="シリコンパワー メモリモジュール 204Pin SO-DIMM DDR3-1600(PC3-12800) 8GB×2枚組 SP016GBSTU160N22" border="0" /></a></td>
<td valign="top"><span>
シリコンパワー
売り上げランキング : 398</span><a href="http://www.amazon.co.jp/%E3%82%B7%E3%83%AA%E3%82%B3%E3%83%B3%E3%83%91%E3%83%AF%E3%83%BC-%E3%83%A1%E3%83%A2%E3%83%AA%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB-DDR3-1600-PC3-12800-SP016GBSTU160N22/dp/B0094P98FK%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3DB0094P98FK" target="_top">Amazonで詳しく見る</a><span> by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
メモリの交換の仕方は公式サポートに書いてあるので、取り掛かる前に一読を。

__メモリカードの仕様__

- DDR3 (Double Data Rate Small Outline Dual Inline Memory Module) 方式
- 67.6mm x 30mm (1.18 インチ)
- 2 GB または 4 GB
- 204 ピン
- PC3-12800 DDR3 1600 MHz タイプの RAM


+ __<a href="http://support.apple.com/kb/HT1270?viewlocale=ja_JP">MacBook Pro：メモリの取り外し方法と取り付け方法</a>__


あと、メモリ交換する際にMBPを開かなきゃいけないんだけど、これて保証の対象外になるんだよなーと思ってたけど、保証の対象外になるのはそのメモリ交換に起因する故障の場合で、例えば電源タップがなんか知らんが壊れたとかなら期間内であれば保証してもらえるって感じかな。


+ __<a href="https://discussionsjapan.apple.com/thread/10116307?start=0&amp;tstart=0">SSDやメモリを換装するとサポート対象外...？: Apple サポートコミュニティ </a>__


確かに公式サポートでメモリの取り外し方書いてあるし、いいのかな。とはいえ、買ってもう1年するし保証期間も終わるってるしな、どうでもいいやということで、交換してみる。

まずは静電気対策のためにとりあえず全裸になりましょう。

<iframe src="https://www.flickr.com/photos/t32k/8645666878/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

裏面をみてみると、10本のネジがありますんで外しましょう。家にある100均の精密ドライバーセット使ってみたけど、サイズが合わなかった。00番のプラスドライバーが必要ということが分かったので、下記を注文した。とりあえず全裸になったけどドライバー届くまで服を着ようと思う。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B002SQLEIG/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/41-2usJbNaL._SL160_.jpg" alt="アネックス(ANEX) 精密ドライバー プラス00×50 No.3450" width="160" height="160" border="0" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E3%82%A2%E3%83%8D%E3%83%83%E3%82%AF%E3%82%B9-ANEX-%E7%B2%BE%E5%AF%86%E3%83%89%E3%83%A9%E3%82%A4%E3%83%90%E3%83%BC-%E3%83%97%E3%83%A9%E3%82%B900%C3%9750-No-3450/dp/B002SQLEIG%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3DB002SQLEIG" target="_blank">アネックス(ANEX) 精密ドライバー プラス00×50 No.3450</a><img style="border: none;" src="http://www.assoc-amazon.jp/e/ir?t=warikiru-22&amp;l=ur2&amp;o=9" alt="" width="1" height="1" /></span>兼古製作所
売り上げランキング : 32<a href="http://www.amazon.co.jp/%E3%82%A2%E3%83%8D%E3%83%83%E3%82%AF%E3%82%B9-ANEX-%E7%B2%BE%E5%AF%86%E3%83%89%E3%83%A9%E3%82%A4%E3%83%90%E3%83%BC-%E3%83%97%E3%83%A9%E3%82%B900%C3%9750-No-3450/dp/B002SQLEIG%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3DB002SQLEIG" target="_blank">Amazonで詳しく見る</a> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
無事にプラスドライバーがきたので全裸になる。右上右から3本までは長いネジであとは短いネジの計10本をはずす。

<iframe src="https://www.flickr.com/photos/t32k/8644568759/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

外すと、こんな感じで右中央にメモリ部分を確認できる。

<iframe src="https://www.flickr.com/photos/t32k/8644568711/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

全裸になってるけど、メモリ部分を外す前に金属っぽいとこ触って放電しておきましょう。取り外し方はメモリがハマってる両端のレバーみたいなものを外側に開くとパカっと上にメモリが開くような感じになる。

<iframe src="https://www.flickr.com/photos/t32k/8644568671/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

慎重に外してみた感じ。下段のメモリを取り外すのがてこづった。

<iframe src="https://www.flickr.com/photos/t32k/8645666616/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

ほんで、買ったメモリ取り付けて完了！

<iframe src="https://www.flickr.com/photos/t32k/8644568509/player/" width="640" height="358" frameborder="0" allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

Yeah!!!!!!!

![](/static/blog/2013/04/fd79ce5dba48706f16fc11179000825b.png)

ちゃんと認識してるみたい！

+ __<a href="http://support.apple.com/kb/HT1379?viewlocale=ja_JP">NVRAM と PRAM について </a>__

あと念の為にNVRAMのリセットもしておいたほうがよいとおもう。
