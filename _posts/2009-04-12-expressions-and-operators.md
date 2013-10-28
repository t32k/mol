---
layout: post
title: JavaScript 第5版 5章 式と演算子
categories:
- javascript
tags:
- sai5
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/04/expressions-and-operators.html
  pvc_views: '2598'
  _edit_last: '1'
  _wp_old_slug: javascript-%e7%ac%ac5%e7%89%88-5%e7%ab%a0%e3%80%80%e5%bc%8f%e3%81%a8%e6%bc%94%e7%ae%97%e5%ad%90
---
<b>式</b>：JavaScriptインタプリタが評価して値を生成できるもの（リテラルや変数）
<b>リテラル</b> = リテラル式
<b>演算子</b>：式を組み合わせる役目
単項演算子、二項演算子、三項演算子
Precedence (優先順位)
Associativity (結合性)
<blockquote><a href="http://e-words.jp/w/E382AAE3839AE383A9E383B3E38389.html">オペランド　【operand】</a>
  コンピュータプログラミングにおいて、演算の対象となる値や変数のこと。演算内容をあらわす記号などは「演算子」または「オペレータ(operator)」という。例えば「A+10」という式では、「A」と「10」がオペランドで、「+」がオペレータである。
</blockquote>
オペランドの型
JSは可能な限り式を適切な型に変換しようと試みる
<b>左辺値</b>：代入文の左側に記述してもよい式という意味
演算子の優先順位
w = x + y*Z;　→　w = (x + y)*z;
数学の式と同じ感じ。括弧を利用することで明示的に評価順序を指定
算術演算子
<ul>
  <li>加算演算子（+）：数値の加算もしくは文字列の連結</li>
  <li>減算演算子（-）：数値の減算（オペランドが数値でない場合はオペランドは数値に変換）</li>
  <li>乗算演算子（*）：数値の乗算（オペランドが数値でない場合オペランドは数値に変換）</li>
  <li>除算演算子（/）：数値の除算（オペランドが数値でない場合オペランドは数値に変換）</li>
  <li>乗除算演算子（%）：割った余り</li>
  <li>単項マイナス（-）：オペランドの前に置いて使用。正負を変更</li>
  <li>単項プラス（+）：明示的に示すだけで特に何もしない</li>
</ul>


<b>インクリメント演算子</b>（++）：オペランドに1を加える。置く位置によってプレインクリメント、ポストインクリメントがある。
<pre><code>i = 1;
j = ++1; //iもjも2
i = 1;
j = i++; //iは2だが、jは1</code></pre>
インクリメント演算子はループカウンタでよく使われる。
<b>デクリメント演算子</b>（--）：インクリメントの反対
<b>等値演算子</b>（==）と<b>同値演算子</b>（===）
等値演算子：緩やかに型変換を行いながら値を比較してて2つのオペランドが「等しい」かどうか調べる
null == undefinedはtrue
片方が数値で片方が文字列の場合、文字列を数値に変換してから比較
片方がtrueで1に変換、片方がfalseで0に変換
"1" == true はtrue!
同値演算子：厳密に比較して2つのオペランドが「同一」であるか調べる
同じ型でないとダメ
NaN値はどの値とも同一になりません。
true,true、false,false、null,null、undefined,undefinedでOK
この逆の不等演算子（!=）と非同値演算子（!==）がある
関係演算子
比較演算子
小なり演算子（< ） 、大なり演算子（>）、小なりイコール演算子（< =）、大なりイコール演算子（>=）
trueとfalseを返す（※大文字は小文字をよりも「小さい」）
in 演算子
左側の値が右側のオブジェクトのプロパティ名であれば、trueを返す。

<pre><code>var hoge = {x:1, y:1 };
"x" in hoge // true
"z" in hoge // false</code></pre>
instanceof 演算子
左側のオブジェクトが右側のクラスのインスタンスであれば、trueを返す。

<pre><code>var d = new Date();
d instanceof Date; // true
d instanceof Object; //true すべてのオブジェクトはObjectクラスのインスタンス
d instanceof Number; // false</code></pre>

文字列演算子
現場で慣れろｗ
論理演算子
論理積演算子（&amp;&amp;）：true,trueでtrue
論理和演算子（||）：どちらか一方がtrueならtrue
論理否定演算子（!）：オペランドの論理値を反転
ビット演算子
パスｗ
代入演算子（=）
算術演算を伴う代入演算子
<pre><code>a op = b　→　 a = a op b</code></pre>
その他の演算子
<b>条件演算子</b>（<b>?:</b>）：if文みたいな事が簡潔に書けるよ
typeof 演算子：単項演算子。オペランドのデータ型を示す文字列に返す
number,string,boolean,object,function,undefined
オブジェクト生成演算子（new）：新しいオブジェクトを生成し、そのオブジェクトを初期化するためにコンストラクタ関数を呼び出す
delete 演算子：オペランドに指定されたオブジェクトプロパティや配列要素、変数を削除
void 演算子：undefinedを返す
カンマ演算子：for文でよく使う
配列とオブジェクトにアクセスする演算子（[] .）
関数呼び出し演算子（()）()
