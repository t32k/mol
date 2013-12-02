---
layout: post
title: grunt-contribさえあればOK！
categories:javascript
status: publish
type: post
published: true
---
世の中、Grunt0.4が出たって持ちきりでやんス。

+ <a href="http://gruntjs.com/blog/2013-02-18-grunt-0.4.0-released">Grunt 0.4.0 released - Grunt: The JavaScript Task Runner</a>

今までビルトインタスクだった下記はことごとくgrunt-contrib-*シリーズと呼ばれるプラグインに置き換わってしまった。

+ __concat__ → grunt-contrib-concat plugin
+ __init__ → stand-alone grunt-init utility
+ __lint__ → grunt-contrib-jshint plugin
+ __min__ → grunt-contrib-uglify plugin
+ __qunit__ → grunt-contrib-qunit plugin
+ __server__ → grunt-contrib-connect plugin
+ __test__ → grunt-contrib-nodeunit plugin
+ __watch__ → grunt-contrib-watch plugin

<a href="https://github.com/gruntjs/grunt/wiki/Upgrading-from-0.3-to-0.4">Upgrading from 0.3 to 0.4 · gruntjs/grunt Wiki </a>

もし諸君がconcat、lint、minといったタスクをGrunt 0.4でも使いたい場合は、このように書いてないだろうか。

```
module.exports = function(grunt) {
  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    uglify: { .... },
    min: { .... },
    concat: { .... },
    lint: { .... },
    }
  });
  // Load the plugins
  grunt.loadNpmTasks('grunt-contrib-uglify');
  grunt.loadNpmTasks('grunt-contrib-min');
  grunt.loadNpmTasks('grunt-contrib-concat');
  grunt.loadNpmTasks('grunt-contrib-lint');
  // Default task.
  grunt.registerTask('default', ['uglify']);
};
```

contribシリーズのタスクを利用したいのなら、全部入りの<strong><a href="https://github.com/gruntjs/grunt-contrib">grunt-contrib</a></strong>をひとつ読みこむだけで利用できる。

```
// Load the plugin
grunt.loadNpmTasks('grunt-contrib');
```

grunt-contribなかに全部入ってるんだね。

<img src="http://t32k.me/mol/file/2013/03/ss.png" alt="" title="contrib" width="614" height="451" class="size-full wp-image-4753 fig" />

※ とはいえgrunt-contribだとアップデートはひとまとめになるので、各contribの最新版を使いたいのなら個別に管理したほうがいいかも

そんだけ。
