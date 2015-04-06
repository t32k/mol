---
date: 2015-04-06
title: コマンドラインからGoogle Analyticsにデータを記録するGAERをつくった
subtitle: デベロッパーもGoogle Analyticsをもっと使おう！
categories: development
excerpt: 表題の通りのNode.jsのCLIツールを作った。Googleアナリティクスのイベントトラッキングレポートに、下記のように任意のJSONデータを送りつける。
ogimage: http://t32k.me/mol/images/2015/0406-00.png
---

[![GAER](/mol/images/2015/0406-00.png)](https://github.com/t32k/gaer)

+ __[t32k/gaer - GitHub](https://github.com/t32k/gaer)__

表題の通りのNode.jsのCLIツールを作った。Googleアナリティクスのイベントトラッキングレポートに、下記のように任意のJSONデータを送りつける。

```shell
$ npm install -g gaer 
$ gaer -t UA-xxxxx-xx -r reportName path/to/data.json
  Sending [||||||||||||||||||||||||] 100%
  Success: The data is sent to UA-xxxxx-xx
```

## デベロッパーとGoogleアナリティクス

基本的にイベントトラッキングレポートは、ページ遷移をともわないイベント、例えばPDFのダウンロードリンクをクリックした等を計測するために使われる。

```javascript
// JavaScript
ga('send', 'event', 'クリックイベント', 'PDF', '資料請求');
```

クリックしたイベントに上記のような関数を実行するので、いろいろ使い勝手がいい機能だ。別にこれはアクセス解析のためだけに使用するんじゃなくて、以前から[JavaScriptのエラーが発生したらそのページのURLを記録する](http://qiita.com/hidek84/items/e42f8632d95b9444aea4)等、デベロッパーライクな使い方をしてる人がいたりする。

そうでもなくても、Googleアナリティクスは、『__サイトの速度__』であったり、『__ユーザーの環境__』等の、デベロッパーも見るべき指標が多い。だから、もっとみんなGoogleアナリティクス使おうぜってことで、GAREを利用して欲しい。

GAREは[Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide)を使って、データを記録している。記録するJSONのキー分、ループでPOSTしてるだけだ。

```json
{
  "foo" : 12,
  "bar" : 2.1,
  "baz" : 9
}
```

こんな感じのシンプルなデータ構造のJSONなら送れる。


## モニタリングツールとして使う

なぜ、GAERを作ったのか。[StyleStats](https://github.com/t32k/stylestats)という、CSSのヘルスチェックツールがある。下記のように使うとJSONデータでCSSの状態を確認することができる。

```shell
$ npm install -g stylestats
$ stylestats -f json -n foo.css
{
  "stylesheets": 2,
  "size": 6682,
  "dataUriSize": 0,
  "gzippedSize": 1992,
  "rules": 86,
  "selectors": 179,
  "simplicity": 0.48044692737430167,
  "mostIdentifier": 2,
  "lowestCohesion": 17,
  "totalUniqueFontSizes": 12,
  "totalUniqueFontFamilies": 1,
  "totalUniqueColors": 6,
  "idSelectors": 0,
  "universalSelectors": 0,
  "unqualifiedAttributeSelectors": 17,
  "javascriptSpecificSelectors": 0,
  "importantKeywords": 0,
  "floatProperties": 4,
  "mediaQueries": 3
}
```

ファイルサイズがどれだけとか、ルール数がどれだけとか、これだけ見ても多少は役に立つかもしれないが、CSSは絶えず変化するものなので、できればこのデータの推移を把握したいものである。そうなると、__データを貯める__のとそれを__グラフに出力__する作業が必要となる。

今まで、[Jenkinsにプロットする](https://github.com/t32k/stylestats/wiki/Plot-with-Jenkins)やり方や、[moniteurというツールを使うやり方](https://github.com/t32k/stylestats/wiki/Plot-with-moniteur)を試してみたが、グラフがダサかったり、実装方法がやや複雑だったりして、あんまりしっくりきてなかった。

+ [StyleStats＋αでCSSを継続的にチェックする | アライドアーキテクツのクリエイターブログ](http://creator.aainc.co.jp/archives/7123)

この人のように、D3.jsを使って、フルスクラッチで作るのが妥当なんだろうけど、なにぶんめんどくさがり屋なのでめんどくさい。

```shell
$ stylestats -f json -n https://google.com | gaer -t UA-xxxxxxx-x -r Google
```

だもんで、上記のような感じで、JSONで書きだした結果をパイプでGAERに渡しても、Googleアナリティクスにレコードさせればよい。

[![](/mol/images/2015/0406-01.png)](http://t32k.me/mol/images/2015/0406-01.png)

記録したデータは、Googleアナリティクスの『行動』＞『イベント』のメニューで確認できる。

[![](/mol/images/2015/0406-02.png)](http://t32k.me/mol/images/2015/0406-02.png)

まだデータ貯まってなくてアレだけど、まぁこんな感じで確認できるようになった。あとはこれを一日一回とか定期実行させればよい（これも若干面倒だけど、[Heroku Scheduler](https://addons.heroku.com/scheduler)を使うのがお手軽かも）。ほか、PushしたタイミングでCIサーバーのほうで実行するのもありかな。

なにせイベントトラッキングレポートなので、デフォルトではイベントの回数がメインになっているので、カスタムレポートで平均値だけを表示にしたりするのが若干面倒だけど、ここは使い方次第だと思う。

僕はStyleStatsのデータを記録するためにGAREを作ったけど、皆さんもグラフ作るの面倒くさいなってデータがあったらGoogleアナリティクスにレポートさせれば良いと思う。なんか良い使い方あったら教えて下さい。




