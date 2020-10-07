---
date: 2020-10-07
title: SwiftUIでの色とか
excerpt: 書き方の違いなんだろうか？と思ってたけど、全然違った。
ogimage: https://t32k.me/mol/images/2020/1007/00.png
categories: 
    - swiftui
---

UIKitの`UIColor`とSwiftUIの`Color`は違うと気づいた最近。

例えば、赤色を表示したいときは、SwiftUIでは `Color.red` と書く。たまに`Color(.red)` というのも見かけて、書き方の違いなんだろうか？と思ってたけど、全然違った。`Color(.red)` は `Color(UIColor.red)` の略した書き方で、`UIColor` をSwiftUIの`Color`として使う方法だった。

ややこしいのは`Text("hoge").foregroundColor(.red)`のようなケース。文字色を赤色にしたいとき、foregroundColorモディファイアは`Color`が引数に来ると想定しているので、`foregroundColor(Color.red)`と同じである。もし、UIColorの方の赤を指定したかったら、`foregroundColor(Color(.red))`と書かなければならない。

ちなみに、赤色としても微妙に違う。

![](/mol/images/2020/1007/00.png)

```swift
struct ContentView: View {
    var body: some View {
        HStack {
            ZStack {
                Rectangle().foregroundColor(Color(.red))
                Text("UIColor").foregroundColor(.white)
            }
            ZStack {
                Rectangle().foregroundColor(Color.red)
                Text("SwiftUI's Color").foregroundColor(.white)
            }
        }
    }
}
```

どうして、気づくの時間がかかったかというと、今作成しているのはモックアプリでシステムカラーしか使ってなかったためである。つまり、`Color(.	systemRed)`のような書き方で統一していたというか、システムカラーは`UIColor`なので、そう書かざるをえなかった。

![](/mol/images/2020/1007/01.png)

システムカラーを使うと、ダークモードのときや、アクセシビリティモードのときに適切な色味に変換してくれるメリットがある。つまり、システムカラーさえ使っとけば、おーるおっけー。やったね 🤗

気をつけなければならないのは、黒や白といったものである。コンポーネントの背景色を白色にしたいと思って、安易に `Color.white` を使わない。当たり前だが`Color.white` はダークモードのときも白色だがアプリ全体の背景色は黒色になる。そうしたとき、想定していない見た目になるかもしれな。そうゆうときは `Color(.systemBackground)`を使うと良い。文字色も`Color(.label)`を使うと、黒と白が反転して良い感じになる。

![](/mol/images/2020/1007/02.png)

濃淡を使い分けたかったら、`SystemGray`を使うと良い。

CSSだけど、[このブログをダークモードに対応](/mol/log/dive-into-the-dark-side/)したとき、めんどくさかったんだよなと思い出した。そういう意味では、ダークモードだけでなくアクセシビリティモードのときのカラーセットもはじめから用意してくれているiOS様様である。

- [Color \- Visual Design \- iOS \- Human Interface Guidelines \- Apple Developer](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/color/)

<div class="__media"><a href="https://www.amazon.co.jp/dp/4815604061/?tag=warikiru-22" target="_blank" rel="noopener">
<img src="https://images-na.ssl-images-amazon.com/images/I/416ZqsPCCjL._SX393_BO1,204,203,200_.jpg" alt="" class="__media__image">
<div class="__media__body">
    <div>SwiftUI 徹底入門</div>
    <div class="__media__text">金田 浩明</div>
    <div>Amazon.co.jpで詳細を見る</div>
</div>
</a></div>
