---
layout: post
title: JavaScript 第5版 3章 データ型と値
categories:
- javascript
tags:
- sai5
status: publish
type: post
published: true
meta:
  pvc_views: '2695'
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/03/datatypes-and-values.html
  _edit_last: '1'
---
<h2>数値</h2>
整数リテラル：数のこと
浮動小数点リテラル
<h2>文字列</h2>
文字列リテラル：文字のこと。引用符で囲む。
エスケープシーケンス：バックスラッシュ（日本語環境では円記号）を使って制御コードを表す文字
（ex. \nは改行）
<h2>論理値</h2>
trueとfalse (数値コンテキストでは0と1に変換)
<h2>複合データ型</h2>
オブジェクト：複数の基本型や複合型の値の集合（連想配列としても使える）
オブジェクトの生成：コンストラクタ関数、オブジェクトリテラル（｛プロパティ名：値, プロパティ名：値｝入れ子も可能）
プロパティ（フィールド）：オブジェクトに格納されている値
メソッド：プロパティに代入されている関数
配列：データにインデックスを付けて順序付けてまとめたもの。文字列を添え字とする配列のことを「連想配列（ハッシュ）」
配列の生成：Array()コンストラクタ、配列リテラル（[値, 値, 値]入れ子も可能）
関数：実行可能なコード（数値や文字列と同じく値なのでプロパティに代入可能）
関数定義3つ、function文、関数リテラル（で定義された関数はラムダ関数と呼ぶこともある）、Function()コンストラクタ（あまり使わない）
<pre><code>// function文
function add(x, y) {
    return x + y;
}</code></pre>
<pre><code>// 関数リテラル
var add = function (x, y) { return x + y; };</code></pre>
<pre><code>// Function()コンストラクタ
var add = new Function('x', 'y', 'return x + y');</code></pre>
その他のデータ型

null：値がないことを表す特殊な値
undefined：未定義、設定されていない変数、存在しないオブジェクトプロパティにアクセスした時に返される。
Dateオブジェクト
正規表現
Errorオブジェクト
トークン：プログラミング言語のソースコードを構成する単語や記号の最小単位。
ビルトインオブジェクト：JSにあらかじめ用意されているオブジェクトがいくつかある。
<blockquote>（）
丸括弧（まるかっこ）は、小括弧（しょうかっこ）、パーレンとも言う
｛｝
波括弧（なみかっこ）は、ブレース、ブレイス (brace) とも言う。なお、中括弧（ちゅうかっこ）と呼ばれることもある
［］
角括弧（かくかっこ）は、ブラケット (bracket) とも言う。また、大括弧（だいかっこ）と呼ばれる</blockquote>
<a href="http://ja.wikipedia.org/wiki/%E6%8B%AC%E5%BC%A7">http://ja.wikipedia.org/wiki/括弧</a>
