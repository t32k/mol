---
date: 2020-12-11
title: SwiftのOptional型とか
excerpt: なんかアンラップしろって言われたら、とりあえずビックリマークつけときゃいいんやなと雑に覚えてしまっっていたので、のちのち困ることになった。
ogimage: https://images-na.ssl-images-amazon.com/images/I/416ZqsPCCjL._SX393_BO1,204,203,200_.jpg
categories: 
    - swiftui
---

TypeScriptもあんまり使ったことなかったから、型がどうも苦手というか慣れない。 `Int` とか `String` とかそうゆうシンプルなものだと分かるが、そのシンプルな型をよくわからないものにするのがOptional型だと苦手意識を持っていた。

```swift
var a: String = "swift"
var b: String? = nil
var c: Optional<String> = nil
```

`b` と `c` は書き方が違うだけでどちらもオプショナルString型。まぁ`nil`を許容するかどうかって話なのだが、問題は扱い方。

```swift
var foo: Int? = 3
var bar: Int = foo + 1
```

`bar` のところでエラーになる。アンラップしろよとかなんとか注意される。

## アンラップ（開示）

なんでや!! `foo` に3が代入されとるのは明らかやろ！と思っていたが、アンラップしろと言われているので、とりあえずアンラップしてみる。

```swift
var foo: Int? = 3
var bar: Int = foo! + 1
```

`foo` は `Optional<Int>` であって、 `Int` ではないので、違う型同士で足し算はできない。そこで、オプショナルIntからIntを取り出さなければならない。これをアンラップといい、上記のようにビックリマークをおしりにつける。そうするとちゃんと計算を実行できるようになる。

なんかアンラップしろって言われたら、とりあえずビックリマークつけときゃいいんやなと雑に覚えてしまっっていたので、のちのち困ることになった。

```swift
var foo: Int?
var bar: Int = foo! + 1
```

`foo` に値が代入されていない場合、アンラップしても `nil` が返ってくるのでエラーになる。

## オプショナルバインディング (if-let文)

```swift
var foo: Int? = 3
if let f = foo {
    print("答えは\(f + 1)です")
} else {
    print("答えは1です")
}
```

もし値が入ってなかったら、違う処理を記述したいと思う。そうゆうときは `if let　~ { }` みたいな感じの構文を書く。これをオプショナルバインディングと呼ぶ。

`foo` に値があれば、`f` に代入されて、答えは4です。とprintされるが、`foo` が `nil` だったら、else節に飛び、答えは1です。とエラーにならずにprintされる。

## guard文

```swift
var foo: String?
func printStr(message: String?) {
    guard let str = message else {
        print("nilです")
        return
    }
    print(str)
}
printStr(message: foo)
```

guard文でも似たようなことができる。 `guard 条件 else { /* returnやbreak */ }` と書いて、条件が成立しなかった場合、else節にとび、処理を中断したりできる。

## nil合体演算子(Nil-Coalescing Operator) 

```swift
(foo != nil) ? foo! : "にる！"
```

`foo` が `nil` じゃなかったらその値を使って、 `nil` なら `にる！`を使うみたいな条件を、三項演算子で書くとこうなるが、`??` のnil合体演算子を使うともっとシンプルにこう書ける。

```swift
foo ?? "にる！" 
```

便利。

## まとめ

とまぁ、そんなムズカシイことではないんだけど。実際のユースケースで体験してこなかったので、身についてなかったんだと思う。

今、図書管理アプリを作っているのだが、本の情報をGoogle Books APIを叩いてとってきている。しかし、この取ってきたデータに著者情報があったりなかったり、サブタイトルがあったりなかったりと結構チグハグなデータだったのだ。

```swift
struct Book {
    var id: String
    var author: String?
    var title: String
    var subtitle: String?
    var description: String?
    var imageLinks: ImageLinks?
    var publisher:  String?
    var publishedDate: String?
}
```

モデルで表すとこんな感じで、やたらOptional型を多用することになったので、今回Optionalとちゃっと向き合ってみたのだ。

```swift
Vstack {
  Text(book.title)
  Text(book.subtitle ?? "")
  if let d = publishedDate {
    Text("出版年: \(d)")
 }
  Text("著者: \(book.author ?? "不明")")
}
```

SwiftUIで画面を構築するときもこんな感じで、値がなかったときの表示の仕方や、デフォルト値を表示するなど、今回学んだことを大いに活用した。

もう、Optinal型なんて怖くない＞ｍ＜！

<div class="__media"><a href="https://www.amazon.co.jp/dp/4815604061/?tag=warikiru-22" target="_blank" rel="noopener">
<img src="https://images-na.ssl-images-amazon.com/images/I/416ZqsPCCjL._SX393_BO1,204,203,200_.jpg" alt="" class="__media__image">
<div class="__media__body">
    <div>SwiftUI 徹底入門</div>
    <div class="__media__text">金田 浩明</div>
    <div>Amazon.co.jpで詳細を見る</div>
</div>
</a></div>
