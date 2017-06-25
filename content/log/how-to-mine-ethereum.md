---
date: 2017-06-30
title: Ethereumをマイニングしてみる（2017夏）
subtitle: How to mine Ethereum on a Windows PC
categories: 
    - gadget
excerpt: 豆腐メンタルな自分にとって、デイトレは命を削るようなもので、こんなこと続けられない。まっとうに生きようと思い仮想通貨のマイニングを決意した2017年の夏である。
ogimage: https://t32k.me/mol/images/2017/mining/00.jpg
---

![](/mol/images/2017/mining/00.jpg)

年初に立てた目標である[ANA SFC獲得](/mol/log/2017-sfc-outro/)を早々に達成してしまい、生きる意味を失いかけていた。幸い、最近は仮想通貨にご執心で日々デイトレーダーのごとく生活していた。ただ、豆腐メンタルな自分にとって、デイトレは命を削るようなもので、こんなこと続けられない。まっとうに生きようと思い仮想通貨のマイニングを決意した2017年の夏である。

仮想通貨と聞けばビットコインを思い出すだろうが、ビットコインのマイニングに関しては専用のマシンを使い、工場などで大規模に行うのが主流であり、なおかつ中国のような電気代が安い国でやるのがセオリーであり、個人ではどうこうするものではない。

