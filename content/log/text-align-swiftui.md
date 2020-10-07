---
date: 2020-09-28
title: SwiftUIでの文字寄せとか
excerpt: まず初めに、文字寄せだが、テキストを左寄せ・右寄せにしたいときどうすればよいんだろうと思った
ogimage: https://t32k.me/mol/images/2020/0928/01.png
categories: 
    - swiftui
---

最近、SwiftUIデビューをした。太古の昔にTitanium MobileでiOSアプリを作ったことはあるが、基本Web畑で育ってきたt32kにとっては、iOSというかSwiftというかSwiftUIでのユーザーインターフェイス作成は、まるで外国での生活のようで、いろいろカルチャーギャップを感じる。そうゆうことを書きたい。

まず初めに、文字寄せだが、テキストを左寄せ・右寄せにしたいときどうすればよいんだろうと思った。Xcodeでプロジェクトを作成すると`Hello World!`の文字列を表示するボイラープレートが用意されている。

![](/mol/images/2020/0928/01.png)

この文字列は上下・左右・真ん中に表示されている。これを左寄せにしたい。Webでいう、`text-align: left`は、SwiftUIではどうするんだろうと私は考える。

![](/mol/images/2020/0928/02.png)

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .frame(alignment: .leading)
    }
}
```

`frame`モディファイアで`aligment`というプロパティがあるのでそれに`.leading`２セットすればよいらしい。

なるほど。動かない。

それもそのはずだ、Textビューのサイズ（青枠）を見ればわかる。文字でいっぱいいっぱいなので、どちらか片方に寄せれないっぽい。

![](/mol/images/2020/0928/03.png)

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .frame(maxWidth: .infinity, alignment: .leading)
    }
}
```

Frameのサイズを画面いっぱいにひろげてみると、なるほどな、左に寄せることができた。ちなみに右寄せの場合は`.trailing`だ。

またStackOveflowでこうゆう回答も見かけた。

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            HStack {
                Text("Hello, World!")
                Spacer()
            }
            HStack {
                Spacer()
                Text("Hello, World!")
            }
        }
    }
}
```

`Spacer()`使うと楽だぜヒャッハーという。これだと`Spacer()`が目一杯広がるので、frameのwidthを明示的に指定しなくてもいいし楽っぽい。

でもSpacerというものWebでは邪道と言われ続けたスペーサーGIFのようなものと感じるので、あまり頼りすぎるのではよくないのではないかと思った。`alignment`で明示的に文字寄せを表現しているのは意味的に正しいと思う。

てか、そもそもなんで `text-align:left/right` を `.leading/.trailing` というのか考える必要がある。iOSはアラビア語圏などにも対応している。つまり右から左へ読む文化だ。つまり`.leading`と指定した文字寄せは日本語圏などは左になるが、アラビア語圏などでは右に配置されるので、__先頭__ が変わるから`left/right`という名前なんだと理解した。なるほど、多言語文化対応だ。

```swift
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
      ContentView().environment(\.layoutDirection, .rightToLeft)
    }
}
```

というわけで、環境変数レイアウト方向にRTLにセットしてみると、

![](/mol/images/2020/0928/04.png)

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, alignment　左")
                .frame(maxWidth: .infinity, alignment: .leading)
            Text("Hello, alignment　右")
                .frame(maxWidth: .infinity, alignment: .trailing)
            
            HStack {
                Text("Hello, spacer 左")
                Spacer()
            }
            HStack {
                Spacer()
                Text("Hello, spacer 右")
            }
            
            HStack {
                Text("左")
                Spacer()
                Text("右")
            }
        }
    }
}
```

`alignment`で指定した文字寄せは予想通り、反対になっている。予想外だったのは`Spacer()`で文字寄せしたコードも反対になっている点だ。レイアウト方向にRTLになると`HStack`(横方向に並べるやつ)の並びも反転するのか。。。これは頭がよいのか、おせっかいなのかよくわからないけど、注意する必要がある。

まぁ、そんな感じで文字寄せひとつとってもいろいろ発見があるなーと思いました（こなみかん）

<div class="__media"><a href="https://www.amazon.co.jp/dp/4815604061/?tag=warikiru-22" target="_blank" rel="noopener">
<img src="https://images-na.ssl-images-amazon.com/images/I/416ZqsPCCjL._SX393_BO1,204,203,200_.jpg" alt="" class="__media__image">
<div class="__media__body">
    <div>SwiftUI 徹底入門</div>
    <div class="__media__text">金田 浩明</div>
    <div>Amazon.co.jpで詳細を見る</div>
</div>
</a></div>
