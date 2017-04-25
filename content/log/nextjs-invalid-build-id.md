---
date: 2017-04-25
title: Deploying Multiple Instances for Next.js
categories: 
    - development
excerpt: 最近、Next.jsを触っている。ほぼゼロ設定で、サーバーサイドでReactをレンダリングできたり、ルーティングがめちゃ簡単だったり、今のところいい感じである。
ogimage: https://t32k.me/mol/images/2017/nextjs.png
---

年始に立てた目標『[SFC会員になる！](/mol/log/new-years-resolutions-2017/)』も達成してしまい、そろそろちゃんとデベロッパーに戻るかーと思いリハビリながらメモを上げていこうと思う。

- [Next\.js \- Qiita](http://qiita.com/nkzawa/items/1e0e93efd13fb982c8c0)

最近、[Next.js](https://zeit.co/blog/next2)を触っている。ほぼゼロ設定で、サーバーサイドでReactをレンダリングできたり、ルーティングがめちゃ簡単だったり、今のところいい感じである。

> An unexpected error has occurred.

開発をしていて、たまに、というか、けっこうな確率でエラーページが表示されていて、なんでだろう？とログを見てみたら、

![](/mol/images/2017/0425-00.png)

BUILD_IDちゃうやんけー！と怒られていた。

- [Deployment · zeit/next\.js Wiki](https://github.com/zeit/next.js/wiki/Deployment)

ご丁寧にもWikiに買いてあった。

Next.jsの起動コマンドは`next build; next start`って感じでbuildコマンドを打ってから起動するのだけど、要は複数のインスタンスで毎回buildコマンドが走って、その度に
にユニークな`BUILD_ID`が生成されて、インスタンス間で異なるものになっちゃってる話だと理解した。

というわけで、ユーザー側で任意のIDで上書きしてやればいい。WikiにあるようにGitのコミットIDとか利用すればいいっぽい。

```
next build && echo $(git rev-parse HEAD) > .next/BUILD_ID
```

というわけで、こうゆう感じで書いたのだけど、GAE/Node.jsの環境ではうまくいかなかった。

```
next build && echo $GAE_VERSION > .next/BUILD_ID
```

めんどくさかったので、[GAEの環境変数](https://cloud.google.com/appengine/docs/flexible/nodejs/runtime)の`GAE_VERSION`を`BUILD_ID`として利用したら、サーバーエラ


