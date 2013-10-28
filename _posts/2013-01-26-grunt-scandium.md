---
layout: post
title: 'Titanium もくもく会 Tokyo #5でLTしました'
categories:
- javascript
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '838'
---
<script async class="speakerdeck-embed" data-id="5e65f51048bc01306b0e22000a1e9845" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>
<ul>
	<li><a href="http://atnd.org/events/34307"><strong>Titanium もくもく会 #5 2013 : ATND </strong></a></li>
</ul>
表題どおり、昨日喋ってきました。Titanium Studioを使わない、普段使い慣れている環境でTitaniumを触りたかったので、僕からはSublime Text2とGruntの開発環境について少し話しました。
<h2>Code Completion</h2>
<ul>
	<li><a href="http://unbounded.io/post/28394170197/titanium-mobile-develpoment-with-sublime-text-2-and"><strong>Titanium Mobile Develpoment with Sublime Text 2 and Intellij IDEA | UNBOUNDED.IO </strong></a></li>
</ul>

ここに書いてあるとおりだと、SublimeCodeIntelインストールして、 jsca2jsから対象のバージョンのJSファイルをダウンロードしてCodeIntelにパスを指定してあげればいいって書いてあるんだけど、動いてなかった＞ｍ＜だれか教えて下さい。
<pre><code>// your home directory( ~/.codeintel/config
{
 "JavaScript": {
  "javascriptExtraPaths":["add_your_path_here"]
  }
}</code></pre>
<h2>Build Command</h2>
<ul>
	<li><strong><a href="http://docs.appcelerator.com/titanium/latest/#!/guide/Titanium_Command-Line_Interface_Reference ">Titanium Command-Line Interface Reference - Titanium 3.0 - Appcelerator Docs</a></strong></li>
</ul>

<pre><code>brew install node
npm install -g titanium
npm install -g grunt-cli
cd /your_porject_path
npm install grunt@0.4.0rc7
npm install grunt-scandium</code></pre>

Command-Line Interface が正式にリリースされたということで、これならGruntから動かせるということで<a href=" https://github.com/t32k/grunt-scandium">grunt-scandium</a>というのプラグイン作りました。npm install grunt-scandiumでインストールできるお。単に、GruntからTitanium CLIを叩いてるだけですが、かなりの数のBuild Optionを考えると細かいBuild設定などGruntfileでできるのでその点で便利かなと思っています。
<pre><code>// Example Settings
scandium: {
    ios: {
        platform : 'ios',
        project_dir : '/path/to/your_project',
        force: true,
        build_only: false,
        options: {
            device_family: 'iphone',
            sim_version: '6.0'
        }
    },
    android: {
        platform : 'android',
        project_dir : '/path/to/your_project',
        options: {
            android_sdk: '/path/to/android-sdk',
            target: 'emulator',
            avd_skin: 'HVGA'
        }
    }
}</code></pre>

grunt-titaniumにしなかったのは畏れ多かったからです(・ω&lt;)

あと、AndroidはSDKのtargetが見当たらないぜって言われるんだけど、だれか教えて下さい。
CODESTRONG!
