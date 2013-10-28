---
layout: post
title: grunt-contribさえあればOK！
categories:
- javascript
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '2253'
---
世の中、Grunt0.4が出たって持ちきりでやんス。
<ul>
	<li><a href="http://gruntjs.com/blog/2013-02-18-grunt-0.4.0-released">Grunt 0.4.0 released - Grunt: The JavaScript Task Runner</a></li>
</ul>
今までビルトインタスクだった下記はことごとくgrunt-contrib-*シリーズと呼ばれるプラグインに置き換わってしまった。
<ul>
	<li><strong>concat</strong> → grunt-contrib-concat plugin</li>
	<li><strong>init</strong> → stand-alone grunt-init utility</li>
	<li><strong>lint</strong> → grunt-contrib-jshint plugin</li>
	<li><strong>min</strong> → grunt-contrib-uglify plugin</li>
	<li><strong>qunit</strong> → grunt-contrib-qunit plugin</li>
	<li><strong>server</strong> → grunt-contrib-connect plugin</li>
	<li><strong>test</strong> → grunt-contrib-nodeunit plugin</li>
	<li><strong>watch</strong> → grunt-contrib-watch plugin</li>
</ul>
<div><a href="https://github.com/gruntjs/grunt/wiki/Upgrading-from-0.3-to-0.4">Upgrading from 0.3 to 0.4 · gruntjs/grunt Wiki </a></div>
もし諸君がconcat、lint、minといったタスクをGrunt 0.4でも使いたい場合は、このように書いてないだろうか。
<pre><code class="javascript">module.exports = function(grunt) {

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

};</code></pre>
contribシリーズのタスクを利用したいのなら、全部入りの<strong><a href="https://github.com/gruntjs/grunt-contrib">grunt-contrib</a></strong>をひとつ読みこむだけで利用できる。

<pre><code class="javascript">  // Load the plugin
  grunt.loadNpmTasks('grunt-contrib');</code></pre>

grunt-contribなかに全部入ってるんだね。

<img src="http://t32k.me/mol/file/2013/03/ss.png" alt="" title="contrib" width="614" height="451" class="size-full wp-image-4753 fig" />

※とはいえgrunt-contribだとアップデートはひとまとめになるので、各contribの最新版を使いたいのなら個別に管理したほうがいいかも

そんだけ。

