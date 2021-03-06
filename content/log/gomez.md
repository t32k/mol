---
date: 2009-03-24
title: Webサイトパフォーマンス管理と客観的評価手法セミナー
categories: 
    - report
---

3月12日に開かれた<a href="http://www.gomez.co.jp/company/press/090205.html">Webサイトパフォーマンス管理と客観的評価手法セミナー</a>に行ってきたー
<h2 id="section01">1.サイトパフォーマンスの重要性</h2>
<h3>（ゴメスが定義する）サイトパフォーマンスとは？</h3>
<strong>サイトパフォーマンス</strong> = <strong>表示速度</strong> + <strong>稼働率</strong>
<ul>
  <li><strong>表示速度</strong> = ユーザーがWebページにアクセスしてから、完全にページが表示されるまでの時間</li>
  <li><strong>稼働率</strong> = ページ稼働率（エラーになっていない率) + オブジェクト稼働率（エラーになっていない率）</li>
</ul>
安定性と信頼感の一つの評価基準にサイトパフォーマンスが存在
<h3>サイト表示速度が企業経営に与える影響</h3>
<ul>
  <li>アマゾンはページの反応が<strong>0.1秒遅く</strong>なると、売り上げが「<strong>1%ダウン</strong>」する</li>
  <li>グーグルのページ反応が<strong>0.5秒遅く</strong>なると、アクセス数が「<strong>20%ダウン</strong>」する</li>
  <li>一般的に表示スピードが<strong>1秒遅く</strong>なると、PVは<strong>11%</strong>、コンバージョンは<strong>7%</strong>、顧客満足度は<strong>16%ダウン</strong>する
<div style="text-align: right;"><a href="http://www.gomez.com/download/aberdeen-gomez-best-in-class.pdf"><small>Aberdeen Group Report</small></a></div></li>
</ul>
<h3>ヨドバシドットコムとアリコのパフォーマンスダメージ</h3>
前者はCMS導入によるパフォーマンス劣化、後者はAIGの経営破綻危機が懸念されサイトにユーザーが殺到。
（ヨドバシは20~50秒の表示速度が3日間続いた）
<h3>ユーザーがサイトを重いと感じる時間</h3>
Yahoo!のアンケート調査によれば、<strong>67.8％の人が5秒がライン！</strong>
<img src="http://lh5.ggpht.com/_1drnogi3vdg/ScjlY50NBuI/AAAAAAAAAUM/T3tVR3osl24/yahoo.png" alt=""/>
<div style="text-align: right;"><small><a href="http://polls.dailynews.yahoo.co.jp/quiz/quizresults.php?wv=1&amp;poll_id=849&amp;typeFlag=1">Yahoo!ニュース - 意識調査 - ページ表示、何秒で「重い」と感じる？</a>
実施期間：2007年6月13日 ~ 2007年6月26日</small></div>
<h3>Webサイトの反応時間の3つの重要限界</h3>
<ul>
  <li>心理的・感情的な違和感を感じないのは<strong>0.1秒</strong>まで</li>
  <li>思考の流れが妨げられないのは<strong>1秒</strong>まで</li>
  <li>注意力を維持する限界の時間は<strong>10秒</strong>まで</li>
</ul>
<div style="text-align: right;"><small><a href="http://www.useit.com/papers/responsetime.html">ヤコブ・ニールセン博士　反応時間 - ３つの重要限界</a></small></div>
<strong>
以上から一般的なサイトは5秒が最低ライン、1秒を目標ラインとすべし！</strong>
<h2 id="section02">2.事例：業界別パフォーマンス状況</h2>
<strong>証券各社のパフォーマンス状況</strong>
1秒を争う証券取引の世界では、パフォーマンスの向上は非常に大事。
1位のカブドッドコム証券はテキスト中心のシンプルなページ構成を実現

<strong>銀行各社のパフォーマンス状況</strong>
全体的に速い表示速度を記録。
14位のイーバンク銀行はパーツ数の多さが原因で遅くなっている

<strong>不動産仲介各社のパフォーマンス状況</strong>
業界全体としては良好なパフォーマンス状況

<strong>ニュースサイト各社のパフォーマンス状況</strong>
業界全体としてはパフォーマンスは良くない
トップページに動的なパーツが多いのも一因

<strong>ヤフー対Google対goo</strong>
google.co.jpが0.171秒と最速。yahoo.co.jpは0.978秒、gooは0.524秒
<span style="font-size: 85%;">（データセンター拠点からの測定。家庭PCからの測定の場合、High Broadbandで3.165秒）</span>
<h2 id="section03">3.パフォーマンス管理9つの道</h2>
<ol class="order">
  <li>あらゆる関係部署を巻き込む</li>
  <li>パフォーマンス評価手法を共有する</li>
  <li>ベースラインを設定する</li>
  <li>ユーザーを知る</li>
  <li>機能設計基準以外にも注目する</li>
  <li>実際のパフォーマンスを測定する</li>
  <li>サードパーティのパフォーマンスを測定する</li>
  <li>パフォーマンス検証を継続する</li>
  <li>パフォーマンス重視文化を仕組み化する</li>
</ol>
<h3>あらゆる関係部署を巻き込む</h3>
<ul>
  <li><strong>経営層</strong>
