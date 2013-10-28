---
layout: post
title: マイクロフォーマット ~Webページをより便利にする最新マークアップテクニック~
categories:
- books
- markup
tags:
- microformats
status: publish
type: post
published: true
meta:
  blogger_blog: warikiru.blogspot.com
  blogger_author: t32khttp://www.blogger.com/profile/06797489791220082722noreply@blogger.com
  blogger_permalink: /2009/02/microformats.html
  _edit_last: '1'
  pvc_views: '2890'
---
HTML5と言えば、意味的な要素が追加されセマンティックな色合いが強まっていますが、まだまだ足りないですね。だって、「店名」をマークアップするときはどの要素を使えばいいの？「名前」をマークアップするときは？「地名」は？ってな具合に。

かといって、&lt;shop&gt;や&lt;name&gt;というように新しい要素がどんどん作られたらそれもそれで困りますね。そんなこんなでMicroformats(´∀｀*)ｳﾌﾌ 簡単に言えば、新しく要素なんて作らずclass属性やrel属性を使って意味的な部分を補っていこうって考えですかね。

↓詳しくはこの本を読んだら良いと思う。
<table border="0" cellpadding="5">
<tbody>
<tr>
<td valign="top"><a href="http://www.amazon.co.jp/exec/obidos/ASIN/4839925445/warikiru-22/ref=nosim/" target="_blank"><img class="fig" src="http://ecx.images-amazon.com/images/I/41vZZo0080L._SL160_.jpg" border="0" alt="マイクロフォーマット ~Webページをより便利にする最新マークアップテクニック~ (Web Designing BOOKS)" /></a></td>
<td valign="top"><span><a href="http://www.amazon.co.jp/%E3%83%9E%E3%82%A4%E3%82%AF%E3%83%AD%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88-%7EWeb%E3%83%9A%E3%83%BC%E3%82%B8%E3%82%92%E3%82%88%E3%82%8A%E4%BE%BF%E5%88%A9%E3%81%AB%E3%81%99%E3%82%8B%E6%9C%80%E6%96%B0%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%83%86%E3%82%AF%E3%83%8B%E3%83%83%E3%82%AF%7E-Web-Designing-BOOKS/dp/4839925445%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4839925445" target="_blank">マイクロフォーマット~Webページをより便利にする最新マークアップテクニック~ </a>
木達 一仁 </span>

<span>毎日コミュニケーションズ  2008-07-23
売り上げランキング : 234040
おすすめ平均  <img src="http://g-images.amazon.com/images/G/01/detail/stars-3-0.gif" alt="" /></span>

<span><a href="http://www.amazon.co.jp/%E3%83%9E%E3%82%A4%E3%82%AF%E3%83%AD%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88-%7EWeb%E3%83%9A%E3%83%BC%E3%82%B8%E3%82%92%E3%82%88%E3%82%8A%E4%BE%BF%E5%88%A9%E3%81%AB%E3%81%99%E3%82%8B%E6%9C%80%E6%96%B0%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%83%86%E3%82%AF%E3%83%8B%E3%83%83%E3%82%AF%7E-Web-Designing-BOOKS/dp/4839925445%3FSubscriptionId%3D15SMZCTB9V8NGR2TW082%26tag%3Dwarikiru-22%26linkCode%3Dxm2%26camp%3D2025%26creative%3D165953%26creativeASIN%3D4839925445" target="_blank">Amazonで詳しく見る</a></span> <span>by <a href="http://www.goodpic.com/mt/aws/index.html">G-Tools</a></span></td>
</tr>
</tbody>
</table>
んで、僕もようやく読み終えました（・ω・）
<div>

リファレンス本かなと思いきやステップアップ式のガイド本だったのが残念（一応、巻末に仕様リファレンスはある）。そのせいで、例えばhreviewの仕様について知りたかったらまずhreviewの章の部分読んで、事例研究の章を読んで、仕様リファレンス部分を読まなければならず、飛び飛びですごいめんどい。CSSのスタイル指定とかあんまり必要ないんでないかな。

とはいえ、<a href="http://microformats.org/wiki/ja">Microformats Wiki</a>を除けば、日本語でコレだけMicroformatsについて書かれてるドキュメントはこれしかないし、実際に使われているMicroformatsの事例など紹介して丁寧に解説されてあるので分かりやすかったかなと思う。

特にYahoo!の事例なんかは、中の人のMicroformatsに対する考えも聞けて面白い。
<blockquote>なぜマイクロフォーマットを採用したのかって？　何よりまず、Yahoo!ではどのスタッフもただウェブに夢中だからだ。ウェブがどんどん繁栄するのを見たいのさ。マイクロフォーマットはウェブを活気づけるのに役立ちそうだし、最終的にはユーザのためにもなるだろうと感じた。ウェブサイトでも組織でも、大規模になるほど制約が出てくることがあるのは確かだけど、裏を返せばその規模の大きさが有利になることもある。マイクロフォーマットのような例では、Yahoo!クラスの規模があれば、その技術が一定のハードルを超えて広まる可能性がある。僕らは光栄にもその役目を果たしたわけで、マイクロフォーマットをの力でウェブが一段とユーザの役に立つようになるのを楽しみにしているんだ。
<span class="Apple-style-span" style="font-size: small;"><a href="http://nate.koechley.com/blog/about/">Nate Koechley</a></span></blockquote>
<div>

いいですね、米ヤホーはオープンな感じがして、とても好きです。実際に<a href="http://developer.yahoo.com/searchmonkey/">SearchMoneky</a>ではhAtom、hCalendar、hCard、hReview、XFNをインデックスしているみたいです。また、Nate Koechleyはこんなことも言ってます↓
<blockquote>ウェブをもっと良い世界にしてくれるものなら、何でも利用した方がいいと思う。それがマイクロフォーマットほど技術的な影響が小さいものなら、使わない手はない。もちろん、状況次第で臨機応変に判断する必要があるけれど、マイクロフォーマットに対応するのは楽勝モノだと思うよ。おまけに、自分たちの努力がウェブ全体の進化にとってプラスとなるかもしれないというボーナスまで付くことになる、。<span class="Apple-style-span" style="font-size: small;">
P378 | マイクロフォーマットの利用価値</span></blockquote>
事実Microformats、最小限の工数で対応しようと思えばclass属性いじるだけでいいですからね。それによってCSSを変更しなければならないとかないし（名前かぶったらしなきゃいけないけど。。）、古い環境に影響せずにそれに対応するUAにはそれ相応の価値を提供できる。これって<a href="http://warikiru.blogspot.com/2008/12/understanding-progressive-enhancement.html">Progressive Enhancement</a>的な考え方に通じますね。素敵♪

</div>
<div>みんなもMicroformatsでDOしちゃったらいいんだよ(　´∀｀)つ</div>
</div>
