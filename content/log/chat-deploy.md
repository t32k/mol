---
date: 2018-02-14
title: チャットデプロイしたい2018
subtitle: 
categories: 
    - development
excerpt: タイトルの通り、チャットデプロイしたい。
---

タイトルの通り、チャットデプロイしたい。

- 開発環境 `master`ブランチ
- QA環境 `deployment/qa`ブランチ
- 本番環境 `deployment/production` ブランチ

自分のところは、上記みたいに環境とブランチがマッチングしていて、そのブランチにコミットなりマージするとCircleCIのほうでデプロイしてくれる。

例えば、開発環境でおおかた確認してQA環境に反映したいときは`master`から`deployment/qa`にPRを作成しマージして、デプロイしてた。それめんどいので、そこをボットでやらせたいと思った。要はこうゆう感じ。

1. slack上から任意の言葉でbotにデプロイを指示する
2. slackのbotがGitHub APIでプルリクエスト作成・マージを実行する
3. CircleCIがGAEにデプロイする

[3.はもう出来てる](/mol/log/circleci2-yml-nodejs/)ので、1.2.を見てみよう。

## 1. Slack Bot

SlackのBotってどうやって作るんだっけなー、Hubotってあったよなーと思いつつ、今はBotkitが安定して開発されているっぽいからそれを使う。

- [Botkit: Building Blocks for Building Bots](https://botkit.ai/)

![](/mol/images/2018/0214-00.png)

Custom Integrations > Botsからボットを登録して、API Tokenを取得しておく。


- [botkit/slack\_bot\.js at master · howdyai/botkit](https://github.com/howdyai/botkit/blob/master/examples/slack_bot.js)

あとは、レポジトリのexamplesディレクトリのなかにあるslack_bot.jsに先程のトークンを渡して起動させればおｋ。


```
controller.hears(['hello'], 'direct_mention', (bot, message) => {
    bot.reply(message, 'Hello!');
    // ここからGitHubのAPIを叩く
});
```

`controller.hears`でなんか受け取って、それで反応してあげれば良いのが分かる。

## 2. GitHub Apps

まぁGitHubでゴニョゴニョしたいので、GitHub API v3を叩く。

- [GitHub API v3 \| GitHub Developer Guide](https://developer.github.com/v3/)

Node.jsのAPIクライアントはoctokitがよさそうってことで使ったのだが、Authenticationがむずい、ドハマリした。

- [octokit/rest\.js: GitHub REST API client for Node\.js](https://github.com/octokit/rest.js)

まず、いろいろ認証の仕方が多い。どれを選べばいいんだ！一番簡単なのはPersonal access tokensだったけど、これだと僕のアカウントでプルリクエストが作成され、マージされてしまう。やはりBotとして実行してもらいたいので、だめ。

- [GitHubと連携する新しいアプリの形：GitHub Appsの作り方 \- Qiita](https://qiita.com/icoxfog417/items/fe411b94b8e7ae229e3e)

これを読む限り、GitHub Appsがいちばんオサレそうなので、この方法でやってみる。
GitHub Appsとして認証するためには、まず[JSON Web Token](https://jwt.io/introduction/)を作らないといけないらしい。

- [Authentication options for GitHub Apps \| GitHub Developer Guide](https://developer.github.com/apps/building-github-apps/authentication-options-for-github-apps/#authenticating-as-a-github-app)

GitHubのドキュメント見ると、Rubyコードの例が書いてあるけど、Node.jsでやるにはどーしたらいいんだー！と悩んだあげく、こんな感じに書いた。

```
const fs = require("fs");
const jwt = require("jsonwebtoken");
const key = fs.readFileSync(`${__dirname}/private-key.pem`);
const opts = { algorithm: "RS256" };
const payload = {
  iat: Math.floor(Date.now() / 1000) - 30,
  exp: Math.floor(Date.now() / 1000) + 60 * 10,
  iss: YOUR_ISSUE_NUMBER
};
const jwtToken = jwt.sign(payload, key, opts);
```

まずはGitHubのWebからGitHubAppsを登録する。パーミッションの設定も忘れなく。

- [GitHub App Permissions \| GitHub Developer Guide](https://developer.github.com/v3/apps/permissions/)

![](/mol/images/2018/0214-01.png)

んでprivate-key.pemを生成しとく。それと、アプリの発行IDもその設定画面にあるのでメモっとく。あとは、`jsonwebtoken`というnpmを使って、トークンを生成する。

```
const octokit = require("@octokit/rest")({
  headers: {
    accept: "application/vnd.github.machine-man-preview+json",
    authorization: `Bearer ${jwtToken}`
  }
});
const installationToken = await octokit.apps.createInstallationToken({
  installation_id: YOUR_INSTALLATION_ID
});
```

![](/mol/images/2018/0214-02.png)

んで、octokitを初期化するときに、`headers`に先程のJWTトークンをBearerのあとにひっつける。`installation_id`がなんぞやってことだけど、Appの設定のAdvancedでなんかアクセスがあるっぽいので、そこから知る。


```
octokit.authenticate({
  type: "integration",
  token: installationToken
});
```

んで、この`installationToken`を`octokit.authenticate`に渡してようやくAPIが叩けるようになる。PR作成したかったら`octokit.pullRequests.create(opts)`とか叩けばよい。すごく長かった。。。

## Google Compute Engine

![](/mol/images/2018/0214-03.png)

あとは、Botのメッセージを`attachments`を使うとボットっぽくてよい。成功失敗とかバーの色変えられるのでよい。

```
bot.reply(message, {
  attachments: [
    {
      fallback: "Success",
      color: "good",
      title: `#${result.number} ${result.title}`,
      title_link: result.html_url,
      text: "プルリクできたのだー:smirk_cat:"
    }
  ]
});
```

んで、いつもBotとかホストするのにherokuにホストしてたけど、最近GCPまわり触ってるからせっかくなので、GCEにホストした。

- [Google Compute Engine上でSlackのBotkitを動かすぞい！ \- Qiita](https://qiita.com/operandoOS/items/01dd36264f735782f64b)

すごく簡単だった。


```
token=your_token nohup node slack_bot.js &
```

あとバックグラウンドでもプロセスを活かすためには、`nohup [command] &`と打てばよいと教えてもらった。ありがとう。



