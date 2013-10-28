---
layout: post
title: JavaScript 第5版 8章 関数
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
  blogger_permalink: /2009/05/functions.html
  _edit_last: '1'
  pvc_views: '3526'
---
関数：
一度の定義だけでプログラムから何度も実行や呼び出しが行えるJSのコード
メソッド：
オブジェクトを介して呼び出す関数

JSの関数は他のプログラミング言語で「サブルーチン」や「手続き」と呼ばれている
<h2>8.1 関数の定義と呼び出し</h2>
関数定義の書式
先頭にキーワードfunctionを記述
その後ろに関数の名前を指定

その後ろに引数を括弧で囲んで指定、引数が複数ある場合カンマで区切る。
引数は省略可能

関数の本体を構成する文を中括弧で指定。
<pre><code>// ショートカット関数 document.write() よりも便利なことも
// return文がないので未定義値が返る
function print(msg) {document.write(msg, "&lt;br&gt;");}</code></pre>
()演算子を使って呼び出す
（括弧の前には関数「名」でなくても、計算した結果が関数値になる式であればどんな式でも指定できる）
print("Hello" + name);

関数の引数のデータ型とか個数とかはJSチェックしない、うまいことやってくれる

<strong>入れ子型の関数</strong>
<pre><code>function hypotenuse(a, b){
 function square(x) { return x*x; }
 return Math.sqrt(square(a) + square(b));
}</code></pre>
入れ子型の関数は入れ子にする関数のトップレベルに定義しなければならない
if文やwhile文など文ブロックの中には定義できない。関数リテラルの場合はどこでもOK

<strong>関数リテラル</strong>
関数リテラルは匿名関数を定義する式
<pre><code>
</code></pre><pre><code>// function文
function f(x) { return x*x; }
</code></pre>
<pre><code>// 関数リテラル
var f = function(x) { return x*x; }</code></pre>

書式上は関数名を指定しても問題ない、自分自身を呼び出す再帰呼び出しする関数のとき便利
<pre><code>var f =  function fact (x) { if (x = 1) return 1; else return x*fact-(x-1); }</code></pre>
関数リテラルはJavaScriptの文ではなく式として生成されるので非常に柔軟で便利
<pre><code>f[0] = function(x) { return x*x; };
// 関数を定義し、変数に格納する a.sort(function(a,b){return a-b;});
// 関数を定義し、別の関数に渡す
var tensquared = (function(x){return x*x;})(10);
// 関数を定義してすぐに呼び出す</code></pre>
<strong>関数の命名規則</strong>
関数にはその名前の意味が分かるような、それでいて簡潔な名前を付けるように!
難しいな＞＜　アンダースコア形式で記述する（俺ルール）
<h2>8.2 関数の引数</h2>
関数の引数は任意の個数の引数を使って呼び出すことができる。
定義時の引数の数と同じじゃなくてもいい。
どんな型の値でも引数として渡せる

<strong>省略可能な引数</strong>
値が省略された引数には未定義値が設定される
呼び出し時に省略できる引数をもつような関数を定義する場合、
省略された引数に適切なデフォルト値が設定されなければならない
<pre><code>function copyPropertyNamesToArray(o, /* 省略可能 */ a) {
 if (!a) a = [];
 // 未定義値またはnullの場合は空の配列を生成する
 for(var property in o) a.push(property);
 return a;
}</code></pre>
関数をこのように定義しておくと引数を省略できる
<pre><code>var a = copyPropertyNamesToArray(o); 
// oのプロパティの名前を新しい配列に格納する
copyPropertyNamesToArray(p, a);   
// その配列にpのプロパティの名前を追加する</code></pre>
<strong>可変長の引数リスト（Arguments オブジェクト）</strong>
argumentsはArgumentsオブジェクトを参照する特別なプロパティ
Argumentsオブジェクトは「配列のような」オブジェクト
関数に渡された引数値はarguments[]配列の要素に格納され数値インデックスで参照できる
Argumentsオブジェクトにはcalleeプロパティも存在する
arguments.lengthで引数の個数を参照できる
<pre><code>function max(/* ...  */) {
 var m = Number.NEGATIVE_INFINITY;
 // 全ての引数を調べて最大値を見つける
 for(var i = 0; i ＜ arguments.length; i++)
 if (arguments[i] ＞ m) 
 m = arguments[i];
 // 最大値を返す
return m;
}</code></pre>
<pre><code>var largest = max(1, 10, 2, 3, 100, 1000);</code></pre>
↑これ任意の個数の引数を受け取ることが可能な関数を可変長引数関数またはvarags関数という

<strong>callee プロパティ</strong>
callee プロパティは現在実行中の関数を参照
callee プロパティを利用することで自分自身を再帰的に呼び出す匿名関数を記述できる
<pre><code>function (x) {if (x ＜= 1) return 1;return x * arguments.callee(x-1);}</code></pre>
<strong>引数としてオブジェクトのプロパティを利用</strong>
よくわからん＞＜

