---
date: 2013-07-03
title: nvmでnode.jsを管理する
subtitle:
categories: 
    - development
excerpt:
ogimage:
---

こんちわ！@t32kだ！

私はしがないHTMLコーダーですが、そんな私でも最近はgruntなどのnode.js環境を必要とするツールなど使っています。ということで、node.jsをインストールしなきゃあかんのですよ。

## Mac OS X Installer (.pkg)

幸い、私のような最下級サイヤ戦士でも簡単にnode.jsをインストールできるように公式サイトではインストーラーが用意されています。やったね、たえちゃん！ということで、人生になんの疑問もなく私はこれを使ってました。

+ [Node.js](https://nodejs.org/)

しかし、node.jsの進化は凄まじいものがありまして、月単位？週単位？で新しいバージョンがアップデートされていたなんてのはザラです。プラス、私は出来る限り（stableで）最新のバージョンにしておきたいという性格なので、node.jsのバージョンが新しく出るたびに、公式サイト行って、インストーラーDLして、インストール画面をクリック！クリック！クリック！なんて作業はもうやなんだよ！

![](http://t32k.me/static/blog/2013/07/537090ed538f9d4ad7649e9ba5cb040b.png)

ということで、インストーラーによる管理は辞めたい！

思い立ったら吉日DAY！インストーラーでインストールしたnode.jsをアンインストールしましょう。インストーラがあるのならアンインストーラあるのかなと思ったらなかった／(^o^)＼けど、スクリプトあったよ。

+ [Mac OS X uninstall script for packaged install of node.js](https://gist.github.com/nicerobot/2697848)

```shell
$ curl -ksO https://gist.github.com/nicerobot/2697848/raw/uninstall-node.sh
$ chmod +x ./uninstall-node.sh
$ ./uninstall-node.sh
$ rm uninstall-node.sh
```

上から順番に実行してくだけだよ。


## Homebrew

以前からbrew doctorをするとnodeがlinkしてねーよ！と注意されていたのだが、インストーラでインストールしたnode.jsが優先されていたのだろうと思う。ってことで、今はアンインストールしたから大丈夫ってことで、Homebrewでnode.jsを管理してみる。

```shell
$ brew install node
```

入ったー！簡単！

あれ、npm使えなくね？とおもったら、`npm install -g`したnpmは以下に、`/usr/local/share/npm/bin`保存されるらしい。

```shell
#npm
export PATH="/usr/local/share/npm/bin:$PATH"
```

ということで、bash_profileとかにpathを通しておく。

+ [Homebrewでnode.jsとnpmをインストール | bulblub](http://bulblub.com/2013/04/20/install_nodejs_with_homebrew/)

これで、完璧だね、やったね、たえちゃん！

> @t32k nvmかnodebrewかnaveのどれか絶対使った方がいいです！

と思ったら、同僚のエンジニアさんから親切なツイートが！

## nvm

+ [creationix/nvm](https://github.com/creationix/nvm)
+ [isaacs/nave](https://github.com/isaacs/nave)
+ [hokaccha/nodebrew](https://github.com/hokaccha/nodebrew)

Node.jsのバージョン管理には上記のようなものあるらしいけど、どれ使ったらいいんだろう... Rubyはrvm使ってるし、名前似てるし、nvm使ってみる！

```shell
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
```

でインストール！

```shell
source ~/.nvm/nvm.sh
```

を、bash_profileとかに書いておく。

```shell
$ nvm install 0.10
```

で、0.10.x系の最新がインストールされる。

```shell
$ nvm alias default 0.10
```

で、デフォルトで使用されるnode.js のバージョンが0.10.x系の最新になる。ほらね、簡単でしょ？