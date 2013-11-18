---
layout: post
title: grunt-initとYeoman
subtitle: 愛しさと切なさと心強さと
categories: maple
status: publish
type: post
excerpt: "YO～メーン！YO～メーン！YO～メーン！"
---
愛しの[Maple](https://github.com/t32k/maple)のScaffold（足場組み：プロジェクトに必要なコード一式を揃えてくれる）には`grunt-init`を使用していたが`yo`に変えた。これまではYeoman自体なんかゴツくてやだなと漠然と思ってたんだけど、Gruntだけでかゆいところに手が届かなくて、あれやこれや拡張しようと思ったら煩雑になってくるので、いっそのことYeamon1つで収まるのならそれもまた良いのかなと思ってきた。俺も年食ったもんだ。

+ [Project Scaffolding - Grunt: The JavaScript Task Runner](http://gruntjs.com/project-scaffolding)
+ [Yeoman - Modern workflows for modern webapps](http://yeoman.io/)

これまでの`grunt-init`を使ってMapleプロジェクトを使うとこまでの手順。

```
# プロジェクトディレクトリを作成して移動
$ mkdir maple_proj && cd maple_proj
# MapleのScaffold
$ grunt-init maple
# Gruntfileの場所に移動
$ cd src/tools
# Grunt Tasksに必要なnode_modulesをインスコ
$ npm install
# Default taskを実行
$ grunt
```

`yo`を使ってMapleプロジェクトを使うとこまでの手順。

```
$ mkdir maple_proj && cd maple_proj
$ yo maple
$ grunt
```

印象操作も甚だしいｗプロジェクトのディレクトリ構成も変更した。

要は`yo`コマンドを実行するとプロジェクトファイルのスキャフォールドをした後に、`npm install && bower install`をYeomanが自動的にしてくれるのが移行した最大の理由だYO。俺も年食ったもんだ。

`grunt-init`でも自動的に`npm install`できないこともないらしいが、めんどうそうだ。何よりもそれ実行するためのモジュールをインストールしなきゃならないので、手数自体変わらない。

Yeomanに変えた他のメリットとしては、Node.jsが必要なこと自体変わらないが、Yeoman自体にGruntと[Bower](http://bower.io/)が内包されているので、スキャフォールドを動かすまでの手数も1つ減らすことができた。

```
$ npm install -g grunt-cli
$ npm install -g grunt-init
$ git clone https://github.com/t32k/grunt-init-maple.git ~/.grunt-init/maple --recursive
```
上記でBowerに依存してたらさらに一手必要になる。

```
$ npm install -g yo
$ npm install -g generator-maple
```
うん、シンプル。ちなみに無駄にjQueryをBower管理している。generatorもnpm管理できるしいいね。

てことで、Mapleプロジェクトを動かすところまでは[Node.js](http://nodejs.org/)がインストールされている前提で、5手でイケる！

```
$ npm install -g yo
$ npm install -g generator-maple
$ mkdir maple_proj && cd maple_proj
$ yo maple
$ grunt
```

しかも、[前回の記事でCompass依存から脱却しlibSassを使っている](http://t32k.me/mol/log/good-bye-compass-good-bye-ruby/)ので、`gem install sass && gem install compass`しなくてもSassの編集ができるYO。

（Taskによっては別途インストールする必要性がある）

+ [t32k/maple](https://github.com/t32k/maple)
+ [t32k/generator-maple](https://github.com/t32k/generator-maple)

そんじゃByeByeだYO!!!!!