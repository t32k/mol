---
date: 2013-07-03
title: nvmでnode.jsを管理する
categories: development
---

こんちわ！<a href="https://twitter.com/t32k">@t32k</a>だ！

私はしがないHTMLコーダーですが、そんな私でも最近はgruntなどのnode.js環境を必要とするツールなど使っています。ということで、node.jsをインストールしなきゃあかんのですよ。
<h2>Mac OS X Installer (.pkg)</h2>
幸い、私のような最下級サイヤ戦士でも簡単にnode.jsをインストールできるように公式サイトではインストーラーが用意されています。やったね、たえちゃん！ということで、人生になんの疑問もなく私はこれを使ってました。
<ul>
	<li><a href="http://nodejs.org/"><strong>node.js</strong></a></li>
</ul>
しかし、node.jsの進化は凄まじいものがありまして、月単位？週単位？で新しいバージョンがアップデートされていたなんてのはザラです。プラス、私は出来る限り（stableで）最新のバージョンにしておきたいという性格なので、node.jsのバージョンが新しく出るたびに、公式サイト行って、インストーラーDLして、インストール画面をクリック！クリック！クリック！なんて作業はもうやなんだよ！

<a href="/static/blog/2013/07/537090ed538f9d4ad7649e9ba5cb040b.png"><img class="aligncenter size-full wp-image-4988" title="node.js" src="/static/blog/2013/07/537090ed538f9d4ad7649e9ba5cb040b.png" alt="" width="734" height="576" /></a>

ということで、インストーラーによる管理は辞めたい！

思い立ったら吉日DAY！インストーラーでインストールしたnode.jsをアンインストールしましょう。インストーラがあるのならアンインストーラあるのかなと思ったらなかった／(^o^)＼けど、スクリプトあったよ。
<ul>
	<li><a href="https://gist.github.com/nicerobot/2697848"><strong>Mac OS X uninstall script for packaged install of node.js </strong></a></li>
</ul>
<pre><code class="bash">$ curl -ksO https://gist.github.com/nicerobot/2697848/raw/uninstall-node.sh
$ chmod +x ./uninstall-node.sh 
$ ./uninstall-node.sh 
$ rm uninstall-node.sh</code></pre>
上から順番に実行してくだけだよ。
<h2>Homebrew</h2>
以前からbrew doctorをするとnodeがlinkしてねーよ！と注意されていたのだが、インストーラでインストールしたnode.jsが優先されていたのだろうと思う。ってことで、今はアンインストールしたから大丈夫ってことで、Homebrewでnode.jsを管理してみる。

<pre><code class="bash">$ brew install node</code></pre>

入ったー！簡単！

あれ、npm使えなくね？とおもったら、npm install -g したnpmは以下に、/usr/local/share/npm/bin 保存されるらしい。

<pre><code class="bash"># npm
export PATH="/usr/local/share/npm/bin:$PATH"</code></pre>

ということで、bash_profileとかにpathを通しておく。

<ul>
	<li><strong><a href="http://bulblub.com/2013/04/20/install_nodejs_with_homebrew/">Homebrewでnode.jsとnpmをインストール | bulblub </a></strong></li>
</ul>

これで、完璧だね、やったね、たえちゃん！

<blockquote class="twitter-tweet"><a href="https://twitter.com/t32k">@t32k</a> nvmかnodebrewかnaveのどれか絶対使った方がいいです！

— CO2クリエイター79 (@79yuuki) <a href="https://twitter.com/79yuuki/statuses/352104822507442179">July 2, 2013</a></blockquote>
と思ったら、同僚のエンジニアさんから親切なツイートが！
<h2>nvm</h2>
<ul>
	<li><a href="https://github.com/creationix/nvm">nvm</a></li>
	<li><a href="https://github.com/isaacs/nave">nave</a></li>
	<li><a href="https://github.com/hokaccha/nodebrew">nodebrew</a></li>
</ul>
Node.jsのバージョン管理には上記のようなものあるらしいけど、どれ使ったらいいんだろう。。

Rubyはrvm使ってるし、名前似てるし、nvm使ってみる！
<pre><code class="bash">$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh</code></pre>
でインストール！

<pre><code class="bash">source ~/.nvm/nvm.sh</code></pre>
を、bash_profileとかに書いておく。

<pre><code class="bash">$ nvm install 0.10</code></pre>
で、0.10.x系の最新がインストールされる。

<pre><code class="bash">$ nvm alias default 0.10</code></pre>
で、デフォルトで使用されるnode.js のバージョンが0.10.x系の最新になる。

ほらね、簡単でしょ？