<strong>引数の型</strong>
JavaScriptは弱い型付き言語なので、型があってるかどうかチェックを入れる関数を盛り込むとよい
（だいぶ端折った＞＜）
コメントを利用する「省略可（optional）」など
<h2>8.3 データとしての関数</h2>
JavaScriptの関数はデータとして扱えるので変数に代入したり、
オブジェクトのプロパティや配列の要素に格納できちゃう、なんでもできちゃう
<pre><code>function square(x) { return x*x;  }</code></pre>
上記は新たに関数オブジェクトを生成し、squareという名前の変数に格納する
関数を別の変数に代入しても使える↓
<pre><code> var a = square(4);  
// aは数値の16になる
 var b = square;  
// bはsquareと同じ関数を参照する
 var c = b(5);  
// cは数値の25になる</code></pre>
関数はオブジェクトのプロパティにも格納可能、この場合関数はメソッドと呼ぶ
<pre><code>var 0 = new Object;
o.square =  function square(x) { return x*x;  }
y = o.square
// yの値は16</code></pre>
関数を配列の要素に格納すれば、関数の名前なしで関数を呼び出しできる
<pre><code>var a = new Array(3);
a[0] =  function square(x) { return x*x;  }
a[1] = 20;a[2] = a[0](a[1]);
// a[2]の値は400</code></pre>
<h2>8.4 メッソドとしての関数</h2>
オブジェクトを介して呼び出される関数をメソッドという
関数をf、オブジェクトoを、メソッドをmとすると次のように記述できる
<pre><code>o.m = f;  
// 格納
o.m();  
// 呼び出し
o.m(x, x+2);  
// 引数を２つ指定</code></pre>
メソッドを呼び出す時に使用したオブジェクトが、メソッドの本体の中でthisキーワードの値になる！
<pre><code>var calculator = {
 operand1: 1,
 operand2: 1,
 compute: function() {this.result = this.operand1 + this.operand2;}
};
calculator.compute();    
// 1+1を表示する
print(calculator.result); 
// 計算結果を表示する

rect.setSize(width, height);setRectSize(rect, width, height);</code></pre>
どちらのコードもオブジェクトrectに対して同じ操作をしているが、
操作の対象がオブジェクトrectであることは前者のほうが明らか。

関数がメソッドとしてではなく関数として呼び出された場合、thisキーワードはグローバルオブジェクトを参照。ややこいことに、メソッドとして呼び出された関数中に入れ子にされた別の関数が関数として呼び出された場合も、グローバルオブジェクトを参照
<h2>8.5 コンストラクタ関数</h2>
オブジェクトのプロパティを初期化する関数で、new演算子と一緒に使われる
<h2>8.6 関数のプロパティとメソッド</h2>
関数に対してtypeof演算子を使うと「function」が返るが実際は特殊なJavaScriptオブジェクト

<strong>lengthプロパティ</strong>
arguments配列のlengthプロパティ：引数リストで宣言された引数の個数
Functionオブジェクトののlengthプロパティ：ある関数で宣言された個数

<strong>prototypeプロパティ</strong>
どの関数にもあらかじめ定義されたプロトタイプオブジェクトを参照するprototypeプロパティがある

<strong>自分専用の関数プロパティの定義</strong>
<pre><code>//静的変数を生成し初期値を設定uniqueInteger.counter = 0;

function uniqueInteger() {return uniqueInteger.counter++;}</code></pre>
よくわからん＞＜

<strong>apply()メソッドとcall()メソッド</strong>
この２つのメソッドを利用するとあるオブジェクトのメソッドであるかのように関数を呼び出すことができる
よくわからん＞＜
<h2>8.7 ユーティリティ関数</h2>
なんか便利らしい＞＜
<h2>8.8 関数のスコープとクロージャ</h2>
難解なので飛ばす＞＜
<h2>8.9 Function() コンストラクタ</h2>
あんまり使われないらしい
<pre><code>var f =  new Function("x", "y", "return x*y");function f(x, y) {return x*y;}</code></pre>
上記は同じ意味。

<strong>Function() コンストラクタの特徴</strong>
JavaScriptのコードを実行時に動的に生成しコンパイルできる
Function() コンストラクタを使うたびに新しい関数オブジェクトが生成されるのでループや関数中で呼ぶな
Function() コンストラクタが生成する関数は静的スコープを使わん、常にトップレベルの関数としてコンパイルされる
関連リソース

<ul>
  <li><a href="http://builder.japan.zdnet.com/sp/javascript-kickstart-2007/story/0,3800083428,20364588,00.htm">JavaScriptのイロハ：「関数はオブジェクト」って理解できますか？ - builder by ZDNet Japan</a>
</li>
  <li><a href="http://builder.japan.zdnet.com/sp/javascript-kickstart-2007/story/0,3800083428,20371265,00.htm">JavaScriptの関数オブジェクトを完璧に理解する - builder by ZDNet Japan</a></li>
</ul>
