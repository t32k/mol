---
layout: post
title: Google アナリティクスでiOSのバージョンを確認する方法
categories:
- analytics
tags:
- google analytics
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  pvc_views: '7888'
---
先日、同僚さんからGoogle アナリティクスでiOSのバージョン（5か4か）が確認できませんでした＞＜って報告を受けました。あれそうだっけかなと思って、【ユーザー】&gt;【ユーザーの環境】&gt;【ブラウザとOS】&gt;【オペレーティングシステム】とiPhoneをクリックしてドリルダウンしたら(not set)としか表示されてませんでした。

iOS4をいつまでサポートするのかシェアを見ながら判断したいところですので、この状況はよろしくないです、ってことでGAで 確認する方法を考えてみた。
<pre>var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-xxxxxxx-x']);
(function () {
    var ua = navigator.userAgent,
        isIOS = /iP(?:hone|ad|od)/.test(ua);
    if (isIOS) {
        var device = ua.match(/iPhone|iPad|iPod/),
            version = ua.match(/OS\s([\d_]+)/);
        version = version &amp;&amp; version[1].replace(/_/g, '.');
        _gaq.push(['_setCustomVar', 5, String(device), String(version), 2]);
    }
})();
_gaq.push(['_trackPageview']);

(function () {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();</pre>
<ul>
	<li><a href=" https://gist.github.com/2041381">How to get the iOS Version with Google Analytics. — Gist</a></li>
</ul>
上記のコードを_trackPageview メソッドの前で呼び出してあげればOKです。

_setCustomVarの後の番号はどのカスタム変数のスロットを使うかってことなので、ご自身の空いてるとこ（1 - 5）の数値にしてください。UAにiPhone|iPad|iPodの文字列がなければなんにもしません。無害な子です。

で、データが貯まると、【ユーザー】&gt;【ユーザーの分布】&gt;【カスタム変数】&gt;【カスタム変数（キー 5）】のレポートでデバイス（iPhone/iPad/iPod）＞バージョンの構造でレポートされます。iOSでOpera miniを使ってるとUA自体にOSのバージョン情報がないのでnull としてレポートされます。Firefox MobileはOKだった。
<p style="text-align: center;"><a href="/static/blog/2012/03/cv_key.png"><img class="aligncenter  wp-image-3973" title="カスタム変数　キー" src="/static/blog/2012/03/cv_key.png" alt="" width="500" height="245" /></a></p>
<p style="text-align: center;">*カスタム変数（キー5）:デバイス</p>
<p style="text-align: center;"><a href="/static/blog/2012/03/cv_value.png"><img class="aligncenter  wp-image-3972" title="カスタム変数　値" src="/static/blog/2012/03/cv_value.png" alt="" width="500" /></a></p>
<p style="text-align: center;">*カスタム変数（値5）:バージョン</p>
&nbsp;

iPhone/iPad/iPodブチヌキでバージョンシェアを見たい方は、<a href="https://www.google.com/analytics/web/permalink?type=custom_report&amp;uid=jJn51A65S9iFV9IL7T_SJA">こんな風にカスタムレポート</a>を作ればOKです。カスタム変数の値（設定したスロット番号）をディメンションに指標並べるだけ。

軽く試してみたけど、自己責任でお願いします。なんかおかしいことあったら教えてください。

※ ユーザー定義値にバージョン情報を記録して、フィルタでOSバージョン（not set）を置換する方法も考えたけどめんどくさいのでカスタム変数で取ることにした。確認できたら消せばいいし。後腐れもなし。

Special Thanks pocotan001++
