---
date: 2011-01-02
title: querySelectorとquerySelectorAllというかLive NodeListとStatic NodeList
categories: javascript
---

先日、`getElementsByClassName`便利だぜ！とブログに書いたら、to-Rの西畑先生より`querySelectorAll`アルヨ！と言われたので、調べてみる。

## querySelectorとquerySelectorAll

+ [IE8 で実装された Selectors API とは何か？ - IT戦記](http://d.hatena.ne.jp/amachang/20080306/1204787459)

まぁ上記エントリにほぼ全てが書かれているので、特に今さら書くことはないのですが、自分メモのために。

なにはともあれ、サポート状況をば。

+ [DOM Core](http://quirksmode.org/dom/core/)

Fx3.0は対応していないけど、IE8は対応してるのか。素敵！

```javascript
element = document.querySelector(selectors);
```

+ [Document.querySelector() - Web API Interfaces | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)

`querySelector`ってのもある。基本的な使い方は両方一緒で`selectors</em`の引数に、取得したい要素のCSSセレクタ書いてあげればいい。`querySelector`は最初に見つけてきた単一の要素を返すのに対して、

> 
```javascript
elementList = document.querySelectorAll(selectors);
```
elementList is a non-live NodeList of element objects.

+ [Document.querySelectorAll() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)

querySelectorAll はノードリストを返す。

```javascript
var node = document.querySelectorAll('#hoge > h2');
```

つまり、`#hoge`の中の子供のh2だけを取ってくるなんてことも、上記のようにCSSセレクタで簡単に書けちゃう。jQueryライクに書けちゃう。だから、これまでFirefoxのグリモンとかChromeの拡張機能を作成するときは僕はjQuery読み込んでいたんだけど、簡単なものであればSelectors API使えば、jQueryに頼らなくても良くなった。

## Live NodeListとStatic NodeList

はい、そんなわけでSelectors API＼(-o-)／なんですけども、ひとつ気になる点がありました。`querySelectorAll`が返すのはnon-liveなノードリストと書いてあります。non-liveって何よ？ってことで、仕様書、仕様書

<blockquote>querySelectorAll() メソッドから返される NodeList オブジェクトは 動的 (live) ではなく、静的 (static) である必要があります ([DOM-LEVEL-3-CORE], section 1.1.1) (must)。元文書の構造が変化しても、その変化が NodeList オブジェクトに反映されることは許されていません (must not)。つまり、返されるオブジェクトは、リストが生成された時点で文書に存在していたノードに対しクエリをかけ、マッチする Element ノードを取得することを意味します。<a href="http://standards.mitsue.co.jp/resources/w3c/TR/selectors-api/">
セレクター API Level 1</a></blockquote>

ほほー静的なノードリストなわけですね。具体的な例ですと、

```javascript
var divs = document.getElementsByTagName("div"),
    i=0;
while(i > divs.length){
 document.body.appendChild(document.createElement("div"));
 i++;
}
```

getElementsByTagName()で返される値は動的なノードリストですので、上記のスクリプトは無限ループになる。
<pre><code>var divs = document.querySelectorAll("div"),
    i=0;
while(i &lt; divs.length){
 document.body.appendChild(document.createElement("div"));
 i++;
}</code></pre>
代わって、querySelectorAllで返される値は静的なノードリストで、取得してきた時点での数になります。つまり、divが10個そのときあったのであれば、その後に何個divを生成しようが10回でこのループは止まります。

違いが分かりましたけど、なんでちゃうのん？
<ul>
	<li><a href="http://web.g.hatena.ne.jp/vantguarde/20081114/1226673398">querySelectorAllがliveじゃないNodeList返すのはなんで？ - vantguarde - web:g</a></li>
</ul>
コメント欄にuupaaせんせがDOMアクセスを減らすためと書いてある。

おーなるほど、パフォーマンスのためか？と思ったのでもうちっと調べてみると、こんな記事があった。
<ul>
	<li><a href="http://www.nczonline.net/blog/2010/09/28/why-is-getelementsbytagname-faster-that-queryselectorall/">Why is getElementsByTagName() faster that querySelectorAll()? | NCZOnline</a></li>
	<li><a href="http://journal.mycom.co.jp/articles/2010/10/01/javascript-nodelist-difference/index.html">【レポート】getElementsByTagName()がquerySelectorAll()より高速な理由  | マイコミジャーナル</a></li>
	<li><a href="http://d.hatena.ne.jp/vwxyz/20101005">Nicholas C. Zakas「getElementsByTagName()がquerySelectorAll()よりも高速な件」 - クライアント・サイド・スクリプティング with Web Standards</a></li>
</ul>
上記ブログに書いてあることをなんとなく理解すると、静的リストはまるまるコピーするから事前にやることが多いので、動的リストよりも遅くなる。けども、取ってきたノードリストをイテレートする分には動的リストは毎回チェックするのに対して、静的リストはしないから速い。とのことみたいな事言ってるんだけど、

<a href="http://jsperf.com/">jsPerf</a> ってところでパフォーマンスしてみたのがこれ。ついでに、ほかのgetElementsBy*メソッドもテストしてみた。

<strong>getElementsByTagName VS querySelectorAll · jsPerf</strong>
<ul>
	<li><a href="http://jsperf.com/getelementsbytagname-vs-queryselectorall">http://jsperf.com/getelementsbytagname-vs-queryselectorall</a></li>
	<li><a href="http://jsperf.com/getelementsbytagname-vs-queryselectorall/2">http://jsperf.com/getelementsbytagname-vs-queryselectorall/2</a></li>
</ul>
<strong>getElementsByName VS querySelectorAll · jsPerf</strong>
<ul>
	<li><a href="http://jsperf.com/getelementsbyname-vs-queryselectorall">http://jsperf.com/getelementsbyname-vs-queryselectorall</a></li>
	<li><a href="http://jsperf.com/getelementsbyname-vs-queryselectorall/2">http://jsperf.com/getelementsbyname-vs-queryselectorall/2</a></li>
</ul>
<strong>getElementsByClassName VS querySelectorAll · jsPerf</strong>


<ul>
	<li><a href="http://jsperf.com/getelementsbyclassname-vs-queryselectorall">http://jsperf.com/getelementsbyclassname-vs-queryselectorall</a></li>
	<li><a href="http://jsperf.com/getelementsbyclassname-vs-queryselectorall/2">http://jsperf.com/getelementsbyclassname-vs-queryselectorall/2</a></li>
</ul>

なんか全部のテストで、（Operaを除いて）getElementsBy*（動的）が速いんですけど。。。でも、<a href="http://jsperf.com/getelementsbytagname-a-0-vs-queryselector-a/4">このテスト</a>だとQSAの方が速い。。。うんーわからん。だれかおせーてエロい人！

結局、`getElementsBy*`で取れるもんはわざわざ、QSAでやらないほうがいいよ。ってことかな。あ、だからってQSAをディスってないよ。クラスの複数付けとか取ってくるときはQSAでやったほうが楽チンだし速いからね。と思ったけど、<a href="http://jsperf.com/the-benefit-of-using-the-selectors-api">このテスト</a>だとgetElementsByTagNameの方が速いじゃん（High Perfromace JavaScriptにはQSAのほうが2-6倍速いって書いてあるのに...）

とりあえず、よく分かりません。