---
date: 2018-11-06
title: CircleCIでHugoを実行してGitHub Pagesにデプロイ
subtitle: Automate Your Blog Deployment with CircleCI on GHPages
categories: 
    - development
excerpt: シェルスクリプトの書き方覚えても数秒で忘れてしまう難病なので、何してるか、わかんなかったので自分用にコメントしとく。
ogimage: https://t32k.me/mol/images/2018/1106-00.png
---

これまではHugoで生成したHTMLをWerckerでGitHub Pagesにデプロイしていたんだけど、定期的にWerckerのアップデートかなんかで動かなくなる・修正するを何回かやった結果、疲弊して、めんどくさくなった。

最近ではすっかりブログ書かなくなったのもあって、手元でHugoを動かして`docs`フォルダにHTMLを直接コミットするという体たらくである。[先の記事で購入したWEB+DB PRESS](/mol/log/978-4297101725-web-db-press-107/)の特集の一つがCircleCIだったので、ちゃんとCIでデプロイしてみようとした話。

まぁ、そうゆうわけで、`Hugo` + `CircleCI` + `GitHub Pages`の構成で動かしたかったわけだけど、うまいことコレ！ってのがなかったので、以下の記事を参考にかけ合わせた感じ。

- [Automate Your Static Site Deployment with CircleCI - CircleCI](https://circleci.com/blog/automate-your-static-site-deployment-with-circleci/)
- [RealOrangeOne: Example setup for deploying a hugo site to github pages using circleci](https://github.com/RealOrangeOne/circleci-hugo-template)

以下はメモ

## CircleCI 2.0

![](/mol/images/2018/1106-01.png)

まずは、CircleCI側、config.ymlの設定。

```
version: 2
jobs:
  build:
    branches:
      only:
        - master
```

まぁ、ブログなので、`master`オンリーのブランチで実行。

```
 docker:
      - image: cibuilds/hugo:latest
```

dockerイメージとして、[cibuilds/hugo:latest](https://github.com/cibuilds/docker-hugo)という、ドンピシャなイメージがあった。Hugoはgolang製なので、記事をググってると、まずみんなgolangのイメージを選んでHugoをインストールしてしてたけど、このイメージはそのステップが必要はないので便利。

```
    working_directory: ~/hugo
    steps:
      - run:
          name: Update enviroment
          command: apk update && apk add git
```


`cibuilds/hugo`イメージはAlpine Linuxベースとのことで、`apk`でパッケージを最新にしといて、`git`も追加。


```
      - run:
          name: System information
          command: echo "$(hugo version)"
      - checkout
      - run:
          name: Building blog pages
          command: |
            HUGO_ENV=production hugo -v
            cp public/index.xml public/feed.xml
```

あとは、GitHubからコードをチェックアウトして、Hugoで生成している。RSS用に`feed.xml` にコピーしとく。


```
      - add_ssh_keys:
          fingerprints:
            - "SO:ME:FIN:G:ER:PR:IN:T"
```
   
デフォルトで作成されるdeploy keyはチェックアウトする(read)だけの権限なので、ghpageブランチにコミット(write)できる権限を作成しとく。

**Add user key** ボタンを押すとユーザーレベルのSSH keyが登録されるので、GitHubの設定ページで、そのFingerprintをコピーして上記に追加。
   
```
      - deploy:
          name: Deploy to GitHub Pages
          command: |
            chmod +x ./.circleci/deploy.sh
            ./.circleci/deploy.sh
```

あとはデプロイ用のシェルスクリプトを実行している。

## GitHub Pages

シェルスクリプトの書き方覚えても数秒で忘れてしまう難病なので、ほぼ[RealOrangeOne](https://github.com/RealOrangeOne/circleci-hugo-template/blob/master/.circleci/deploy.sh)氏のコードを拝借している。何してるか、わかんなかったので自分用にコメントしとく。

```
#!/usr/bin/env bash

# エラー時、実行を止める
set -e

DEPLOY_DIR=deploy

# gitの諸々の設定
git config --global push.default simple
git config --global user.email $(git --no-pager show -s --format='%ae' HEAD)
git config --global user.name $CIRCLE_USERNAME

# gh-pagesブランチをdeployディレクトリにクローン
git clone -q --branch=gh-pages $CIRCLE_REPOSITORY_URL $DEPLOY_DIR

# rsyncでhugoで生成したHTMLをコピー
cd $DEPLOY_DIR
rsync -arv --delete ../public/* .

git add -f .
git commit -m "Deploy #$CIRCLE_BUILD_NUM from CircleCI [ci skip]" || true
git push -f
```

`push.default simple` って何の設定なんだろうと思ったけど、これのおかげで、`git push origin gh-pages`とかしなくていいのか。なるほど simple!

- [git push引数省略時のデフォルト動作設定 - Qiita](https://qiita.com/dehali22/items/09cc89ed87f022668d80)

これでしばらくは、デプロイが安定するだろう...( ˘ω˘)ｽﾔｧ