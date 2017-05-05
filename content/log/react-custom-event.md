---
date: 2017-05-05
title: Reactコンポーネントを外から操作したい
categories: 
    - development
excerpt: 最近、Reactを触っているのだけど、Reactコンポーネント外から任意のReactコンポーネントを操作したい事情に駆られた（何を言ってるのか分からねぇと思うが俺も（ｒｙ）。
---

最近、Reactを触っているのだけど、Reactコンポーネント外から任意のReactコンポーネントを操作したい事情に駆られた（何を言ってるのか分からねぇと思うが俺も（ｒｙ）。

```javascript
export default class Hoge extends Component {
  constructor(props) {
    super(props);
    this.state = { text: '' };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick(e) {
	  this.setState({ text: 'unko' });
  }
  render() {
	  ...
  }
}
```

普通のケースだと、こんな感じで`Hoge`のコンポーネントのどっかをクリックしたら、`state`の`text`に`unko`をセットすることによって、`render`がはしるみたいな、わかりやすい。なんの問題ない。

ただ、このコンポーネントを、`window.Hoge.setState({ text: 'unko' })`みたいに、グローバルから操作したい場合ってどうしたらいいんだろうかとけっこう悩んだ。

## re-render


```javascript
export default class Hoge extends Component {
  render() {
	  return(<span id='hoge'>{ this.props.text }</span>)
  }
}
window.Hoge = Hoge;
```

とりあえず、`Hoge`をグローバルの`window`に生やす。

```javascript
export default class Fuga extends Component {
  constructor(props) {
    super(props);
    window.createHoge = (value) => {
      const Hoge = window.Hoge;
      const elm = document.getElementById('hoge');
      elm.innerHTML = '';
      ReactDOM.render(<Hoge text={value} />, elm);
    };
  }
}
```

親のコンポーネントなり、なんなりで、新規に`Hoge`を作るグローバル関数を定義する。

```javascript
window.createHoge('unko');
```

で、`Hoge`コンポーネントの`props`に`unko`渡して、上書きすることでできた。なんか無理矢理感あるけど...

既にレンダリングしてある`Hoge`コンポーネントってどうやって取得したらいいんだろうか？(
謎

## custom event

とりあえず`unko`を表示できてホッとしてたけど、今度はこの`unko`を他のコンポーネントに伝えたいって場合どうすればいいんだろうと悩んだ。

```javascript
export default class Fuga extends Component {
  constructor(props) {
    super(props);
    window.createHoge = (value) => {
     const event = new CustomEvent('createHoge', { 'detail': value });
      document.getElementById('piyo').dispatchEvent(event);
      ...
    };
  }
}
```

`createHoge`のときに、`createHoge`イベントを発火させる。んで伝えたい値もセットしておく。

```javascript
export default class Piyo extends Component {
  constructor(props) {
    super(props);
    this.state = { text: '' };
		this.handleHoge= this.handleHoge.bind(this);
  }
  componentDidMount() {
    this.refs.piyo.addEventListener('createHoge', this.handleHoge);
  }
  componentWillUnmount() {
    this.refs.piyo.removeListener('createHoge', this.handleHoge);
  }
  handleHoge(e) {
    this.setState({ text: e.detail });
  }
  render() {
	  return(<span ref='piyo' id='piyo'>{this.state.text}</span>);
  }
}
```

受け手のコンポーネント`Piyo`でリッスン♪これで、`window.createHoge('unko');`することで、`Hoge`コンポーネントが作られ上書きし、`Piyo`コンポーネントにも`unko`が表示される。

なんか[MobX](https://mobx.js.org/)みたいなストア管理のライブラリ使えば、もっとシュッとできるんだろうなと思いつつ、しかし、そこまでの規模じゃないと思い、この結果に至りました。ちーん( ˘ω˘)