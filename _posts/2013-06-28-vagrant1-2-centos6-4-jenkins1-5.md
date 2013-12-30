---
layout: post
title: VagrantでCentOSを入れてJenkinsを導入してみる
categories: development
status: publish
type: post
published: true
excerpt: "我もJenkins触ってみたかったんや..."
---
![](/static/blog/2013/06/vj.png)

我も<a href="http://jenkins-ci.org/">Jenkins</a>触ってみたかったんや...

1. Jenkinsで我もジョブ書きたい
2. とりあえずローカル環境で動かしたい
3. Macのインストーラーで一発やん！
4. でもいろいろインスコしたら危なそう
5. んじゃ、VM上でJenkins動すか &lt;-イマココ

ってことで、<a href="http://www.vagrantup.com/">Vagrant</a>使ってみることにする。

## 各種インストール

<strong><a href="https://www.virtualbox.org/wiki/Downloads">VirtualBox をインストール</a>しましょう。</strong>

最新の4.2.14でvagrant upすると"Progress object failure: NS_ERROR_CALL_FAILED"ってエラーでるので、4.2.12をインストールしませう。

<strong><a href="http://downloads.vagrantup.com/">Vagrantをインストール</a>しましょう。</strong>

以前に、gem installでvagrantをインスコした人はuninstallしておきませう。古いのがあるとうまく動きません。

vagrantで利用できるBoxファイルはここに一覧がありますんで、好きなやつ選びましょう。

+ <a href="http://www.vagrantbox.es/">A list of base boxes for Vagrant - Vagrantbox.es</a>

僕はCentOSをいれたかったので、<em>”CentOS 6.4 x86_64 Minimal (VirtualBox Guest Additions 4.2.12, Chef 11.4.4, Puppet 3.1.1)”</em>を選びました。

```
$ vagrant box add centos-6.4 http://developer.nrel.gov/downloads/vagrant-boxes/CentOS-6.4-x86_64-v20130427.box
```

これで、ローカルの~/.vagrant.d/boxes/にcentos-6.4って名前でBoxファイルが保存されます。

```
$ vagrant init
centos-6.4 A `Vagrantfile` has been placed in this directory. You are now ready to `vagrant up` your first virtual environment! Please read the comments in the Vagrantfile as well as documentation on `vagrantup.com` for more information on using Vagrant.
$ vagrant up 
Bringing machine 'default' up with 'virtualbox' provider... [default] Importing base box 'centos-6.4'... ...
```

あとは、initで初期化して、upで起動させる。

```
$ vagrant ssh
Welcome to your Vagrant-built virtual machine. 
[vagrant@localhost ~]$
```

sshでVMの中に入れます。

```
$ sudo yum install java-1.7.0-openjdk.x86_64
```

Jenkinsで必要なためcentOSにJavaをインストールします。

```
$ sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
$ sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key 
$ sudo yum install jenkins
```

<a href="http://pkg.jenkins-ci.org/redhat/">RedHat Linux RPM packages for Jenkins</a>のページ見ながら、Jenkinsをインストールします。
<pre><code class="bash">$ sudo service jenkins start</code></pre>
Jenkinsを起動させます。

<a href="http://localhost:8080/">http://localhost:8080/</a>でJenkinsのホーム画面が表示されれば成功です。

が、表示されない。

## 各種設定

```
$ sudo vi /etc/sysconfig/iptables
```

```
# 下記一行追加
-A INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT
```

8080のポートを空けます。

```
$ /etc/init.d/iptables restart
```

再起動します。

<a href="http://localhost:8080/">http://localhost:8080/</a>でJenkinsのホーム画面が表示されれば成功です。
が、表示されない。

```
# Vagrantfile

# Create a forwarded port mapping which allows access to a specific port 
# within the machine from a port on the host machine. In the example below, 
# accessing "localhost:8080" will access port 80 on the guest machine. 
config.vm.network :forwarded_port, guest: 8080, host: 8001 

# Create a private network, which allows host-only access to the machine 
# using a specific IP. 
config.vm.network :private_network, ip: "192.168.33.10"
```

Vagrantfileの設定で、<a href="http://e-words.jp/w/E3839DE383BCE38388E38395E382A9E383AFE383BCE38387E382A3E383B3E382B0.html">ポートフォワーディング</a>を設定します。
（ゲストOS上の8080への接続をホストOSの8001からアクセスするみたいな感じ？）
config.vm.network :private_networkのコメントアウトを外します(外さなくてもいいかもしんない)。

```
$ vagrant reload
```

再起動して、

<a href="http://localhost:8001/">http://localhost:8001/</a>でJenkinsのホーム画面が表示されれば成功です。

![](/static/blog/2013/06/232fb3827d5a5421172fdd16db1ad854.png)

ほらね、簡単でしょ？

## 参考

<a href="http://ja.wikipedia.org/wiki/TCP%E3%82%84UDP%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E3%83%9D%E3%83%BC%E3%83%88%E7%95%AA%E5%8F%B7%E3%81%AE%E4%B8%80%E8%A6%A7">TCPやUDPにおけるポート番号の一覧 - Wikipedia </a>
