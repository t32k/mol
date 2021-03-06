---
date: 2011-01-02
title: querySelectorとquerySelectorAllというかLive NodeListとStatic NodeList
categories:
  - development
---

先日、`getElementsByClassName`便利だぜ！とブログに書いたら、to-R の西畑先生より`querySelectorAll`アルヨ！と言われたので、調べてみる。

## querySelector と querySelectorAll

- [IE8 で実装された Selectors API とは何か？ - IT 戦記](http://d.hatena.ne.jp/amachang/20080306/1204787459)

まぁ上記エントリにほぼ全てが書かれているので、特に今さら書くことはないのですが、自分メモのために。

なにはともあれ、サポート状況をば。

- [DOM Core](http://quirksmode.org/dom/core/)

Fx3.0 は対応していないけど、IE8 は対応してるのか。素敵！

```javascript
element = document.querySelector(selectors);
```

- [Document.querySelector() - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

`querySelector`ってのもある。基本的な使い方は両方一緒で`selectors</em`の引数に、取得したい要素の CSS セレクタ書いてあげればいい。`querySelector`は最初に見つけてきた単一の要素を返すのに対して、

>

```javascript
elementList = document.querySelectorAll(selectors);
```

elementList is a non-live NodeList of element objects.

- [Document.querySelectorAll() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)

querySelectorAll はノードリストを返す。

```javascript
var node = document.querySelectorAll("#hoge > h2");
```

つまり、`#hoge`の中の子供の h2 だけを取ってくるなんてことも、上記のように CSS セレクタで簡単に書けちゃう。jQuery ライクに書けちゃう。だから、これまで Firefox のグリモンとか Chrome の拡張機能を作成するときは僕は jQuery 読み込んでいたんだけど、簡単なものであれば Selectors API 使えば、jQuery に頼らなくても良くなった。

## Live NodeList と Static NodeList

はい、そんなわけで Selectors API＼(-o-)／なんですけども、ひとつ気になる点がありました。`querySelectorAll`が返すのは non-live なノードリストと書いてあります。non-live って何よ？ってことで、仕様書、仕様書

> querySelectorAll() メソッドから返される NodeList オブジェクトは 動的 (live) ではなく、静的 (static) である必要があります ([DOM-LEVEL-3-CORE], section 1.1.1) (must)。元文書の構造が変化しても、その変化が NodeList オブジェクトに反映されることは許されていません (must not)。つまり、返されるオブジェクトは、リストが生成された時点で文書に存在していたノードに対しクエリをかけ、マッチする Element ノードを取得することを意味します。

- [セレクタ API Level 1](http://standards.mitsue.co.jp/resources/w3c/TR/selectors-api/)

静的なノードリストなわけですね。具体的な例だと、

```javascript
var divs = document.getElementsByTagName("div"),
  i = 0;
while (i > divs.length) {
  document.body.appendChild(document.createElement("div"));
  i++;
}
```

getElementsByTagName()で返される値は動的なノードリストですので、上記のスクリプトは無限ループになる。

```javascript
var divs = document.querySelectorAll("div"),
  i = 0;
while (i < divs.length) {
  document.body.appendChild(document.createElement("div"));
  i++;
}
```

代わって、`querySelectorAll`で返される値は静的なノードリストで、取得してきた時点での数になります。つまり、div が 10 個そのときあったのであれば、その後に何個 div を生成しようが 10 回でこのループは止まります。

違いが分かりましたけど、なんでちゃうのん?

- [querySelectorAll が live じゃない NodeList 返すのはなんで？ - vantguarde - web:g](http://web.g.hatena.ne.jp/vantguarde/20081114/1226673398)

コメント欄に uupaa せんせが DOM アクセスを減らすためと書いてある。

おーなるほど、パフォーマンスのためか？と思ったのでもうちっと調べてみると、こんな記事があった。

- [Why is getElementsByTagName() faster than querySelectorAll()? - NCZOnline](https://www.nczonline.net/blog/2010/09/28/why-is-getelementsbytagname-faster-that-queryselectorall/)
- [getElementsByTagName()が querySelectorAll()より高速な理由 | マイナビニュース](http://news.mynavi.jp/articles/2010/10/01/javascript-nodelist-difference/)
- [2010-10-05 - 以下斜め読んだ内容](http://vwxyz.hateblo.jp/entries/2010/10/05)

上記ブログに書いてあることをなんとなく理解すると、静的リストはまるまるコピーするから事前にやることが多いので、動的リストよりも遅くなる。けども、取ってきたノードリストをイテレートする分には動的リストは毎回チェックするのに対して、静的リストはしないから速い。とのことみたいな事言ってるんだけど、

[jsPerf: JavaScript performance playground](http://jsperf.com/)でパフォーマンスチェックしてみたのが以下のテスト。ついでに、ほかの`getElementsBy*`メソッドもテストしてみた。

### getElementsByTagName VS querySelectorAll · jsPerf

- [getElementsByTagName VS querySelectorAll · jsPerf](http://jsperf.com/getelementsbytagname-vs-queryselectorall)
- [getElementsByTagName VS querySelectorAll · jsPerf](http://jsperf.com/getelementsbytagname-vs-queryselectorall/2)

### getElementsByName VS querySelectorAll · jsPerf

- [getElementsByName VS querySelectorAll · jsPerf](http://jsperf.com/getelementsbyname-vs-queryselectorall)
- [getElementsByName VS querySelectorAll · jsPerf](http://jsperf.com/getelementsbyname-vs-queryselectorall/2)

### getElementsByClassName VS querySelectorAll · jsPerf

- [getElementsByClassName VS querySelectorAll · jsPerf](http://jsperf.com/getelementsbyclassname-vs-queryselectorall)
- [getElementsByClassName VS querySelectorAll · jsPerf](http://jsperf.com/getelementsbyclassname-vs-queryselectorall/2)

なんか全部のテストで、（Opera を除いて）`getElementsBy*`（動的）が速いんですけど.でも、[このテスト](http://jsperf.com/getelementsbytagname-a-0-vs-queryselector-a/4)だと QSA の方が速い...うんーわからん。だれかおせーてエロい人！

結局、`getElementsBy*`で取れるもんはわざわざ、QSA でやらないほうがいいよ。ってことかな。あ、だからって QSA をディスってないよ。クラスの複数付けとか取ってくるときは QSA でやったほうが楽チンだし速い。と思ったけど、[このテスト](http://jsperf.com/the-benefit-of-using-the-selectors-api)だと getElementsByTagName の方が速いじゃん（High Perfromace JavaScript には QSA のほうが 2-6 倍速いって書いてあるのに...）

とりあえず、よく分かりません!