サイトパフォーマンスの劣化が収益に及ぼす悪影響はいくらか？</li>
  <li><strong>現場マネージャー</strong>
サイト改修や新機能導入がパフォーマンスに影響を及ぼさないか？</li>
  <li><strong>デザイナー</strong>
リッチコンテンツやグラフィックで表示速度が遅くならないか？</li>
  <li><strong>アプリケーション開発部門</strong>
コード手法ひとつでパフォーマンスに影響を与えないか？</li>
  <li><strong>品質管理部門</strong>
自分のデスクトップからではなく正確なユーザーエクスペリエンスはどのようなものか？</li>
  <li><strong>オペレータ部門</strong>
ユーザーに一番近い立場にいる部門はパフォーマンスの影響状況をWebチームに迅速にフィードバックをする</li>
</ul>
<h3>パフォーマンス評価手法を共有する</h3>
<ul>
  <li><strong>Availability：可用性</strong> サイトがダウンしていない割合
<span style="font-size: 85%;">稼働率が99%だと1年間の動作不能時間は3日15時間36分に及ぶ
経産省のSaaS産業向けのガイドラインでは稼働率を99.9％を保証するように通達</span></li>
  <li><strong>Responsiveness：反応性</strong> サイトの表示速度</li>
  <li><strong>Consitency：一貫性</strong> 時間・地域等によらず一貫して安定していること</li>
  <li><strong>User satisfaction：顧客満足度</strong></li>
</ul>
<h3>ベースラインを設定する</h3>
多くの企業はサイトを監視しているがパフォーマンスのベースラインを設定しない
<ul>
  <li>競合他社と比較する</li>
  <li>パフォーマンス推移を知る</li>
</ul>
<h3>ユーザーを知る</h3>
<ul>
  <li>最も重要なターゲット顧客を知る</li>
  <li>ターゲットの行動特性を知る</li>
  <li>各ターゲットに最適化されたサイトを構築する</li>
</ul>
<h3>機能設計基準以外にも注目する</h3>
<ul>
  <li>スタンダードでないOS・ブラウザにも対応する</li>
  <li>iPhone等のスマートフォンにも対応する</li>
  <li>世界各国からのアクセス（海外出張ビジネスマン・旅行者・海外居住者）に対応する
<span style="font-size: 85%;">（日本からみれば1秒前後のyahoo.co.jpもアメリカから見れば11-12秒、イギリスから見れば18秒）</span></li>
  <li>アプリケーション開発の王道は「最初はきちんと立ち上げること、次にそれを改善すること」</li>
  <li>ページサイズを管理する。特にページビュー上位10ページ</li>
  <li>IE6,7とFirefoxでのダウンロード速度の違い</li>
  <li>WindowsとMacでのダウンロード速度の違い</li>
</ul>
<h3>実際のパフォーマンスを測定する</h3>
定期的かつ継続的かつ同手法にてパフォーマンス測定を行う
<ul>
  <li>ISP拠点からのレスポンス計測</li>
  <li>リアルユーザー（家庭PC）からのレスポンス計測</li>
</ul>
<h3>サードパーティのパフォーマンスを測定する</h3>
自社の努力によらないパフォーマンスへの影響を考慮する
<h3>パフォーマンス検証を継続する</h3>
<ul>
  <li>日々のサイト更新の中でパフォーマンスに影響を与えることもある</li>
  <li>競合他社の状況を常に監視しておく</li>
  <li>パフォーマンスエラーが検知できるような体制をつくっておく</li>
</ul>
<h3>パフォーマンス重視文化を仕組み化する</h3>
<ul>
  <li>目標値を業績評価基準に組み込む</li>
  <li>客観的・継続的で明確なパフォーマンス測定ツールの導入</li>
</ul>
<h2 id="section04">4.どうしたらパフォーマンスが向上するのか？</h2>
<h3>Yahoo!Exceptional Performanceの14のルール</h3>
<ol class="order">
  <li>Make fewer HTTP requests</li>
  <li>Use a CDN</li>
  <li>Add an Expires header</li>
  <li>Gzip components</li>
  <li>Put CSS at the top</li>
  <li>Move JS to the bottom</li>
  <li>Avoid CSS expressions</li>
  <li>Make JS and CSS external</li>
  <li>Reduce DNS lookups</li>
  <li>Minify JS</li>
  <li>Avoid redirects</li>
  <li>Remove duplicate scripts</li>
  <li>Turn off ETags</li>
  <li>Make AJAX cacheable and small</li>
</ol>
<h3>ゴメスが薦めるパフォーマンス改善ポイント</h3>
<strong>1ページ・1テーマ・1スクリーンの原則</strong>を貫く

技術側面では、特に以下の4つが重要
<ul>
  <li>パーツ数を減らす</li>
  <li>JavaScript・CSS内の不要な記述を削除する</li>
  <li>CSSを適度に分割する</li>
  <li>サードパーティのコンテンツが悪影響を及ぼしていないかチェックする</li>
</ul>
ゴメス・コンサルティング株式会社に関して
<ul>
  <li><a href="http://web-tan.forum.impressrd.jp/e/2009/02/06/4793">Webサイトのパフォーマンスを可視化！ / Gomez, Inc. | Web担当者Forum</a></li>
</ul>
