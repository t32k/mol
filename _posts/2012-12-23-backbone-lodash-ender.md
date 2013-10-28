---
layout: post
title: Backbone +  Lo-Dash + Ender?
categories:
- javascript
- performance
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '1794'
---
<strong><a href="http://www.adventar.org/calendars/15">Backbone.js Advent Calendar 2012</a></strong>
<blockquote>Backbone.jsのTIPSとかパターンとか、他のライブラリとの連携などなど。
フルスタック感がない分、各自でいろいろ編み出しながら使いこなしていると思うので、そのあたりの共有がてら書きましょう！</blockquote>
ということで、Advent Calendarでは与えられたテーマから外れた内容で記事を書くことに定評のある<a href="https://twitter.com/t32k">@t32k</a>が23日目をお贈りしてやんよ(o°3°b)b

私、恥ずかしながらBackbone.jsとは今のところ無縁な最下級HTMLコーダー(戦闘力・たったの５か・・ゴミめ・・・)でして、そんあ僕でもいつかはAPIとか使って情報とってきて面白いWebアプリケーション作りたいと思うわけです。そこでBackbone.jsなわけです。

そんなわけでわけの分からぬまま<a href="http://backbonejs.org/">Backbone.jsの公式サイト</a>を読んでみると
<blockquote>Backbone's only hard dependency is either <a href="http://underscorejs.org/">Underscore.js</a> <small>( &gt; 1.4.3)</small> or <a href="http://lodash.com/">Lo-Dash</a>. For RESTful persistence, history support via <a href="http://backbonejs.org/#Router">Backbone.Router</a> and DOM manipulation with<a href="http://backbonejs.org/#View">Backbone.View</a>, include <a href="https://github.com/douglascrockford/JSON-js">json2.js</a>, and either <a href="http://jquery.com/">jQuery</a> <small>( &gt; 1.4.2)</small> or <a href="http://zeptojs.com/">Zepto</a>.</blockquote>
とかいてあり、とりあえず、Backbone.jsを使うには、Underscore / Lo-Dashと、jQuery / Zeptoが必要みたい。Lo-Dashについては、<a href="http://havelog.ayumusato.com/develop/javascript/e531-backbone_webapp_case_intro.html">1日目の@ahomuさん</a>もちょっと触れてるね。
<pre><code class="javascript">// For Backbone's purposes, jQuery, Zepto, or Ender owns the `$` variable.
Backbone.$ = root.jQuery || root.Zepto || root.ender;</code></pre>
ソースコードの方を読んでみると、jQuery / Zepto以外にもEnderってのも使っていいらしい。なんぞこれ初耳よ！どれ使ったらいいのよ！

ということでBackboneはおいといて、この記事は形から入る男@t32kが Underscore / Lo-Dash と Zepto / Ender について調べてみるよ！
<h2>Underscore / Lo-Dash</h2>
<ul>
	<li><a href="http://underscorejs.org/">Underscore.js</a> (v1.4.3)</li>
	<li><a href="http://lodash.com/">Lo-Dash</a> (v1.0.0-rc.3)</li>
</ul>
Underscoreに関しては、Backboneと同じDocumentCloudが管理してるので、Backbone使うんならUnderscoreというように1セットのように考えている人も多いように思います。実際、@ahomuさんが使ってなかったら僕も知らなかったす。

