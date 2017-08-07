---
date: 2017-07-30
title: Ethereumをマイニングしてみる（2017夏・改）
subtitle: How to build an Ethereum mining rig
categories: 
    - gadget
excerpt: 一ヶ月間。マイニングリグをまともに動かすにかかった時間である。グラボ最大搭載数である6枚で最高のパフォーマンスがでなかったので、ほぼ全部買い直した。
ogimage: https://t32k.me/mol/images/2017/0802-00.jpg
--- 

一ヶ月間。マイニングリグをまともに動かすにかかった時間である。[先月の記事](/mol/log/how-to-mine-ethereum/)で一通りの機材を揃えてみたが、グラボ最大搭載数である6枚で最高のパフォーマンスが(まともに起動も)できなかったので、ほぼ全部買い直した。

## PCケース

いらない。マイニングできなくなったら普通のデスクトップとして使おう、なんて甘っちょろいこと考えていた自分が恥ずかしい。俺たちは自作PCを作っているんじゃない、マイニングリグを作っているんだ。ということで、物理的スペースと排熱の問題からメタルラック最高である。

## HDD

<div class="__media"><a href="https://www.amazon.co.jp/dp/B01M2WYNP2/?tag=warikiru-22" target="_blank" rel="noopener">
  <img src="https://images-na.ssl-images-amazon.com/images/I/81HuBRY8QcL._SX425_.jpg" class="__media__image">
  <div class="__media__body">
    <div>WD SSD 内蔵SSD M.2 120GB WD Green SATA3.0 6G / 3年保証 / WDS120G1G0B</div>
    <div class="__media__text">パソコン・周辺機器</div>
    <div>Amazon.co.jpで詳細を見る</div>
  </div>
</a></div>

マザーボードによっては取り付けることはできないかもしれないが、M2.SSDだと省スペース・省電力でいい！という[記事を前回書いた](/mol/log/m2-wds120g1g0b/)。

## マザーボード

<div class="__media"><a href="https://www.amazon.co.jp/dp/B072LXX4NF/?tag=warikiru-22" target="_blank" rel="noopener">
  <img src="https://images-na.ssl-images-amazon.com/images/I/61PPti4YSTL._SX522_.jpg" class="__media__image">
  <div class="__media__body">
    <div>BIOSTAR LGA 1151 プロセッサ対応 Intel B250 チップセット搭載 ATXマザーボード TB250-BTC</div>
    <div class="__media__text">パソコン・周辺機器</div>
    <div>Amazon.co.jpで詳細を見る</div>
  </div>
</a></div>

前回購入したマザーボードもPCIeスロットは6個あり、仕様上はグラボを稼働できるはずなのだが、どうやっても、うまくいかない。そもそもPRIME X370-PROでマイニングしている人がいないので、圧倒的に情報量が少ない。

ということで、王道のTB250-BTCを購入した。ゼロ設定とまでは言わないが、ちょっと設定をいじるだけで6枚グラボを稼働させることが出来た。なによりも、同じ構成でマイニングしている人の記事を読めることが出来たのが大きかった。

(AMD対応のTB350-BTCというマザーボードもあるので間違いないようにしよう！)

## CPU

<div class="__media"><a href="https://www.amazon.co.jp/dp/B01B2PJRPA/?tag=warikiru-22" target="_blank" rel="noopener">
  <img src="https://images-na.ssl-images-amazon.com/images/I/51XojlwY7xL._SY450_.jpg" class="__media__image">
  <div class="__media__body">
    <div>Intel CPU Celeron G3900 2.8GHz 2Mキャッシュ 2コア/2スレッド LGA1151 BX80662G3900 【BOX】</div>
    <div class="__media__text">パソコン・周辺機器</div>
    <div>Amazon.co.jpで詳細を見る</div>
  </div>
</a></div>

Intel対応のマザーボードに変えたので、CPUもAMDからIntel CPUへ。ということで5千円くらいで購入できる。Ryzenコスパいいけど、マイニングにはオーバースペックなので、このぐらいのCPUでいい。

## GPU

<div class="__media"><a href="https://www.amazon.co.jp/dp/B071L1VGQW/?tag=warikiru-22" target="_blank" rel="noopener">
  <img src="https://images-na.ssl-images-amazon.com/images/I/91QK2rDAbaL._SX522_.jpg" class="__media__image">
  <div class="__media__body">
    <div>ASUS  AMD RX580搭載ビデオカード  DUAL-RX580-O8G</div>
    <div class="__media__text">パソコン・周辺機器</div>
    <div>Amazon.co.jpで詳細を見る</div>
  </div>
</a></div>

運良く、発売日にRX580を購入できた。このASUSのDUAL-RX580-O8Gはほどよくマイニング仕様になっている。近いうちに発売されるマイニング専用のグラボはHDMI出力がなかったりして、完全に振り切ってる感はあるが、こちらのモデルはちゃんとある。こちらはIP5X対応防塵ファンであったり、長時間稼働を前提としたつくりになっていたりして、とてもよい( ˘ω˘)

## 電源ユニット

<div class="__media"><a href="https://www.amazon.co.jp/dp/B0190M09RW/?tag=warikiru-22" target="_blank" rel="noopener">
  <img src="https://images-na.ssl-images-amazon.com/images/I/51YRg%2BnvQLL._SX425_.jpg" class="__media__image">
  <div class="__media__body">
    <div>Corsair RM750x 80PLUS GOLD認証取得 750W静音電源ユニット PS594 CP-9020092-JP</div>
    <div class="__media__text">パソコン・周辺機器</div>
    <div>Amazon.co.jpで詳細を見る</div>
  </div>
</a></div>

RX580を6枚購入できたが、こやつの消費電力は最大で185Wなので、グラボだけで1110W消費することになってしまう。1000Wの電源を持っていたが、慌てて550Wの電源ユニットも追加した。1500Wくらいの電源ユニットを購入するのがいいんだろうけど、1000Wを超えるとワット単価が高くなるのでコスパが悪い。ネットの向こうのお友達は750W x 2基という構成だったので、頭が良いなと思いました( ˘ω˘)

## マイニングリグ

![](/mol/images/2017/0802-00.jpg)

とうわけで、元気よく動いてます( ˘ω˘)
