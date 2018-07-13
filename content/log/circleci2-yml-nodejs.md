---
date: 2018-01-30
title: CircleCI 2.0でGAE/Node.jsのプロジェクトをデプロイ（改）
subtitle: Persisting Data in Workflows
categories: 
    - development
excerpt: 前回の記事で、CircleCIからGAEにNode.jsアプリをデプロイ方法を説明したのだけど、もっといい方法があるのではないかと思ってた。
ogimage: https://t32k.me/mol/images/2018/0130-00.png
---

[前回の記事](/mol/log/circleci2-yml/)で、CircleCIからGAEにNode.jsアプリをデプロイ方法を説明したのだけど、もっといい方法があるのではないかと思ってた。

```
version: 2
jobs:
  build:
    working_directory: ~/repo
    docker:
      - image: circleci/node:8

    steps:
      - checkout
      - run:
          name: System information
          command: |
            echo "Node $(node -v)"
            echo "Yarn v$(yarn --version)"
      - run:
          name: Install dependencies
          command: yarn
      - run:
          name: Build
          command: yarn run build
      - run:
          name: Test
          command: yarn test
      - save_cache:
          key: cache-{{ .Branch }}-{{ checksum "yarn.lock" }}
          paths:
            - ~/repo/.cache/yarn
            - ~/repo/dist
            - ~/repo/node_modules
            - ~/repo/package.json  
  
  deploy:
    working_directory: ~/repo
    docker:
      - image: google/cloud-sdk

    steps:
      - checkout
      - restore_cache:
          key: cache-{{ .Branch }}-{{ checksum "yarn.lock" }}
      - run:
          name: Deploy to Google App Engine
          command: |
            echo "$GOOGLE_AUTH" | base64 -i --decode > "$HOME/gcp-key.json"
            gcloud auth activate-service-account --key-file "$HOME/gcp-key.json"
            gcloud --quiet config set project "$GOOGLE_PROJECT_ID"
            gcloud --quiet app deploy app.yaml --version $(echo $CIRCLE_BRANCH | sed "s/\//\-/g")
          no_output_timeout: 20m
```

`build`と`deploy`でDockerイメージが違うのが嫌だなーって思っていて、これをどうすうるのがいいんだろうと考えたら、やっぱり `circleci/node`のイメージをベースに[Google Cloud SDKをインストール](https://cloud.google.com/sdk/downloads?hl=ja)したイメージを用意するのがいいんだろうと思ったけど、ぼくのDocker力が足りないので、うまくいかず、すぐ諦めた。

## Google Cloud SDK インストール
そしたら去年の10月頃にこうゆうものが出ていたことを知る。

- [GoogleCloudPlatform/cloud\-sdk\-npm\-package: A metapackage that installs Google Cloud Platform's gcloud CLI through NPM](https://github.com/GoogleCloudPlatform/cloud-sdk-npm-package)

npmインストールでCloud SDKをインストールできる代物。うん便利。ローカルで試したところ本当にnpmインストールで、PATHも設定してないのに、`gcloud`コマンドが打てた。

CI上で試してみるとなぜかうまくいかない。`gcloud`コマンドなんてないよ！と怒られる。どうやら、CircleCI上の`$SHELL`の環境変数が`/bin/bash`になってないと、うまく環境を認識できず（`zsh`とか`fish`と区別できない）、[PATHが設定できてないっぽい](https://github.com/GoogleCloudPlatform/cloud-sdk-npm-package/blob/master/helpers-unix.js#L93)。

なので、↓みたいに明示的に指定してあげる必要がある。

```
echo 'source ~/node_modules/@google-cloud/cloud-sdk/google-cloud-sdk/path.bash.inc' >> $BASH_ENV
```

というわけで、無事打てました。

## Job間のデータ共有

これで`circleci/node`のイメージひとつだけ使えるようになった。勘違いしてたのだけど、前回のyamlでJob間dでデータ共有できなかったのはJobのDockerイメージが異なるものだからだと思っていたけど、そうではなかった。

[![](/mol/images/2018/0130-01.png)](https://circleci.com/blog/persisting-data-in-workflows-when-to-use-caching-artifacts-and-workspaces/)

同じ（種類の）イメージでも、`build`Jobで生成したデータを次の`deploy`Jobには持ち越せない。通常データの共有はできない。そうゆうときはCachingを使えばよいのかと思っていたけど、微妙に違ってた。

[![](/mol/images/2018/0130-00.png)](https://circleci.com/blog/persisting-data-in-workflows-when-to-use-caching-artifacts-and-workspaces/)

Cachingは異なるWorkflow間でのデータ共有であり、異なるJob間のデータ共有はWorkspaceという機能を使うのが正しい。

`persist_to_workspace`という項目で、共有したいデータを指定し、`attach_workspace`で取り出す。


```  
version: 2

# =============================================
# References: Reusable Sets
# =============================================
references:
  container_config: &container_config
    docker:
      - image: circleci/node
    working_directory: ~/repo

  restore_npm: &restore_npm
    restore_cache:
      keys:
        - v1-cache-{{ arch }}-{{ .Branch }}-{{ checksum "package-lock.json" }}
        - v1-cache-{{ arch }}-{{ .Branch }}
        - v1-cache

# =============================================
# Jobs: Build and Deploy
# =============================================
jobs:
  build:
    <<: *container_config
    steps:
      - checkout
      - *restore_npm
      - run:
          name: Install Dependencies
          command: npm install
      - save_cache:
          key: v1-cache-{{ arch }}-{{ .Branch }}-{{ checksum "package-lock.json" }}
          paths:
            - node_modules
      - run:
          name: Build
          command: npm run build
      - persist_to_workspace:
          root: dist
          paths:
            - . 
      - run:
          name: Test
          command: npm test

  deploy:
    <<: *container_config
    steps:
      - checkout
      - *restore_npm
      - run:
          name: Set $PATH for `gcloud` command
          command: echo 'source /home/circleci/repo/node_modules/@google-cloud/cloud-sdk/google-cloud-sdk/path.bash.inc' >> $BASH_ENV
      - attach_workspace:
          at: dist
      - run:
          name: Deploy to Google App Engine
          command: gcloud app deploy app.yaml
          no_output_timeout: 20m
          
# Workflowsの設定・・・
```

というわけで、こんな感じになった。`&`と`*`は[YAML記法](https://qiita.com/gctfuji/items/5f8e4c5795ce41b214d1)アンカーとエイリアスで、変数っぽく使える。

- [frontend/config\.yml at master · circleci/frontend](https://github.com/circleci/frontend/blob/master/.circleci/config.yml)

あと、本家の本気のconfig.ymlを見て参考にしたが、Jobが分割されすぎて震えた。