そもそも、Lo-Dashのなぜ必要なのか、Underscoreと全く同じであるのであれば存在する必要性はないのですが、<a href="https://github.com/bestiejs/lodash">README</a>を読んでみるとUnderscoreに勝る利点がいくつか書いてあります。
<h3>consistency</h3>
<ul>
	<li>Allow iteration of objects with a <code>length</code> property [<a href="https://github.com/documentcloud/underscore/pull/799">#799</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L605-L611">test</a>]</li>
	<li>Fix cross-browser object iteration bugs [<a href="https://github.com/documentcloud/underscore/issues/60">#60</a>, <a href="https://github.com/documentcloud/underscore/issues/376">#376</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L618-L642">test</a>]</li>
	<li>Methods should work on pages with incorrectly shimmed native methods [<a href="https://github.com/documentcloud/underscore/issues/7">#7</a>, <a href="https://github.com/documentcloud/underscore/issues/742">#742</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L140-L146">test</a>]</li>
	<li><code>_.isEmpty</code> should support jQuery/MooTools DOM query collections [<a href="https://github.com/documentcloud/underscore/pull/690">#690</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L807-L812">test</a>]</li>
	<li><code>_.isObject</code> should avoid V8 bug <a href="http://code.google.com/p/v8/issues/detail?id=2291">#2291</a> [<a href="https://github.com/documentcloud/underscore/issues/605">#605</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L888-L900">test</a>]</li>
	<li><code>_.keys</code> should work with <code>arguments</code> objects cross-browser [<a href="https://github.com/documentcloud/underscore/issues/396">#396</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L982-L984">test</a>]</li>
	<li><code>_.range</code> should coerce arguments to numbers [<a href="https://github.com/documentcloud/underscore/issues/634">#634</a>, <a href="https://github.com/documentcloud/underscore/issues/683">#683</a>, <a href="https://github.com/bestiejs/lodash/blob/v1.0.0-rc.3/test/test.js#L1383-L1386">test</a>]</li>
</ul>
なんかいろいろ解決されているらしい。
<h3>customization</h3>
<ul>
	<li>lodash bacbone</li>
	<li>lodash csp</li>
	<li>lodash legacy</li>
	<li>lodash mobile</li>
	<li>lodash strict</li>
	<li>loadh underscore</li>
</ul>
<a href="https://github.com/bestiejs/lodash#custom-builds">なんかいろいろカスタムビルド</a>出来るらしい。
<h3>performance</h3>
<p style="text-align: center;"><img class="fig aligncenter" alt="" src="http://t32k.me/mol/file/2012/12/bench.png" width="600" height="386" /></p>
<a href="http://lodash.com/benchmarks">
<ul>
	<li><strong>ベンチマークテスト</strong></li>
</ul>
</a>

だいたい速いらしい(77/89でlodashが速かった。全部テストしてない)
<h4>extra features</h4>
<ul>
	<li>AMD loader support (<a href="http://requirejs.org/">RequireJS</a>, <a href="https://github.com/cujojs/curl">curl.js</a>, etc.)</li>
	<li><a href="http://lodash.com/docs#_"><code>_(…)</code></a> supports intuitive chaining</li>
	<li><a href="http://lodash.com/docs#bindKey"><code>_.bindKey</code></a> for binding <a href="http://michaux.ca/articles/lazy-function-definition-pattern"><em>“lazy”</em> defined</a> methods</li>
	<li><a href="http://lodash.com/docs#cloneDeep"><code>_.cloneDeep</code></a> for <em>“deep”</em> cloning arrays and objects</li>
	<li><a href="http://lodash.com/docs#contains"><code>_.contains</code></a> accepts a <code>fromIndex</code> argument</li>
	<li><a href="http://lodash.com/docs#forEach"><code>_.forEach</code></a> is chainable and supports exiting iteration early</li>
	<li><a href="http://lodash.com/docs#forIn"><code>_.forIn</code></a> for iterating over an object’s own and inherited properties</li>
	<li><a href="http://lodash.com/docs#forOwn"><code>_.forOwn</code></a> for iterating over an object’s own properties</li>
	<li><a href="http://lodash.com/docs#isPlainObject"><code>_.isPlainObject</code></a> checks if values are created by the <code>Object</code> constructor</li>
	<li><a href="http://lodash.com/docs#merge"><code>_.merge</code></a> for a <em>“deep”</em> <a href="http://lodash.com/docs#extend"><code>_.extend</code></a></li>
	<li><a href="http://lodash.com/docs#partial"><code>_.partial</code></a> for partial application without <code>this</code> binding</li>
	<li><a href="http://lodash.com/docs#pick"><code>_.pick</code></a> and <a href="http://lodash.com/docs#omit"><code>_.omit</code></a> accept <code>callback</code> and <code>thisArg</code> arguments</li>
	<li><a href="http://lodash.com/docs#template"><code>_.template</code></a> supports <a href="http://people.mozilla.org/~jorendorff/es6-draft.html#sec-7.8.6">ES6 template delimiters</a> and utilizes <a href="http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/#toc-sourceurl">sourceURLs</a> for easier debugging</li>
	<li><a href="http://lodash.com/docs#contains"><code>_.contains</code></a>, <a href="http://lodash.com/docs#size"><code>_.size</code></a>, <a href="http://lodash.com/docs#toArray"><code>_.toArray</code></a>, <a title="_.countBy, _.every, _.filter, _.find, _.forEach, _.groupBy, _.invoke, _.map, _.max, _.min, _.pluck, _.reduce, _.reduceRight, _.reject, _.shuffle, _.some, _.sortBy, _.where" href="http://lodash.com/docs">and more…</a> accept strings</li>
</ul>
わーい、いっぱいーヽ(=´▽`=)ﾉ

というわけ、Underscoreも改善されてくると思うけど、今んところLo-Dashを使ったほうが良さげな感じ。
<h2>Zepto / Ender</h2>
<ul>
	<li><a href="http://zeptojs.com/">Zepto.js: the aerogel-weight jQuery-compatible JavaScript library </a> (v1.0rc1)</li>
	<li><a href="http://ender.jit.su/">Ender - the no-library JavaScript library </a></li>
</ul>
だんだんめんどくさくなってきたので、
<p style="display: inline !important;"><a href="http://www.whatsmyip.org/http-compression-test/">WhatsMyIP.org | HTTP Compression Test </a>で各ファイルサイズ（Gzip後のサイズ）だけ比べてみる。</p>
■ <a href="http://zeptojs.com/zepto.min.js"><strong>http://zeptojs.com/zepto.min.js</strong></a>
<blockquote>Original Size: 23.45 KB
Compressed Size: 9.22 KB</blockquote>
■ <a href="http://cdn.enderjs.com/jeesh.min.js"><strong>http://cdn.enderjs.com/jeesh.min.js</strong></a>
<blockquote>Actual Page Size: 30.68 KB
Size if Compressed: 11.23 KB</blockquote>
■ <a href="http://code.jquery.com/jquery-1.8.3.min.js"><strong>http://code.jquery.com/jquery-1.8.3.min.js</strong></a>
<blockquote>Original Size: 91.44 KB
Compressed Size: 32.69 KB</blockquote>
Jeesh.min.jsってのはEnder.jsのスタータパックみたいなものでセレクタエンジン（<a href="https://github.com/ded/qwery">Qwery</a>）とか最小限が入ってる構成。こう見てみると、jQueryが重いのは当たり前として、EnderよりZeptoのほうが軽いんだね。

しかし、まぁ個々のメソッドの実行速度(<a href="http://jsperf.com/qwery-vs-jquery-vs-mootools-selector-engines/13)">jQuery vs Zepto.js vs Jeesh(Ender.js) selector engines · jsPerf)</a>を見てみないとなんとも言えないし、古いIEを切り捨てる<a href="http://blog.jquery.com/2012/06/28/jquery-core-version-1-9-and-beyond/">jQuery 2.0</a>がどれだけ軽くなるか気になるとこだけど、個人的にちょっとEnder.js調べてみたいかもと思ったかも ∈ ﾟ) ﾉ

--

とまぁなんやかんや調べてみましたけど、Backbone +  Lo-Dash + Enderって構成がナウいのかな。この辺りに関してはたぶん来年のFrontrend  Vol.4 powered by CyberAgentで詳しく話されるんじゃないかなと思ってる。興味持った人は参加してみてー。案内出てないけど。
