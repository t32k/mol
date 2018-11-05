GitHub Pages---
date: 2018-11-06
title: CircleCIでHugoを実行してGitHub Pagesにデプロイ
subtitle: Automate Your Blog Deployment with CircleCI on GitHub Pages
categories: 
    - development
excerpt: 
ogimage: 
---

これまではHugoで生成したHTMLをWerckerでGitHub Pagesにデプロイしていたんだけど、定期的にWerckerのアップデートかなんかで動かなくなる・修正するを何回かやった結果、疲弊して、めんどくさくなった。

最近ではすっかりブログ書かなくなったのもあって、手元でHugoを動かして直接`docs`フォルダにHTMLを直接コミットするという体たらくであった。先の記事で購入したWEB+DB PRESSの特集の一つがCircleCIだったので、ちゃったCIでデプロイしてみようとした話。

まぁ、そうゆうわけで、`Hugo` + `CircleCI` + `GitHub Pages`の構成で動かしたかったわけだけど、うまいことコレ！ってのがなかったので、以下の記事を参考にかけ合わせた感じ。

- [Automate Your Static Site Deployment with CircleCI - CircleCI](https://circleci.com/blog/automate-your-static-site-deployment-with-circleci/)
- [RealOrangeOne: Example setup for deploying a hugo site to github pages using circleci](https://github.com/RealOrangeOne/circleci-hugo-template)

以下はメモ

## CircleCI 2.0

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

dockerイメージとして、[cibuilds/hugo:latest](https://github.com/cibuilds/docker-hugo)という、ドンピシャなイメージがあった。Hugoはgolang製なので、記事をググってると、まずみんなgolangのイメージを選んでHugoをインストールしてしてたけど、このイメージはその必要はないので便利。


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
            - "c5:38:a6:05:63:ab:e6:56:e1:2f:88:76:b7:2c:f4:05"
```

```
      - deploy:
          name: Deploy to GitHub Pages
          command: |
            chmod +x ./.circleci/deploy.sh
            ./.circleci/deploy.sh
```


