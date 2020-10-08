---
date: 2020-10-08
title: SwiftUIでのスタイルのまとめかたとか
excerpt: SwiftUIだとスタイルはViewに繋げられたモディファイアであり、これがダラダラと記述されているのは、見通しが悪い。
ogimage: https://t32k.me/mol/images/2020/1008/02.png
categories: 
    - swiftui
---

CSSだとスタイルはクラスでまとめられ、BEMなり、なんなりのクラスの命名規則で管理する。SwiftUIだとスタイルはViewに繋げられたモディファイアであり、これがダラダラと記述されているのは、見通しが悪い。

![](/mol/images/2020/1008/00.png)

```Swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .font(.largeTitle)
            .foregroundColor(Color(.systemRed))
            .padding()
            .frame(maxWidth: .infinity, alignment: .leading)
    }
}
```

# カスタムモディファイア

modifier というまんまのものがある。上記のコードは LargeText という ViewModifier 定義すると、.modifier(LargeText(color: Color(.systemRed))) だけを View に繋げれば良い。また引数を持つことができるので、色の部分を抜き出して、青色のテキストを表示したり、緑色のテキストを表示できるといった具合だ。

![](/mol/images/2020/1008/01.png)

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
            .modifier(LargeText(color: Color(.systemRed)))
    }
}
struct LargeText: ViewModifier {
    let color: Color
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .foregroundColor(color)
            .padding()
            .frame(maxWidth: .infinity, alignment: .leading)
    }
}
```

# カスタムスタイル

modifier と似ているが、特定のコンポーネントにはカスタムスタイルを定義する方法が提供されている。

```swift
struct ContentView: View {
    var body: some View {
        Button("ボタン") { print("タップ") }
            .buttonStyle(MyButtonStyle())
    }
}
struct MyButtonStyle: ButtonStyle {
    func makeBody(configuration: Self.Configuration) -> some View {
        configuration.label
            .padding()
            .foregroundColor(Color(.systemBlue))
            .overlay(
                RoundedRectangle(cornerRadius: 8)
                    .stroke(Color(.systemBlue), lineWidth: 1)
            )
    }
}
```

Button の場合は ButtonStyle がある。一見すると別に modifier でも問題じゃないかと思うが、ミソは`configuration`の部分だ。 configuration.isPressedで、押されているのか、いないのかの状態がわかるので、ボタン押下時のスタイルも定義することができる。同様に、トグルにも ToggleStyle というものが提供されており、configuration.isOn でトグルの on/off 状態がわかるので、on/off でスタイルを変更することができる。ということで、ButtonやToggleのスタイルをまとめたいときはカスタムスタイルでまとめる。

# 構造体でまとめる

![](/mol/images/2020/1008/02.png)

```swift
struct ContentView: View {
    var body: some View {
        List {
            HStack {
                Image(systemName: "person.crop.circle.fill")
                    .resizable()
                    .frame(width: 24, height: 24)
                    .padding()
                VStack(alignment: .leading) {
                    Text("Hoge Yamada").font(.callout).fontWeight(.bold)
                    Text("Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.").lineLimit(2).font(.caption)
                }
            }
            HStack {
                Image(systemName: "person.crop.circle.fill")
                    .resizable()
                    .frame(width: 24, height: 24)
                    .padding()
                VStack(alignment: .leading) {
                    Text("Fuga Yamada").font(.callout).fontWeight(.bold)
                    Text("Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.").lineLimit(2).font(.caption)
                }
            }
            HStack {
                Image(systemName: "person.crop.circle.fill")
                    .resizable()
                    .frame(width: 24, height: 24)
                    .padding()
                VStack(alignment: .leading) {
                    Text("Piyo Yamada").font(.callout).fontWeight(.bold)
                    Text("Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.").lineLimit(2).font(.caption)
                }
            }
        }
    }
}
```

受信メール一覧的なリストを作る場合、HStack でプロフ画像と文書を並べてとか一つ一つのリストアイテムを作っていく。まぁ愚直に書けば、上記みたいな感じ。

```swift
struct ContentView: View {
    let friends = [ "Hoge Yamada", "Fuga Yamada", "Piyo Yamada" ]
    
    var body: some View {
        List {
            ForEach(friends, id: \.self) { friend in
                ListItem(name: friend)
            }
        }
    }
    
    struct ListItem: View {
        let name: String
        
        var body: some View {
            HStack {
                Image(systemName: "person.crop.circle.fill")
                    .resizable()
                    .frame(width: 24, height: 24)
                    .padding()
                VStack(alignment: .leading) {
                    Text(name).font(.callout).fontWeight(.bold)
                    Text("Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.").lineLimit(2).font(.caption)
                }
            }
        }
    }
}
```

HStack らへんを ListItem 構造体としてまとめるとこんな感じ。スタイルをまとめるというよりかは、ボタンなり、画像なりある程度の粒度をもったUIコンポーネントとしてまとめるといったことに近い。

今作っているのは簡素な見た目のモックアプリなので、そこまでモディファイアをつなげるてスタイルを作り込んでいくことがないので、modifier はあんまり使わず、構造体でまとめて終わりって感じになっている。

<div class="__media"><a href="https://www.amazon.co.jp/dp/4815604061/?tag=warikiru-22" target="_blank" rel="noopener">
<img src="https://images-na.ssl-images-amazon.com/images/I/416ZqsPCCjL._SX393_BO1,204,203,200_.jpg" alt="" class="__media__image">
<div class="__media__body">
    <div>SwiftUI 徹底入門</div>
    <div class="__media__text">金田 浩明</div>
    <div>Amazon.co.jpで詳細を見る</div>
</div>
</a></div>