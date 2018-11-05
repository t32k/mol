---
date: 2013-03-05
title: grunt-contribさえあればOK！
categories:
  - development
---

世の中、Grunt0.4 が出たって持ちきりでやんス。

- [Grunt 0.4.0 released - Grunt: The JavaScript Task Runner](http://gruntjs.com/blog/2013-02-18-grunt-0.4.0-released)

今までビルトインタスクだった下記はことごとく grunt-contrib-\*シリーズと呼ばれるプラグインに置き換わってしまった。

- **concat** grunt-contrib-concat plugin
- **init** stand-alone grunt-init utility
- **lint** grunt-contrib-jshint plugin
- **min** grunt-contrib-uglify plugin
- **qunit** grunt-contrib-qunit plugin
- **server** grunt-contrib-connect plugin
- **test** grunt-contrib-nodeunit plugin
- **watch** grunt-contrib-watch plugin

もし諸君が concat、lint、min といったタスクを Grunt 0.4 でも使いたい場合は、このように書いてないだろうか。

- [Upgrading from 0.3 to 0.4 - Grunt: The JavaScript Task Runner](http://gruntjs.com/upgrading-from-0.3-to-0.4)

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

contrib シリーズのタスクを利用したいのなら、全部入りの<strong><a href="https://github.com/gruntjs/grunt-contrib">grunt-contrib</a></strong>をひとつ読みこむだけで利用できる。

```
// Load the plugin
grunt.loadNpmTasks('grunt-contrib');
```

grunt-contrib なかに全部入ってるんだね。

![](/mol/file/2013/03/ss.png)

※ とはいえ grunt-contrib だとアップデートはひとまとめになるので、各 contrib の最新版を使いたいのなら個別に管理したほうがいいかも

そんだけ。
