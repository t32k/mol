---
date: 2012-02-22
title: 【翻訳】サイトカタリストとGoogle アナリティクスの比較
subtitle: Omniture SiteCatalyst vs. Google Analytics
categories: translation
excerpt: Omniture SiteCatalyst vs. Google Analytics - An Objective Comparison
---

<cite class="citation">
Original：[Omniture SiteCatalyst vs. Google Analytics](http://www.slideshare.net/Semetis/omniture-sitecatalyst-vs-google-analytics-an-objective-comparison-7814945)（<time>2011-05-03</time>）by [Semetis](http://stevesouders.com/)
</cite>

<div class="fluid">
<iframe src="//www.slideshare.net/slideshow/embed_code/7814945" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe> <div style="margin-bottom:5px"> <strong> <a href="//www.slideshare.net/Semetis/omniture-sitecatalyst-vs-google-analytics-an-objective-comparison-7814945" title="Omniture SiteCatalyst vs. Google Analytics - An Objective Comparison" target="_blank">Omniture SiteCatalyst vs. Google Analytics - An Objective Comparison</a> </strong> from <strong><a href="//www.slideshare.net/Semetis" target="_blank">Semetis</a></strong> </div></div>

## Implementation

__SiteCatalyst (´・ω・｀) BAD__

 + 複雑な実装（evars, props...）
 + カスタマイズの必要性
 + 要：テクニカルスーパーバイザー
 + メンテナンスのために要：ITサポート

 → かなり複雑（実装&メンテナンス）  
 → セットアップに週/月単位でかかる  
 → 非常に高価なソリューション￥￥￥  

__Google Analytics (・∀・) GOOD!__
 
+ すべてのページに（ユニークな）1つのタグを入れるだけ
+ オプション実装が可能
	+ カスタム変数
	+ イベントトラッキング
	+ 仮想ページビュー
	+ Eコマース, ...

 → 基本的な実装は簡単（1日もかからない）  
 → 高度な実装に関してはそれなりに複雑  
 → 無料であり、すべての人が使える

## Input

### Input: Traffic filtering

__SiteCatalyst (´・ω・｀) BAD__

 + フィルタリングオプションに制限がある
 + いくつかのフィルタは追加のコスト発生
 + フィルタはプロファイルではなくレポート毎に設定する必要がある

__Google Analytics (・∀・) GOOD!__

 + あらかじめ定義したカスタムフィルタをプロファイルレベルで適用可能
 + 簡単な設定
 + 例：IP除外、サイトの一部分だけ含める、特定の地域だけ含めるなど...

### Input: Tracking – Traffic sources/Campaigns

__SiteCatalyst (´・ω・｀) BAD__

 + トラッキングコードはすべてのリンクに設定しなければならない
 + その時、トラッキングコードをSiteCatalystレポート上で確認するために分類用のファイルを送信しなければならない（SAINT 分類） 追加のステップとしてキャンペーントラッキングも同様
 +  AdWordsの費用データはトラッキングコードに統合されていない
 + Google AdWordsとの統合はこれまた追加のコストでAdobe SearchCenterというのが存在

__Google Analytics (・∀・) GOOD!__

 + 費用データも含めてGoogle Adowordsとの完全なる統合（無料）
 + その他のリンク（バナーやメルマガ...）もまた、キャンペーン名やソース、メディアを含んだurmパラメータで手動でトラッキングすべき
 + フィルタを使用することでレポート上でリネームや複数のキャンペーン/流入元をまとめることが可能

### Input: Tracking – Goals/Events/Custom Variables

__SiteCatalyst (・∀・) GOOD!__

 + 複数の変数をトラッキング可能、いくつかの計算指標ではブレイクダウンでレポート可能
 + カスタムイベント、コンバージョン、トラフィック（要：カスタマイズ実装）をトラッキング可能
 + CVファネルレポートはSCレポートインターフェース上からセットアップ可能（イベント指標に関して。計算指標はできない）
 + ファネルレポートは事前に設定する必要はなく遡って評価可能

__Google Analytics (´・ω・｀) BAD__

 + ゴール設定は特に実装の手間はない（URLベースのため）
 + ファネルパスとビジュアリゼーションレポートの設定は追加のコード実装無しで簡単にセットアップ可能
 + ファネルレポートは過去に遡れない
 + Eコマーストラッキングは追加のタグ実装が必要
 + カスタム変数（最大で5つ）とイベントトラッキングは異なるセグメントやインタラクションタイプをトラッキング可能
 + イベントをゴールとして設定できる（新GA）


## Interpretation

### Interpretation: Metrics

__SiteCatalyst (・∀・) GOOD!__

 + 指標の計算が可能。これらの指標はSC上で事前に定義された重要指標（例：直帰率、離脱率、ページビュー/訪問数、訪問者あたりの訪問数、ランディングページ、イベントコンバージョンレート,...）とは別の重要指標として定義が可能
 + データウェアハウス全ての生データを蓄積可能、カスタム・複雑なレポートも実行可能(72時間はかかる)
 + クリックスルー、インスタンスはデフォルトの指標として使用される

__Google Analytics (´・ω・｀) BAD__

 + 指標を計算することができない
 + しかし、最も重要な指標に関してはGAで事前に定義されておりすべての（カスタム）レポートで閲覧可能
 + 訪問は最も使用されるデフォルト指標


### Interpretation: Dashboards

__SiteCatalyst (・∀・) GOOD!__

 + いちから作成可能
 + ダッシュボードは全てのレポートを取り込むことが可能
 + フィルタとセグメント設定も保持可能
 + 複数のフォーマットで共有可能

__Google Analytics (・∀・) GOOD!__

 + 最大でプロファイルごとに20ダッシュボードまで作成可能
 + ユーザーフレンドリーで簡単にカスタマイズ可能
 + ダッシュボードレポートにもフィルタが適用されるようになった
 + 新GAでは一瞬で他のユーザーへ複製が可能
 + 複数のフォーマットで共有可能

### Interpretation: On-site performance reporting

__SiteCatalyst (・∀・) GOOD!__

 + 柔軟なカスタムレポートで訪問者の行動を分析可能
 + ページレベルの遷移、累積的なパスレポート
 + 内部キャンペーンのためのトラッキングコード追加可能（分類ファイルは不要）

__Google Analytics (´・ω・｀) BAD__

+ 指定したページの前後しか分析できない
+ ページ内（例：ヘッダー、メニュー...）のインタラクションはイベントトラッキングで評価可能


## Other Differentiating Specificities

__SiteCatalyst__

 + カスタマイズ性が高い（ユーザー行動、ネガティブ分析, ... ）
 + サードパーティや外部システムとの統合（SAINT classification）
 + "Data Sources"経由でデータのインポートが可能（インポート後は削除できない）
 + ページ遷移:ページレベルの遷移と累積的なパスレポート（GAは前後しか見れない）
 + カスタマーサポート
 + 計算指標
 + 複数サイトで同様のレポートが比較可能

__Google Analytics__

 + 生データの利用性、フィルタオプションの拡張性によって複数のプロファイルを作成可能
 + 簡単なCVファネルレポート vs. SCのフォールアウトレポートとイベントコンバージョンファネル
 + 追加のタグ実装なしでのGoogle AdWordsとの統合
 + 簡単に使える！しかも理解しやすい！
 + 共有設定が簡単（但しサブセットデータのみ）
 + 新・ベータバージョンの機能


## Conclusions

 + もし、ある解析ツールから他のツールへ変更するならば、これまでに貯めたデータはあきらめなければならない
 + 新たな機能は移行コストに見合うものですか？またこれからも投資し続けますか（SiteCatalyst）？
 + 決定は見積もり次第です
   + 実装コストは？
   + 新たなデータの解釈の必要性は？
   + 導入するためのリソースと時間は？
   + サードパーティのデータとの連携によるポテンシャルは？（統合の必要性）
   + 自社の要件とSLAの条件は？

***

というわけで、2011年5月のスライドということでちょいちょい古い部分もありますが、なんとなく理解。これにGoogleアナリティクスPremiumとかも入ってくると話は変わってくるだろうなと。
