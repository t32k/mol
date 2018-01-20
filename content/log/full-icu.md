---
date: 2018-01-19
title: SeverとClientでレンダリング結果が違う
subtitle: International Components for Unicode
categories: 
    - development
excerpt: SeverとClientでレンダリング結果が微妙に違うとのこと。
---

Reactをアイソモーフィックに実行しているのだけど、下記のようなエラーが出てた。

> Warning: Text content did not match. Server: "1970-1-18 22:09" Client: "1970/1/18 22:09"

SeverとClientでレンダリング結果が微妙に違うとのこと。

```
new Intl.DateTimeFormat(locales, {
  year: "numeric",
  month: "numeric",
  day: "numeric",
  hour: "numeric",
  minute: "numeric"
});
```

該当のコード。

Node.js側の`Intl`オブジェクトが対応していないのかなと思いつつ、Node v8だし結構新しいしなーと思っていて、原因がわからず、しばらく放っておいた。

![](/mol/images/2018/0119-00.png)

- [Internationalization Support \| Node\.js v9\.4\.0 Documentation](https://nodejs.org/api/intl.html#intl_options_for_building_node_js)

あとで国際化のサポートがビルドの設定ごとで違うらしいと気づいた。デフォルトのビルドでは`--with-intl=small-icu`というもので、部分的なサポートでしかない。それとは別に`full-icu`という全サポートがあるらしく、これ入れたら、サーバーとクライアントでの差異はなくなった。

- [Intl · nodejs/node Wiki](https://github.com/nodejs/node/wiki/Intl)

ちなみにICUとは[International Components for Unicode](http://site.icu-project.org/)の略らしい。確かに全言語対応のデータ毎回入れてたら重いよね。

Node.jsのバージョンマネージャーは`nvm`使ってるんだけど、nvmインストールするときに下記のようなオプションつけると`full-icu`でビルドしたものをインストールできる。

```
nvm install -s v9.4.0 --with-intl=full-icu --download=all
```

でもこれだと毎バージョンごとにICUのデータ入れないといけないからめんどいよね。あとGAE Node.jsのインスタンスとかどこでNode.jsのビルドしてんだ？って感じなので、

- [unicode\-org/full\-icu\-npm: npm module to autoload full ICU data\.](https://github.com/unicode-org/full-icu-npm)

後づけで言語データをインストールができるnpmがある。

```
NODE_ICU_DATA=node_modules/full-icu/
```

あとは環境変数`NODE_ICU_DATA`にfull-icuの言語データへのパスを設定するだけでよい。

国際化とかホント苦手だわと思ったけど、今回の場合、日付の`/`と`-`が違うだけだったので、あんまり考えがめぐらなかったのが反省点。


