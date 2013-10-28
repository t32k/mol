---
layout: post
title: JavaScript 第5版 6章 文
categories:
- javascript
tags: []
status: publish
type: post
published: true
meta:
  pvc_views: '2320'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/04/statements.html
  _edit_last: '1'
---
式：評価して値が生成されるもの
文：JavaScriptに何かをさせるもの

<h2>式文</h2>
副作用を伴う式（代入文など）
<pre><code>s = "Hello " + name;
alert("Welcome, " + name);</code></pre>
厳密に言えば、上記は式だが、Webブラウザに副作用をもたらすという点で文
文の最後には;を記述！


<h2>複合文</h2>
文の中に文が挿入された文（入れ子（ネスト）になった文は副文）
文ブロック：波括弧（{}）で複数の文をまとめて1つの文にする


<h2>if 文</h2>
<pre><code>if (expression) statement</code></pre>
expressionを評価し、trueであるかtrueに変換可能である場合statementを実行
falseの場合は実行しない
<pre><code>if ((addresss == null) || (address == "")) addresss = "undefined"; alert("メールアドレス入れろまいや");</code></pre>
改行とインデントでコードを見やすくしよう。
<pre><code>if (expression)　statement1else　statement2</code></pre>
true以外のときはstatement2を実行


<h2>else if 文</h2>
<pre><code>if (n == 1) {
　//#1を実行
　}　else if (n == 2) {
　　//#2を実行
　　}　else if (n == 3) {
　　　//#3を実行
　　　}　else {
　　　　//すべてのelseが成立しない時は#4を実行
}</code></pre>
if文が前の文のelse句の一部になってるだけのもんです。


<h2>switch文</h2>
条件分岐で使用する変数が1つだけの場合は複数のif文よりこっちがよろし
<pre><code>switch (expression) {　statements}</code></pre>
習うより慣れろってことでさっきのコードをswitch文に書きなおしてみると
<pre><code>switch (n ) {　
case 1;　　
　//#1を実行　
　break;　
case 2;　　
　//#2を実行　
　break;　
case 3;　　
　//#3を実行　
　break;
default;　　
　//どれにも当てはまらないときは#4を実行　
　break;
}</code></pre>
case句は開始点を示すだけで終了点を示さないのでbreak文が必要
関数内ので使うときはreturn文でもＯＫ
caseラベルには副作用をもつ式も記述できるがややこいので定数を使うほうがよい


<h2>while 文</h2>
<pre><code>while (expression) statements</code></pre>
expressionの評価がtrueならstatementを実行、またexpressionの評価に戻ち、falseになるまで実行
大抵のループ文ではcountのようなカウンタ変数使用する
<pre><code>var count = 0;while (count</code></pre>


<h2>do while 文</h2>
ループの本体が少なくとも1回は常に実行されるwhile文
使いどころがわからん（´・ω・｀）


<h2>for 文</h2>
ループ、whileより便利。
<pre><code>for (initialaize; test; increment)　statement</code></pre>
初期化、テスト、更新はループ変数の重要な要素
while 文との違い
<pre><code>initialaize;while (test)　statement　increment;</code></pre>


<h2>for/in 文</h2>
<pre><code>for (variable in object)　statement</code></pre>
variableは、変数、変数を宣言するvar文、配列要素、オブジェクトのプロパティのいずれかです。つまり、代入式の左側として適切なものでなければなりません。objectは、オブジェクト名、または評価するとオブジェクトになる式です。statementは、ループの本体を形成する文、または文ブロックです。
オブジェクトに属するプロパティをすべて調べたい時便利らしい。


<h2>ラベル文</h2>
<pre><code>identifier: statement</code></pre>
先頭に識別子、その後ろにコロン、最後に文を記述


<h2>break 文</h2>
break 文が実行されると最も内側のループまたはswitch文が直ちに終了します。


<h2>continue 文</h2>
continue 文は次の繰り返しからループの処理を再開します。


<h2>var 文</h2>
1つまたは複数の変数を明示的に宣言するときに、var文を使用
var文で生成されたプロパティはdelete演算子で削除できません。


<h2>function 文</h2>
関数を定義する時に使用。
<pre><code>function funcname(arg1 [, arg2 [..., argn]]]) {　statements}</code></pre>
引数はあってもなくてもよい。
波括弧必須。
if文やwhileループの一部として関数は定義できない、トップレベルでして
関数定義は実行されるのではなく、解析されるだけ


