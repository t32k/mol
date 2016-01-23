---
date: 2009-05-29
title: pageTracker._initData関数も廃止予定
subtitle: _initData() _initData()Deprecated. 
categories: 
    - analytics
excerpt: 数ヶ月前のGoogle Analyticsコードアップデートでスニペットにtry,catch文が挿入されたってことを書いた。でも、よくよく見たらpageTracker._initDataの関数もなくなっていない？ってことに気づいた。
---


数ヶ月前のGoogle Analyticsコードアップデートでスニペットに`try/catch`文が挿入されたってことを書いた。でも、よくよく見たらpageTracker._initDataの関数もなくなっていない？ってことに気づいた。

```javascript
var pageTracker = _gat._getTracker("UA-xxxxxxx-x"); 
pageTracker._initData();
pageTracker._trackPageview();
```

少し前のga.jsのコードはこんな感じだったともう。

```javascript
try {
    var pageTracker = _gat._getTracker("UA-xxxxxxx-x");
    pageTracker._trackPageview();
} catch (err) { }
```

`initData()`ってゆうくらいだから初期化する関数なのかと思いGoogle Analyticsトラッキング コード移行ガイドで初期化部分探したけど、載ってない。

Analytics Tracking APIに載っていた。

> _initData() _initData()Deprecated. initData() now executes automatically in the ga.js tracking code. Initializes or re-initializes the GATC (Google Analytics Tracker Code) object. 

Deprecatedってことは廃止予定ってことか。なんかga.js内で自動的に実行しているらしい。 あーすっきり！しかしまぁ、もうちょっとアナウンスしてくれてもいいんだと思うんだけどな...