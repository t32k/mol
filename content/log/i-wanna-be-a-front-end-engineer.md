---
date: 2014-02-14
title: フロントエンドエンジニア（仮）
subtitle: 〜え、ちょっとフロントやること多すぎじゃない！？〜
categories: 
    - development
excerpt: "フロントエンドのワークフロー(Grunt)、最適化（パフォーマンス）について考えたことを紹介します。"
---

<iframe src="http://www.slideshare.net/slideshow/embed_code/31162704" width="427" height="356" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px 1px 0; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>

+ [Developers Summit 2014：【13-D-3】](http://event.shoeisha.jp/devsumi/20140213/session/389)
+ [フロントエンドエンジニア（仮） 〜え、ちょっとフロントやること多すぎじゃない！？〜 // SlideShare ](http://www.slideshare.net/t32k/i-wanna-bea-frontendengineer)

2年前でWebデザイナーだった私がどのようにフロントエンドエンジニアなっていったのか。デザイナーにもなれず、エンジニアにもなれないどっちつかずな職種で自分のアイデンティティを模索し、日々の膨大なタスクに追われながら、フロントエンドのワークフロー(Grunt)、最適化（パフォーマンス）について考えたことを紹介します。

『（仮）が取れた時、運命の技術者に出会える・・・』

## 自己紹介

+ [Koji Ishimoto - t32k.me](https://t32k.me/)
+ Web Performance
	+ [High Performance Web Design](http://www.slideshare.net/t32k/high-performance-web-design)
	+ [Coding Web Performance](http://www.slideshare.net/t32k/coding-web-performance)
	+ [Long Life Web Performance Optimization](http://www.slideshare.net/t32k/long-life-web-performance-optimization)
+ Web Analytics
	+ [Using Google Analytics with jQuery Mobile](http://www.slideshare.net/t32k/using-google-analytics-with-jquery-mobile)
	+ [大規模サイトにおけるGoogleアナリティクス導入から成果まで](http://www.slideshare.net/t32k/lp19-ishimoto)
+ Sass/Compass
	+ [スマートフォンWebアプリ最適化”３つの極意”](http://www.slideshare.net/t32k/web-15218538)
	+ [パフォーマンスから考えるSass/Compassの導入・運用](http://www.slideshare.net/t32k/sasscompass-20689960)
	+ [モバイル制作におけるパフォーマンス最適化について](http://www.slideshare.net/t32k/ss-15915114)
	+ [Manning: Sass and Compass in Action](http://www.manning.com/netherland/)

## フロントエンドエンジニアとは？

+ [A Baseline for Front-End Developers - Adventures in JavaScript Development](http://rmurphey.com/blog/2012/04/12/a-baseline-for-front-end-developers/)

1. JavaScript
2. Git(and a GitHub account)
2. Modularity, dependency management, and production builds
3. In-Browser Developer Tools
4. The command line
5. Client-side templating
6. CSS preprocessors
7. Testing
8. Process automation (rake/make/grunt/etc.)
10. Code quality
11. The fine manual

+ [How to keep up to date on Front-End Technologies - The Recipe](http://uptodate.frontendrescue.org/)

## ツールを管理する

### Front-end Tooling Landscape 

[![](http://i.imgur.com/043Yanf.png)](http://slid.es/passy/yeoman/fullscreen#/1/1)

+ __Boilerplate__ : HTML5 Boilerplate, Twitter Bootstrap, Backbone Boilerplate, Angular seed, Ember starter, Zurb Foundation
+ __Abstractions__ : CoffeeScript, Sass, Less, Compass, Jade, Haml, Zen coding, Markdown, Handlebars, Iced Coffee, TypeScript, Traceur
+ __Frameworks__ : Backbone, Angular, Ember, YUI, Agility, CanJS, Dojo, Meteor, Derby, Spine, Batman, Cujo, Knockout, Knockback, jQuery Mobile, jQuery UI, Closure, ExtJS, Montage
+ __Workflow__ : Chrome DevTools, LiveReload, Codekit, Brunch, WebStorm IDE, watch, Testing, Tincr, JSHint, BrowserStack, Selenium, WebGL Inpector
+ __Performance__ : JavaScript, CSS and Heap profiling, GPU, memory, tracing, PageSpeed
+ __Build__ : Grunt, Rake, Marven, Concat, r.js, Miification, Image optimization, Compression, Module loading, mod_pagespeed

__GUI Apps__

+ [Sass: Syntactically Awesome Style Sheets](http://sass-lang.com/)
+ [Scout - Compass and Sass without all the hassle](http://mhs.github.io/scout-app/)
+ [LiveReload](http://livereload.com/)
+ [CodeKit — THE Mac App For Web Developers](https://incident57.com/codekit/)

__Grunt__

+ [Grunt: The JavaScript Task Runner](http://gruntjs.com/)
+ [node.js](http://nodejs.org/)

```
$ npm install grunt-cli -g
```

__Package.json__

```
$ npm init

This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.
...
```

```
$ npm install grunt --save-dev
$ npm install grunt-csso --save-dev
```

__Gruntfile.js__

```
$ npm install grunt-init -g
$ git clone https://github.com/gruntjs/grunt-init-gruntfile.git ~/.grunt-init/gruntfile
$ grunt-init gruntfile
```

__Gruntfile.js__

```
module.exports = function(grunt) {
  // プロジェクト設定
  grunt.initConfig({
    // タスク設定
    csso: {
      files: {
        'output.css': ['input.css']
      }
    }
  });
  // タスクに必要なプラグインを読み込む
  grunt.loadNpmTasks('grunt-csso');
  // カスタムタスクを設定
  grunt.registerTask('default', ['csso']);
};
```
+ [Plugins - Grunt: The JavaScript Task Runner](http://gruntjs.com/plugins)
+ [t32k/maple](https://github.com/t32k/maple)

#### grunt-contrib-connect/watch

<iframe width="640" height="480" src="//www.youtube.com/embed/MnhmDAPjwT8?rel=0" frameborder="0" allowfullscreen></iframe>

#### grunt-sass

<iframe width="640" height="480" src="//www.youtube.com/embed/ZVXgibjJDwE?rel=0" frameborder="0" allowfullscreen></iframe>

#### grunt-contrib-csslint

<iframe width="640" height="360" src="//www.youtube.com/embed/CjCpRjAX-HE?rel=0" frameborder="0" allowfullscreen></iframe>

#### grunt-kss

<iframe width="640" height="480" src="//www.youtube.com/embed/WbZeB7hih_M?rel=0" frameborder="0" allowfullscreen></iframe>

+ [Yeoman - Modern workflows for modern webapps](http://yeoman.io/)

```
$ npm install yo -g
$ npm install generator-maple -g
$ mkdir your_proj && cd $_
$ yo maple
$ grunt
```

<iframe width="640" height="480" src="//www.youtube.com/embed/GIMmipDkU2M?rel=0" frameborder="0" allowfullscreen></iframe>


## スピードを追跡する

+ [Front-End Ops | Smashing Magazine](http://www.smashingmagazine.com/2013/06/11/front-end-ops/)

> It doesn’t matter how many features you have or how sexy your features are if they aren’t delivered to the user quickly, with ease, and then heavily monitored. ― Alex Sexton

+ [High Performance Web Sites - O'Reilly Media](http://shop.oreilly.com/product/9780596529307.do)
+ [WebPagetest - Website Performance and Optimization Test](https://www.webpagetest.org/)
+ [WebPagetest in 5 minutes — MOL](https://t32k.me/mol/log/webpagetest-5-minutes/)
+ [marcelduran/webpagetest-api](https://github.com/marcelduran/webpagetest-api)
+ [TAP Plugin - Jenkins - Jenkins Wiki](https://wiki.jenkins-ci.org/display/JENKINS/TAP+Plugin)
+ [Velocity 2013 レポート｜サイバーエージェント 公式エンジニアブログ](http://ameblo.jp/principia-ca/entry-11561132297.html)

```
$ npm install webpagetest -g
```

Thank you!
