---
date: 2021-04-27
title: 【翻訳】私ってデザインエンジニアかも...
subtitle: On Design Engineering
excerpt: この記事はデザインエンジニアリングについてのシリーズの一部です。Web開発者の役割の変化やデザインとエンジニアリングの違いについて議論していきたいと思います。
ogimage: https://t32k.me/mol/images/2021/0427/0.jpg
categories: 
    - translation
---

<cite class="citation">
![Trys Mudford](/mol/images/people/trys_mudford.jpg)
Original：[I think I might be a design engineer...](https://www.trysmudford.com/blog/i-think-im-a-design-engineer/)（<time>2021-02-17</time>）by [Trys Mudford](https://twitter.com/trysmudford)
</cite>

この記事はデザインエンジニアリングについてのシリーズの一部です。Web開発者の役割の変化やデザインとエンジニアリングの違いについて議論していきたいと思います。長くなりそうだったので、この記事を補足するために [Prototyping](https://www.trysmudford.com/blog/prototyping/)、[Systemised design foundations](https://www.trysmudford.com/blog/design-foundations/)と[The designer & developer relationship](https://www.trysmudford.com/blog/designer-and-developer-relationship/)に記事を分けました。それでは始めましょう。

---

数年前から、自分がWeb開発のどの領域に当てはまるのか考えてきました。自分のキャリアを振り返れば、ある種の仕事に収束しているのを感じていましたが、それが何という名前なのか、今までは分かりませんでした。

## Web開発者はWebサイトを構築するのか？

「Web開発者」として最初の数年間、実際のところ、その役割はWebサイトを構築することを意味しなかったのです。Webサイトをコピーして更新したり、ファイルをFTPでアップロードしたり、お茶を入れたり、何か問題が起きたときにサーバー管理者に連絡したりしていました。

しだいに責任ある仕事を任されるようになり、実際にWebサイトを構築するようになりました。しかし、それだけではなく、インフラの管理、メールテンプレートの作成、企画の立案、マーケティングキャンペーンの手伝いなども行っていました。それはただWebサイトを構築するだけではありません。

とあるスタートアップに入社したことで、2人の新しいデザイナーと、プロダクトのヘッドレスAPIを開発するバックエンド・エンジニアリング・チームと初めて出会いました。フロントエンドチームは、「フロント」と「バックオブフロントエンド」の両方を担当しました。[ボタンを作り、それをつなぎ込んでいく](https://bradfrost.com/blog/post/front-of-the-front-end-and-back-of-the-front-end-web-development/)。今でもWebサイトを開発していますが、エンジニアリングチームとの共同作業です。

[Clearleft](https://clearleft.com/)のようなデザイン力の高い会社の一員になったことで、デザイナーとエンジニアのより良いコラボレーションの方法に目を向けるようになったり、デザインプロセス全体をより深く理解するようになりました。すべてのプロジェクトとは言いませんが、「フロント・オブ・フロントエンド」に注力するようになり、実際のWebサイトを完成するために「バック・オブ・フロントエンド」をエンジニアリング・チームに引き継ぐようになっています。


## デザインの意図を理解しリリースする

これはWeb開発者の仕事の中でも非常に大きな部分を占めています。しかも、ビジュアルデザインだけではなく、リサーチ、UX、プロダクト、コンテンツ、それまでのプロセス全体が対象となります。プロジェクトに参加する前の良いアイデアをすべて取り入れ、それらをエレガントにまとめ上げ、ユーザーに適切に提供するにはどうすればよいでしょうか。

あなたが「Webサイトを構築する」Web開発者であるならば、それはあなたの責任です。しかし、もしあなたが開発工程の末端ではないとしたらどうでしょう？もしあなたが自分のコードをエンジニアに渡せるとしたら...


## WebのためのWeb開発者

大規模な代理店やほとんどのプロダクトチームには、「エンジニアリング」チームがあり、それは2つの領域に分かれています。

- バックエンド
- バック・オブ・フロントエンド

一般論ですが、これらの分野の開発者は「システムを考える人」であり、プログラミング > デザインという考え方で物事に取り組む傾向があります。私の経験では、彼らの脳はそのように働く傾向があるのです。彼らのスキルは、エレガントで堅牢、かつスケーラブルなコードを書くことで、何か問題が起きたときにプロダクトが破綻しないようにすることです。彼らのスキルは、プロダクト全体を合理的なチャンクに分解し、データを効率的に保存して、簡単にクエリを投げるようににすることです。また、データの漏洩を防ぎ、ユーザーが不正なデータを保存するのを阻止し、ハッカーの攻撃を阻止することにあります。

彼らのスキルは（繰り返しますが、あくまで一般論です）、デザインのニュアンスを理解することではありません。誤解しないでください、それは素晴らしいことです。このようなチームで働く機会を持っているなら、自分が得意なことに集中して、本当のプロに専門分野を任せることができるのは、とても良いことです。このチームでは、（これまで説明してきた）Web開発者は、より大きな開発工程の一部です。彼らは**Webサイトを構築**するというよりも**Webのために構築している**のです。

## デザイン→エンジニアリングの溝

しかし、最近では「デザイン」から「エンジニアリング」へと直進し、フロント・オブ・フロントエンドを完全に見落としている組織が増えています、結局、デザインの次の段階がコードなのだから、エンジニアにUIを作らせればいいのではないか。ちょっと待って下さい、この2つの機能の間にある巨大な溝に飛び込むことは、素晴らしいデザインの意図を失う可能性があります。

[Natalya Shelburne](https://twitter.com/natalyathree)氏の[Beyond Tellerrandでの講演](https://beyondtellerrand.com/events/berlin-2019/speakers/natalya-shelburne)から引用したスライドが、このギャップを説明するのにうってつけなので、私は大好きです。

![](/mol/images/2021/0427/0.jpg)

> ソフトウェアエンジニアの帽子をかぶってデザイナーと仕事をしていると、まるで、ただの丸を渡されて、美しいフクロウを作らなければならないような気分になります。彼らはコードや品質、私がアーキテクチャでやらなければならないことを理解も評価もせず、Webサイトの写真を見てばかり、私が自分がヒーローのように感じます。

![](/mol/images/2021/0427/1.jpg)

> 一方で、私がデザイナーとしてプロジェクトに参加しているとき、どのデザインでも細部まで完璧に仕上げたフクロウを誰かに渡すと、彼らはdivを渡してきます。ごめん、それはただの丸です。

上記の引用と画像は、Natalyaのトークから抜粋したものです。[スクリプト](https://beyondtellerrand.com/events/berlin-2019/speakers/natalya-shelburne)・[講演](https://vimeo.com/373397621)には一見の価値があります。

どちらの領域でも、期待が満たされないことに失望することがあります。しかし、このように2つの役割が異なる考え方を持っている場合、効率的に引き継ぎを成功させるためにはどうすればよいのでしょうか？

## 私たちのアプローチ

- [Design foundations](https://www.trysmudford.com/blog/design-foundations/)\
デザインやコーディングの段階に入る前に、私たちはプロジェクトを管理するための基本的な指示や計算、つまり**タイポグラフィ、スペース、カラー、グリッド**を作成します。
- [Prototyping](https://www.trysmudford.com/blog/prototyping/)\
デザインが表示される場所は最終的にはブラウザなので、デザインを早く実際のデバイスで動かすことができれば、仮定をより早く検証することができます。

## デザインの翻訳

大規模な開発工程の中でWeb開発者としての私たちの目標は可能な限り最善の方法でデザインを「翻訳」することだと思います。経験上、スクラップからシステムを構築するよりも、開発とデザインの両方がシステムを使って構築されていれば、それはかなり簡単なことです。だからこそ私たちは、デザイン段階からコーディング入り、連携して一緒に意思決定するようにしています。つまり、フロントエンドのコードはデザインの延長線上にあります。

あるいは、Jamesがこう言っています：

> プロダクトのコードバージョンの忠実性は、デザインの後ではなく、デザイン段階で構築されます。開発者は、デザイナーのマイクが床に落ちる前にキャッチするのを待つのではなく、デザインチームに組み込まれます。 ― James Gilyead

## この役割はなんですか？

このような方法はとても効果的であり、私の興味を非常にかき立てました。私は、[迅速なビルド](https://www.trysmudford.com/blog/rapid-building/)、システム設計、エレガントでスケーラブルなコードを書くことが好きです。

しかし、もはや**Webサイトを構築している**とは思えませんし、**Webのための構築している**とも思えないこともあります。たとえファンデーションがプロダクトに組み込まれたとしても、プロトタイプは、ほとんどが捨てられてしまいます。デザインをエンジニアリングに翻訳するためや、プロジェクトの前提条件を検証するという目的を果たした後、消えてしまうのです。ある意味で、これは**エンジニアのためのビルド**です。

このささいな気持ちからこの役割には名前があるのではないかと考えました。そしたらあったのです。

## ✨ デザインエンジニアリング ✨

[デザインエンジニアリング・ハンドブック](https://www.designbetter.co/design-engineering-handbook/)を読んでいて、第1章の最後にある段落が私の心を捉えました。

> デザインエンジニアリングとは、デザインとエンジニアリングの重複部分を精査し、納品やアイデアの検証を迅速に行うための分野の名称です。プロトタイピングからプロダクションレディなコードの作成まで、デザイン決定を迅速に行い、リスクを軽減し、UIコードの品質を確立する職能です。デザインエンジニアの仕事は、プロダクト開発とイノベーションを最適化するために、デザイナーとエンジニアが最も効果的にコラボレーションできるようなシステム、ワークフロー、テクノロジーを包括しています。 ― Natalya Shelburne

### それ、私

この段落は、私が気づかないうちに押し進めようとしていた役割を完全に言い当てています。

- アイデア検証
- ラピッドプロトタイピング
- プロダクションコード
- UIコードの品質
- 便利なツールの作成
- システムのカプセル化
- プロジェクトの土台作り
- 効果的なコラボレーション

イエス！これは非常にエキサイティングな発見でした。

## デザインエンジニアの居場所

デザインエンジニアは、先に述べた2つの分野の間の溝に位置し、2つの分野をスムーズに翻訳する方法を見つけ出します。

> 片方で、デザイナーはピクセルパーフェクトなモックアップと美しいインターフェイスを目指します。もう片方でエンジニアはシステムの設計やパターンの最適化に努めます。その中間には、この2つのアプローチがどのように交わるかを考えるデザイナーとエンジニアがいます。 ― Adekunle Oduye | [デザインエンジニアリング・ハンドブック](https://www.designbetter.co/design-engineering-handbook/)

## デザインエンジニアが書くもの

CSSは、デザインエンジニアの主要言語です。

> CSSはプログラミングデザインのために作られたもの。デザイナーとエンジニアの両方に役立つツールであるがゆえに、このような議論がなされることが多いのです。異なるメンタルモデルを持つ人たちが一緒に仕事をしなければならない交差点では、声が大きくなりがちで、時には敵対的になることもありますが、そこにこそ学びがあるのです。 ― Natalya Shelburne | [デザインエンジニアリング・ハンドブック](https://www.designbetter.co/design-engineering-handbook/)


どのようにコードを書こうとも、最終的にはHTML、CSS、JSに集約されます。デザインエンジニアは、ユーザーエクスペリエンスとデベロッパーエクスペリエンスのバランスを取る必要があります。チームが自分たちに合った方法で優れたコードを書けるようにすると同時に、ユーザーエクスペリエンスに悪影響を与えないようにしなければなりません。

そのためには、通常は選択しないような技術を学び、使用することもありますが、それがチームに最高の製品を生み出す力を与えることは間違いありません。

言葉もツールのひとつです。

- デザインとエンジニアリングが直面する課題を**議論する**
- デザインエンジニアが提案するソリューションを**説明する**
- [ファンデーション](https://www.trysmudford.com/blog/design-foundations/)、[プロトタイプ](https://www.trysmudford.com/blog/prototyping/)、システムを**ドキュメント化する**

本質的には、デザインエンジニアの目標は**役に立つこと**です。UXが適切な判断を下すのを助け、リサーチがテストから最も有用なインサイトを得るのを助け、デザイナーが健全で実現可能なアイデアを生み出すのを助け、エンジニアがデザインの意図を理解するのを助ける。しかし、最も重要なのは、エンジニアリングチームのためにデザインを翻訳するためにできることをすることです。

私たちは「クリエイター」と「メンテナー」という言葉を使います。それは、仕事をする人と、うまく維持する人です。しかし、私はこれはスペクトルだと考えています。デザインエンジニアは、クリエイター陣営の中でも最も「創造的」な部分に位置しており、素早く開発し、素早く失敗し、他のクリエイターが後に続くことができるように、悪いアイデアの道を切り開きます。

## まとめ

そうですね、私は実際のところデザインエンジニアかもしれません。今までやってきたことを大きく変えるわけではありません。私がこれまでに手がけてきた[ファンデーション](https://www.trysmudford.com/blog/design-foundations/)、[プロトタイプ](https://www.trysmudford.com/blog/prototyping/)、デザインシステムはすべてこの職能に該当します。 そして、そこにいるのが昔の私ではないということに、とても安心感を覚えています。もっとこのコミュニティを掘り下げていきたいと思っています。

さて、ここで最後の質問ですが...

### すべてのプロジェクトでデザインエンジニアが必要でしょうか？

あえて言えば、プロジェクトをまとめるエンジニアリングの職能があれば、イエスと言えるでしょう。さらに、私はすべてのプロジェクトのデザインプロセスに開発者が関わるべきだと確信しています。開発をウォーターフォールの下流に置くのは簡単なことですが、デザイン＆エンジニアリングの「フクロウの嘆き」からもわかるように、デザイン・エンジニアリングの関与が早ければ早いほど、プロセスはスムーズに進みます。

---

- [【翻訳】デザインエンジニアリング \- MOL](/mol/log/design-engineering/)

2015年にも同様な話題についての記事を訳したが、最近、フロントエンドエンジニアの職域が広がりすぎていているのを感じている。自分はWebデザイナー上がりのフロントエンドエンジニアなので、やっぱりUIを作り込みたいという気持ちがあるし、その領域で自分のスキルが発揮できると思っている。フロント・オブ・フロントエンドとバック・オブ・フロントエンドを分けるの良いと思う一方で、小さなスタートアップでそこまでフロントエンドにリソースを割くことも難しいと思うので、まぁ適材適所で頑張りましょうとしか言えない。とりあえず、もう少しこのデザインエンジニアリングというものを今後探っていきたいと思う。