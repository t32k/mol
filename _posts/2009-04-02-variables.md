---
layout: post
title: JavaScript 第5版 4章 変数
categories:
- javascript
tags:
- sai5
status: publish
type: post
published: true
meta:
  pvc_views: '1996'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/04/variables.html
  _edit_last: '1'
---
<b>変数</b>：値に関連付けられる名前。変数に値を代入（格納）すると言う
JavaScriptには型という考え方がない
↑自動的に型変換してくれる←コードが簡潔になる
変数は使用する前に宣言しなければならない

<pre><code>var i; // 宣言してるだけ
var i = 0; // 宣言して初期化してる</code></pre>

暗黙的に宣言された変数は必ずグローバル変数となる（関数の内部であっても）
<b>変数を宣言するときは必ずvar文を使用すべし！</b>

<b>スコープ</b>：変数の有効範囲
グローバル変数のスコープ：プログラム<b>全体で有効</b>
ローカル変数のスコープ：宣言された<b>関数の内部</b>だけ
ブロックレベルのスコープはない
ある関数で宣言されたすべての変数はその関数全体で有効
<b>変数は関数の先頭でまとめて宣言するべし！</b>

<b>未定義 </b>宣言されていない変数
<b>未代入 </b>宣言はされているが、値が設定されていない変数（未設定変数）

<b>基本型 </b>数値、論理値、null、未定義値
<b>参照型 </b>オブジェクト、配列、関数
8バイトのメモリでは格納できないから参照するの。

文字列は特殊だが基本型と考えてもよい。

<b>ガーベジコレクション</b>
自動的にメモリを解放してくれる。気にしなくてもいい。

<b>オブジェクトのプロパティと変数は実は同じ</b>

<b>グローバルオブジェクト</b>：JavaScriptコードが実行される前に生成される
グローバルオブジェクトのプロパティ：グローバル変数
トップレベルコード：関数の一部ではないコード
クライアントサイドJSのグローバルオブジェクトはWindowオブジェクト
ローカル変数は<b>Callオブジェクト</b>のプロパティ

1つのJavaScriptインタプリタ上に、スクリプトを実行するグローバル実行テキストは複数存在できる。
これらの実行コンテキストはそれぞれ独立していて相互参照可能。

<b>スコープチェーン</b>：オブジェクトを並べたもの。先頭から変数を探す。
例）子callオブジェクト→親callオブジェクト→グローバルオブジェクト
<pre><code>var x = 0;

function func1() {
    var x = 1;

    function func2() {
        var x = 2;

        function func3() {
            var x = 3;
            alert(x); // ここでは3が表示
        }
        alert(x); // ここでは2が表示
    }
    alert(x); // ここでは1が表示
}
alert(x); // ここでは0が表示</code></pre>

<h2>疑問点</h2>
ブロックレベルとは？
ブロック文（波カッコで囲まれた文）というのがあるらしく。そのレベルということ。
ブロック文は通常、制御フロー文（例：if、for、while）で使われるらしいです。

詳しくは<a href="https://developer.mozilla.org/ja/Core_JavaScript_1.5_Guide/Block_Statement">Block Statement - MDC</a>
