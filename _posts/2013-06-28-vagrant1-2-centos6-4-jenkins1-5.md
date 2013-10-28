---
layout: post
title: VagrantでCentOSを入れてJenkinsを導入してみる
categories:
- development
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '1954'
---
<a href="http://t32k.me/mol/file/2013/06/vj.png"><img src="http://t32k.me/mol/file/2013/06/vj.png" alt="" title="vj" width="900" height="100" class="aligncenter size-full wp-image-4945" /></a>

我も<a href="http://jenkins-ci.org/">Jenkins</a>触ってみたかったんや...
<ol>
	<li>Jenkinsで我もジョブ書きたい</li>
	<li>とりあえずローカル環境で動かしたい</li>
	<li>Macのインストーラーで一発やん！</li>
	<li>でもいろいろインスコしたら危なそう</li>
	<li>んじゃ、VM上でJenkins動すか &lt;-イマココ</li>
</ol>
ってことで、<a href="http://www.vagrantup.com/">Vagrant</a>使ってみることにする。<span style="font-size: 13px; line-height: 19px;"> </span>

<h2>各種インストール</h2>

<strong><a href="https://www.virtualbox.org/wiki/Downloads">VirtualBox をインストール</a>しましょう。</strong>

最新の4.2.14でvagrant upすると"Progress object failure: NS_ERROR_CALL_FAILED"ってエラーでるので、4.2.12をインストールしませう。

<strong><a href="http://downloads.vagrantup.com/">Vagrantをインストール</a>しましょう。</strong>

以前に、gem installでvagrantをインスコした人はuninstallしておきませう。古いのがあるとうまく動きません。

vagrantで利用できるBoxファイルはここに一覧がありますんで、好きなやつ選びましょう。
<ul>
	<li><a href="http://www.vagrantbox.es/">A list of base boxes for Vagrant - Vagrantbox.es</a></li>
</ul>
僕はCentOSをいれたかったので、<em>”CentOS 6.4 x86_64 Minimal (VirtualBox Guest Additions 4.2.12, Chef 11.4.4, Puppet 3.1.1)”</em>を選びました。
<pre><code class="bash">$ vagrant box add centos-6.4 http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130427.box</code></pre>
これで、ローカルの~/.vagrant.d/boxes/にcentos-6.4って名前でBoxファイルが保存されます。
<pre><code class="bash">$ vagrant init 
centos-6.4 A `Vagrantfile` has been placed in this directory. You are now ready to `vagrant up` your first virtual environment! Please read the comments in the Vagrantfile as well as documentation on `vagrantup.com` for more information on using Vagrant. 

$ vagrant up 
Bringing machine 'default' up with 'virtualbox' provider... [default] Importing base box 'centos-6.4'... ...</code></pre>
あとは、initで初期化して、upで起動させる。
<pre><code class="bash">$ vagrant ssh 
Welcome to your Vagrant-built virtual machine. 
[vagrant@localhost ~]$</code></pre>
sshでVMの中に入れます。
<pre><code class="bash">$ sudo yum install java-1.7.0-openjdk.x86_64</code></pre>
Jenkinsで必要なためcentOSにJavaをインストールします。
<pre><code class="bash">$ sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo 
$ sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key 
$ sudo yum install jenkins </code></pre>
<a href="http://pkg.jenkins-ci.org/redhat/">RedHat Linux RPM packages for Jenkins</a>のページ見ながら、Jenkinsをインストールします。
<pre><code class="bash">$ sudo service jenkins start</code></pre>
Jenkinsを起動させます。

<a href="http://localhost:8080/">http://localhost:8080/</a>でJenkinsのホーム画面が表示されれば成功です。

が、表示されない。

<h2>各種設定</h2>

<pre><code class="bash">$ sudo vi /etc/sysconfig/iptables</code></pre>
<pre><code># 下記一行追加
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT</code></pre>
8080のポートを空けます。
<pre><code class="bash">$ /etc/init.d/iptables restart</code></pre>
再起動します。

<a href="http://localhost:8080/">http://localhost:8080/</a>でJenkinsのホーム画面が表示されれば成功です。
が、表示されない。

<pre><code class="ruby"># Vagrantfile 

# Create a forwarded port mapping which allows access to a specific port 
# within the machine from a port on the host machine. In the example below, 
# accessing "localhost:8080" will access port 80 on the guest machine. 
config.vm.network :forwarded_port, guest: 8080, host: 8001 

# Create a private network, which allows host-only access to the machine 
# using a specific IP. 
config.vm.network :private_network, ip: "192.168.33.10" </code></pre>
Vagrantfileの設定で、<a href="http://e-words.jp/w/E3839DE383BCE38388E38395E382A9E383AFE383BCE38387E382A3E383B3E382B0.html">ポートフォワーディング</a>を設定します。
（ゲストOS上の8080への接続をホストOSの8001からアクセスするみたいな感じ？）
config.vm.network :private_networkのコメントアウトを外します(外さなくてもいいかもしんない)。
<pre><code class="bash">$ vagrant reload</code></pre>
再起動して、
<a href="http://localhost:8001/">http://localhost:8001/</a>でJenkinsのホーム画面が表示されれば成功です。
<a href="http://t32k.me/mol/file/2013/06/232fb3827d5a5421172fdd16db1ad854.png"><img src="http://t32k.me/mol/file/2013/06/232fb3827d5a5421172fdd16db1ad854.png" alt="" title="スクリーンショット 2013-06-29 2.29.46" width="900"  class="aligncenter size-full wp-image-4955" /></a>
ほらね、簡単でしょ？

<h2>参考</h2>
<a href="http://ja.wikipedia.org/wiki/TCP%E3%82%84UDP%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%83%9D%E3%83%BC%E3%83%88%E7%95%AA%E5%8F%B7%E3%81%AE%E4%B8%80%E8%A6%A7">TCPやUDPにおけるポート番号の一覧 - Wikipedia </a>