<h2>return 文</h2>
関数の本体でしか使えない。関数の値を返す。
return文が実行されると関数の途中であっても中断される。


<h2>throw 文</h2>
例外：ある種の例外的な条件やエラーが発生したことを示すシグナル。
それをスロー（投げる）文。


<h2>try/catch/funaly 文</h2>
try句：通常はこの句のコードが実行される。
catch句：tryブロックで投げられた例外の時だけ実行される
finally句：tryブロックが終了すると必ず実行される。なくてもいい。


<h2>with 文</h2>
<pre><code>with (object)　statement</code></pre>
with文を使用すると無駄が省ける。
<pre><code>frame[1].document.forms[0].address.value</code></pre>
↑こーゆの毎度アクセスするのめんどい
<pre><code>with(frame[1].document.forms[0]) {
    //ここからフォーム要素に直接アクセスできる
    name.vale = "";
    address.vale = "";
}</code></pre>
すっきりー！でも実行速度が遅いのとなんか思いがけない振る舞いをするので控えといたほうがよい。

上記のコードはこんなふうにでも書き換えられる。
<pre><code>var form = frame[1].document.forms[0];
form.name.vale = "";
form.address.vale = "";</code></pre>


<h2>空文</h2>
なにもしない。。。
意図的にやってるふうに　/*空文*/ ;って風に書くとよい式：評価して値が生成されるもの
文：JavaScriptに何かをさせるもの
疑問点


<h2>パーサーってなに？</h2>
<blockquote>パーサ 
構文解析をおこなうプログラム。構文解析器。</blockquote>
構文解析ってなんじゃい？
<blockquote>構文解析
ある文章の文法的な関係を説明すること(parse)。</blockquote>
ついでに字句解析ってのもでてくるけどなんじゃい？
<blockquote>字句解析
ソースコードを構成する文字の並びを、トークン (token) の並びに変換すること。
ここでいう「トークン」とは、意味を持つコードの最小単位のこと。</blockquote>
んで、どうやらコンパイル（プログラミングを処理する）工程は以下の5つに分けれるらしい。
<ol>
	<li>字句解析</li>
	<li>構文解析</li>
	<li>意味解析 → インタプリタ（実行）</li>
	<li>最適化</li>
	<li>コード生成</li>
</ol>


<h2>関数呼び出しスタックってなに？</h2>
まず英単語から、stack(スタック):積む
スタッキングチェアとか言いますね。
んで、ここでの『関数呼び出しスタック』ってのは
関数コールスタックということだろうと思い、 wikipediaの<a href="http://ja.wikipedia.org/wiki/%E3%82%B3%E3%83%BC%E3%83%AB%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF">コールスタック</a>を参照したところ、 図を見た感じだけど、関数の情報をもつスタックフレームを重ねたものをコールスタックというっぽい。
んで、問題のサイ本のP98には
<blockquote>例外が関数中でスローされていてその関数中に例外ハンドラが見つからない場合は、
その関数を呼び出したコードを調べます。このように例外は、関数呼び出しスタックをさかのぼっていきます。</blockquote>
って書いてあるので、関数呼び出しスタックってのは関数版のスコープチェインと考えられるかな。
つまり、内から外へ情報をさがす。これはスタックの構造（積み木）を考えれば、当然かなと。
一番後に積み上げた積み木が一番上となるので、一番最初に調べる。（後入れ先出しと言うらしい）
つまり、一番後に積み上げた：一番最後に定義された関数イコール一番入れ子になった関数から調べていくので合点がいく。 単に『スタック』を『階層』と置き換えて読んだ方がよさそう。
あんまり深入りすると大変そうだｗ
