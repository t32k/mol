---
date: 2021-02-24
title: SegmentedPickerによるビュー切り替えトランジション
categories:
  - swiftui
ogimage: https://t32k.me/mol/images/2021/0224/02.png
excerpt: うん、なんかそれっぽくなった🤗
---

まぁ題名の通り。

```swift
struct ContentView: View {
    @State private var selection = 0
    var body: some View {
        VStack(spacing:0) {
            Picker("画面切替", selection: self.$selection) {
                Text("A").tag(0)
                Text("B").tag(1)
            }.pickerStyle(SegmentedPickerStyle()).padding()
            
            if selection == 0 {
                viewA
            } else {
                viewB
            }
        }
    }
    private var viewA: some View {
        ZStack {
            Color(.blue).edgesIgnoringSafeArea(.all)
            Text("A").foregroundColor(.white)
        }
    }
    private var viewB: some View {
        ZStack {
            Color(.red).edgesIgnoringSafeArea(.all)
            Text("B").foregroundColor(.white)
        }
    }
}
```

よくあるタブ切り替えのような感じのものをPickerのSegmentedPickerStyleで＠Stateを切り替えることでビューも変わる。

![](/mol/images/2021/0224/00.gif)

普通に作ったらこんなかんじで、パッパッと切り替わる。当たり前だ。transitionを指定してないから。

どう動かしたら、ビュー遷移のメンタルモデルが自然にできあがるのだろうか。こうゆう感じの。

![](/mol/images/2021/0224/02.png)

セグメントコントロールを右にスライドしているのだから（A->B）、それに対応するビューも左から右に出てきてほしいものだ。イメージ的に。なんとなく。たぶん。その逆（A<-B）は右から出て左にいってほしいもの。イメージ的に。なんとなく。たぶん。

```swift
VStack {
    Picker
    if selection == 0 {
        viewAlpha
            .transition(
	            .asymmetric(
		            insertion: .move(edge: .trailing),
		            removal: .move(edge: .leading)
		        ))
    } else {
        viewBeta
            .transition(
	            .asymmetric(
		            insertion: .move(edge: .leading),
		            removal: .move(edge: .trailing)
		        ))
    }
}.animation(.default)
```

最初はGeometryReaderでビューの幅サイズを求めて、オフセット値をいじって画面外まで移動させればいいのかな？めんどくさいなーいやだなーと思ったけど、

trainsitionを設定するだけでよかった。そう、SwiftUIならね！

```swift
.transition(.move(edge: .leading)) 
```

普通はこんな感じでtransitionを指定すると思うのだけど、これだと一方方向にしか動かない。


```swift
.transition(
	.asymmetric(
		insertion: .move(edge: .trailing),
		removal: .move(edge: .leading)
))
```

`asymmetric`を利用することで、transitionのinsertionとremovalを個別に指定することができる。

![](/mol/images/2021/0224/01.gif)

うん、なんかそれっぽくなった🤗

