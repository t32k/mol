---
date: 2020-10-01
title: SwiftUIでの余白のとりかたとか
excerpt: こんなの片腕をもがれた状態じゃないか！と思ったが、SwiftUIでは、どうやら勝手が違うようである。
ogimage: https://t32k.me/mol/images/2020/1001/02.png
---

Webレイアウトを組むにあたってMargin/Paddingは非常に重要だ。しかし、SwiftUIにおいてPaddingモディファイアはあるがMarginのそれはない。こんなの片腕をもがれた状態じゃないか！と思ったが、SwiftUIでは、どうやら勝手が違うようである。

![](/mol/images/2020/1001/00.png)

```swift
struct ContentView: View {
    var body: some View {
        HStack(spacing: 40) {
            Text("タグ１")
                .padding()
                .background(Color.yellow)
            Text("タグ2")
                .padding()
                .background(Color.blue)
        }
    }
}
```

上記のように、タグのようなものを横並びにしたいと思ったとき、Marginがないので、どこでタグ間の余白を調整すればよいのかと思っていた。とりあえず、親のHStackに`spacing`プロパティを持つことができるので、ここでMarginの役割をもたせていた。

あとから気づいたが、これは実にWeb的な考え方である。つまりCSSボックスモデルの呪縛からの脱却が必要だ。

![](/mol/images/2020/1001/01.png)　

> [ボックスモデル | MDN](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model)　より

CSSボックスモデルとは上図のように、一番内側にコンテンツがあり次にPaddingとBorder、Marginと広がっていく。なので、一つのCSSセレクタにPadding/Border/Marginのプロパティは１回しか適用できない。この考えが私の頭にこびりついていたのだ。

![](/mol/images/2020/1001/02.png)　
```swift
struct ContentView: View {
    var body: some View {
        Text("コンテンツ")
            .padding()
            .background(Color.yellow)
            .padding()
            .border(Color.red, width: 1)
            .padding()
            .padding()
            .border(Color.green, width: 1)
            .padding()
    }
}
```

実際のSwiftUIにそんなCSSボックスモデルのような制約はない。Paddingは何回使ってもいいし、Borderも何回でもかけることができる。Borderの次にPaddingを指定すれば、Webで言うMargin的な使い方もできる（青枠はデバッグ用のView表示領域）。

ゆえにスタイリングのためにDIVを何個も入れ子にする必要はないのである。当初はMargin以上にDIV的なViewはないのかな？とよく思ったものであるが、そもそも最初からSwiftUIに必要なかったのである。

![](/mol/images/2020/1001/03.png)　
```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("コンテンツ")
                .padding()
                .background(Color.yellow)
            Divider()
            Text("コンテンツ")
                .background(Color.yellow)
                .padding()
        }
    }
}
```

ただ、モディファイアの宣言順序は気をつける必要がある。コンテンツと余白に背景色を塗りたい場合は、最初にPaddingを指定しなければならなかったりとか。まぁ言い換えれば宣言順序どおりにSwiftUiはレンダリングしていくのだなと理解すればよい。

![](/mol/images/2020/1001/04.png)　
```swift
struct ContentView: View {
    var body: some View {
        Text("コンテンツ")
            .padding(.leading, 1)
            .padding(.trailing, 2)
            .padding(.top, 3)
            .padding(.bottom, 4)
            .padding(.vertical, 5)
            .padding(.horizontal, 6)
            .padding(.all, 7)
            .padding(EdgeInsets(top: 1, leading: 2, bottom: 3, trailing: 4))
            .background(Color.yellow)
    }
}
```

最後にPaddingの値の指定のしかた一覧を書いて終わりにする。

<div class="__media"><a href="https://www.amazon.co.jp/dp/4815604061/?tag=warikiru-22" target="_blank" rel="noopener">
<img src="https://images-na.ssl-images-amazon.com/images/I/416ZqsPCCjL._SX393_BO1,204,203,200_.jpg" alt="" class="__media__image">
<div class="__media__body">
    <div>SwiftUI 徹底入門</div>
    <div class="__media__text">金田 浩明</div>
    <div>Amazon.co.jpで詳細を見る</div>
</div>
</a></div>