ただ[Ethereum](https://www.ethereum.org/)などのほかのいくつかの仮想通貨に関しては、をグラフィックボード複数積めば、そこそこ稼げるという噂を聞き、手を出して見た次第である。

## Windows PCの準備

コスパよくグラボを複数積むために、まずデスクトップWindowsを用意しなければならない。大学の時に初めて買ったパソコンがVaioで、それ以降はずっとMacだった自分にとっては自作Windows PCは未知の部分だ。詳しい同僚の助けを得ながら、Amazonでポチッとな！

### マザーボード PRIME X370-PRO

![](/mol/images/2017/mining/01.jpg)

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B06WD4N297/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/51T1YHLsxRL._SL160_.jpg" alt="ASUSTeK AMD X370搭載 マザーボード PRIME X370-PRO【ATX】" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B06WD4N297/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">ASUSTeK AMD X370搭載<br>マザーボード PRIME X370-PRO【ATX】</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail"><br />Asustek<br />売り上げランキング: 3616<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B06WD4N297/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

基本的に一番重要なのはグラボなので、自作PC詳しい人はすっ飛ばしてもらって問題ない。

最近のマザーボードならグラボが6枚くらい積めそうなので、価格.comで人気そうなの選んだ。選ぶポイントはPCI Express x1 or 16xのスロットが何個ついてるかだ。

### CPU AMD Ryzen7 1700 with WraithSpire 65W

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B06WP5YCX6/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="http://ecx.images-amazon.com/images/G/09/nav2/dp/no-image-no-ciu.gif" alt="AMD CPU Ryzen7 1700 with WraithSpire 65W cooler AM4 YD1700BBAEBOX" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B06WP5YCX6/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">AMD CPU Ryzen7 1700 with WraithSpire 65W<br>cooler AM4 YD1700BBAEBOX</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail">Windows<br />AMD<br />売り上げランキング: 724<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B06WP5YCX6/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

GPUでマイニングするのでCPUの性能は関係ない。ので別にそんなにいいCPUを買う必要はないが、最近よくRyzen!Ryzen!と聞くので、流行りに乗ってみた。

### DDR4 メモリ

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B0123ZC44Y/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/31-R33jrbXL._SL160_.jpg" alt="CORSAIR DDR4 メモリモジュール VENGEANCE LPX Series 8GB×2枚キット CMK16GX4M2A2666C16" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B0123ZC44Y/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">CORSAIR DDR4 メモリモジュール<br> VENGEANCE LPX Series 8GB×2枚キット<br>CMK16GX4M2A2666C16</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail"><br />Corsair<br />売り上げランキング: 163<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B0123ZC44Y/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

メモリは8GBくらいあれば十分っぽいが、8GB1枚買うよりも2枚買ったほうが単価が安かったので貧乏性ゆえ2枚組のを購入した。

### HDD

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00QIH3RWW/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/41KNYzGI4GL._SL160_.jpg" alt="Samsung SSD 250GB 850 EVO ベーシックキット V-NAND搭載 2.5インチ 内蔵型  MZ-75E250B/IT" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00QIH3RWW/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">Samsung SSD 250GB 850 EVO<br>V-NAND搭載 2.5インチ 内蔵型  MZ-75E250B/IT</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail"><br />日本サムスン<br />売り上げランキング: 324<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00QIH3RWW/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

これも250GBの買ったけど、120GBとかで十分そう。 なんのアレも無しに、SATAの2.5インチのSSDを買ったけど、最近だとM.2インターフェースのSSDというのがあって、メモリみたいな形で消費電力が少なくて良い（大事！）とマイナーコミュニティなかでは評判のようだった。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01N1PMFNU/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/414em8i5YVL._SL160_.jpg" alt="Samsung SSD 250GB 960 EVO M.2 Type2280 PCIe3.0×4 NVMe1.2 V-NAND搭載 3年保証 日本サムスン正規品 MZ-V6E250B/IT" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01N1PMFNU/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">Samsung SSD 250GB 960 EVO M.2 Type2280<br>PCIe3.0×4 NVMe1.2 V-NAND搭載</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail"><br />日本サムスン<br />売り上げランキング: 922<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01N1PMFNU/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

値段もそこまで変わらないし、こっち買えばよかったかな。

### PCケース

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01AXJQVFK/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/41OXJqzrbAL._SL160_.jpg" alt="SAMA 左側面がフルアクリルパネル(透明)のATXマザー対応ミドルタワーPCケース JAX-02W (黒透 kurosuke)" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01AXJQVFK/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">SAMAマザー対応ミドルタワーPCケース JAX-02W</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail"><br />SAMA<br />売り上げランキング: 594<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01AXJQVFK/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

ミドルタワーサイズであれば問題ないけど、グラボを6枚くらい積むとスペースが無いのでいらないかもしれない。

### 電源ユニット

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01AURFSBI/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/51yBtQnRHDL._SL160_.jpg" alt="ENERMAX ブロンズ 電源 1000W Triathlor ECO ETL1000EWT-M" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01AURFSBI/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">ENERMAX ブロンズ 電源 1000W<br>Triathlor ECO ETL1000EWT-M</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.25</div></div><div class="azlink-detail">Windows<br />ENERMAX<br />売り上げランキング: 6687<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01AURFSBI/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

電源ユニットは超重要である。グラボ一枚ものによるけど100~200Wは消費するので複数枚積む予定なら余裕のある電源ユニットを買おう。

![](/mol/images/2017/mining/02.jpg)

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B0190M0DS2/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/51FP3-XhrQL._SL160_.jpg" alt="Corsair RM1000x 80PLUS GOLD認証取得 1000W静音電源ユニット PS596 CP-9020094-JP" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B0190M0DS2/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">Corsair RM1000x 80PLUS GOLD認証取得 <br>1000W静音電源ユニットPS596 CP-9020094-JP</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted with <a href="http://sakuratan.biz/azlink/dp/Corsair%20RM1000x%2080PLUS%20GOLD%E8%AA%8D%E8%A8%BC%E5%8F%96%E5%BE%97%201000W%E9%9D%99%E9%9F%B3%E9%9B%BB%E6%BA%90%E3%83%A6%E3%83%8B%E3%83%83%E3%83%88%20PS596%20CP-9020094-JP/B0190M0DS2/warikiru-22" target="_blank">AZlink</a>  at 2017.6.25</div></div><div class="azlink-detail"><br />Corsair<br />売り上げランキング: 4157<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B0190M0DS2/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

あと、ブロンズとかシルバーとかゴールドとかクラスがあって、これが高いほど電源効率が良かったり、安全性が高いらしい。マイニングするとずっとフル稼働させるので、気になる所。最初よくわからなかったのでブロンズのものを買ったけど、ゴールドのものに買い直した。

### OS

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01JNAVIL2/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/41x7ZH5OeEL._SL160_.jpg" alt="Microsoft Windows 10 Home Anniversary Update適用版 32bit/64bit 日本語版 (最新)|" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01JNAVIL2/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">Microsoft Windows 10 Home 32bit/64bit</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted with <a href="http://sakuratan.biz/azlink/dp/Microsoft%20Windows%2010%20Home%20Anniversary%20Update%E9%81%A9%E7%94%A8%E7%89%88%2032bit/64bit%20%E6%97%A5%E6%9C%AC%E8%AA%9E%E7%89%88%20(%E6%9C%80%E6%96%B0)%7C/B01JNAVIL2/warikiru-22" target="_blank">AZlink</a>  at 2017.6.25</div></div><div class="azlink-detail">Windows<br />マイクロソフト<br />売り上げランキング: 43<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B01JNAVIL2/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

Linuxでも出来るが、Windowsを購入。64bit版を買った。

## ビデオカード

肝心のビデオカードだが、Ethereumのマイニングに関してはNvidia GeForce系よりもAMD Radeon系のビデオカードが適している。

> ![](/mol/images/2017/mining/rx.png)
引用：[AMDの新GPU「Radeon RX580，RX570，RX560」のスペック・パフォーマンスに迫る](http://androgamer.net/2017/03/29/post-4108/)

Radeon RX 580・570, 480・470が主力のビデオカードとなるが、500系と400系であまりマイニング性能に差がないらしく、消費電力が少ない400系のほうがよさそうに見える。

ただ、400系は生産が終了しているらしくほとんど在庫がない、さらには最近のEthereum価格高騰と仮想通貨ブームによりマイニングが大流行中であり、500系シリーズも在庫がない。本気でない。マジでない。

![](/mol/images/2017/mining/05.jpg)

というわけで秋葉原に足を運んで、なんとかRX560 4GBを3枚ゲットできたので、はじめはこれでがんばる。x80・x70に比べると性能は半減だが、消費電力も半分なので、まぁよい。現在だとGPUメモリが2GBだと採掘できないので4GB以上のものを買おう。

最近のRadeon RX不足により、マイナーコミュニティの方々は割高だがNvidia GeForceにシフトチェンジしているようにみえる。


## 採掘

- [MyEtherWallet: Open\-Source & Client\-Side Ether Wallet](https://www.myetherwallet.com/)

マイニングしたETHを保管するためのウォレットを作成しておく。MyEtherWalletが有名なので、適当に作成しておく。

- [Nanopool \| Ethereum \| Help](https://eth.nanopool.org/help)

上記サイトから、マイニングツールのClaymoreをダウンロードする。

![](/mol/images/2017/mining/config.png)

`Generate your config` ボタンから、ETHのアドレスとか設定する。あとはGenerateされたbatファイルを起動させるだけでOKだ。

![](/mol/images/2017/mining/03.jpg)

RX560 4GBを3枚積んだところ。

![](/mol/images/2017/mining/device.png)

ちゃんと3枚認識している。

![](/mol/images/2017/mining/mining.png)

RX570が22~23Mh/sぐらいのハッシュレートなので、ほんとうに半分な感じ。3枚積んで30~32Mh/sくらい出てる。

![](/mol/images/2017/mining/pool.png)

このレートだとシュミレーター的には電気代差し引いても月フル稼働させて1万円くらいの利益がでるかもしれない。

## 所感

![](/mol/images/2017/mining/04.jpg)

結局、PCケースだと熱がこもるので家庭用メタルラックかってむき出しで使っている。RX560は消費電力も少ないし、補助電源もいらないので、いまのところ電源と熱の問題はそれほどではない。はやくRX570、6枚づけしたい。

<div class="azlink-box"><div class="azlink-image" style="float:left"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00H8JXRD8/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow"><img src="https://images-fe.ssl-images-amazon.com/images/I/41%2B-BIhfykL._SL160_.jpg" alt="アイリスオーヤマ メタルラック カラーメタルシリーズ  ハンガーラック ポール径19mm カラーメタルラック 3段 幅55×奥行35×高さ80㎝ ホワイト CMM-55083" style="border:none" /></a></div><div class="azlink-info" style="float:left;margin-left:15px;line-height:120%"><div class="azlink-name" style="margin-bottom:10px;line-height:120%"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00H8JXRD8/warikiru-22/ref=nosim/" name="azlinklink" target="_blank" rel="nofollow">アイリスオーヤマ メタルラック　CMM-55083</a><div class="azlink-powered-date" style="font-size:7pt;margin-top:5px;font-family:verdana;line-height:120%">posted at 2017.6.26</div></div><div class="azlink-detail"><br />アイリスオーヤマ(IRIS)<br />売り上げランキング: 9394<br /></div><div class="azlink-link" style="margin-top:5px"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/B00H8JXRD8/warikiru-22/ref=nosim/" target="_blank" rel="nofollow">Amazon.co.jp で詳細を見る</a></div></div><div class="azlink-footer" style="clear:left"></div></div>

今回、自作Windos PC自体初めてだったのでコスト度外視で好きなもの購入した。マイニングができなくなったら機械学習でもやろう（たぶんやらないけど）。

コスト重視でやれば10万円未満でマイニングリグは作れるし、RX570とかすでに持っているんならやっておいてもいいんじゃないかな。ただ絶賛全世界で品薄で、通常2~3万くらいのグラボが5~6万くらい取引されているのを見ると、出遅れ感はんぱない。EthereumはPoWも辞める予定とのことなので、Ethereumマイニングは年内ぐらい目処だろう。また今後も新規参入社が増えてDifficultyがあがれば、得られるETHも少なくなる。

そもそも、自作Windos PCすら作ったことがない自分がマイニングしている時点で、ある程度のマジョリティに到達しているようなものだ。

というわけで、趣味で気楽にマイニングしていこうと思う。
