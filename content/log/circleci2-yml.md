---
date: 2017-09-14
title: CircleCI 2.0でGAE/Node.jsのプロジェクトをデプロイ
subtitle: 
categories: 
    - development
excerpt: 基本、ずっとTravisかWerckerを使ってたんだけど、CircleCIデビューしてみた。
---

基本、ずっとTravisかWerckerを使ってたんだけど、CircleCIデビューしてみた。今年の7月にCircleCI 2.0がリリースされ、config.ymlの記法も刷新されたとかで、ググって出て来るのは1.0の記法ばかりで苦労したので、メモ代わりに残しとく。

- [CircleCI2\.0事始め \-新しいcircle\.ymlとworkflows編 · tehepero note\(・ω<\) 2\.0](https://blog.stormcat.io/post/entry/circleci2.0-overview01/)

基本は上記のブログがわかりやすい。

```yaml
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
```

`version: 2` で2.0でやりまっせーって宣言して、dockerイメージとか指定していく。`yarn` がデフォルトで入ってるらしく、GAE/Node.jsも`yarn`が使えるので`yarn`を使っていく。

あとは`run`でステップを指定していく。`command`は`|`を置けば、複数行でも書ける。

```yaml
      - save_cache:
          key: cache-{{ .Branch }}-{{ checksum "yarn.lock" }}
          paths:
            - ~/repo/.cache/yarn
            - ~/repo/dist
            - ~/repo/node_modules
            - ~/repo/package.json
```

- [Using Keys and Templates \- Caching Dependencies \- CircleCI](https://circleci.com/docs/2.0/caching/#using-keys-and-templates)

`{{ hoge }}`はテンプレートで、`checksum` は base64でハッシュを作ってくれる。
ここではユニークなkey名を指定したくて、こんな風にしている。あとはキャッシュさせたいパス。

`build`ステップは終わり。

```yaml
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

つぎに、`deploy`ステップ。`gcloud app deploy`のコマンドでデプロイするので、`gcloud`が入ったdockerイメージを指定。

`restore_cache` で先のステップで保存しといたファイルを呼び出す。

あとはデプロイコマンド。CI上でデプロイするので権限をもったサービスアカウントを作らなければならない。

- [Circle CIでCloud Functionをデプロイする \- GeekFactory](http://int128.hatenablog.com/entry/2017/08/12/153538)

上記はCloud Functionだけど、認証の部分は同じなので真似するとよい。んで、エンコードしたものをCircleCIの環境変数として登録しておく。

- [Using Environment Variables \- CircleCI](https://circleci.com/docs/2.0/env-vars/#build-details)

`$CIRCLE_BRANCH`はCircleCIが設定している環境変数。ビルド番号とかもある。

あと`no_output_timeout`は、GAE/Node.jsへのデプロイがくっそ遅くて、タイムアウト（デフォルト10分）になるので20分に伸ばしてる。

```yaml
workflows:
  version: 2
  build_and_deploy:
    jobs:
      - build
      - deploy:
          requires:
            - build
```

最後はワークフローの設定。[フィルター](https://circleci.com/docs/2.0/configuration-reference/#filters)とかでmasterブランチのときだけ実行とか、必須条件とか決めれる。便利。

## 参考

- [CircleCI 2.0に移行して新機能を活用したらCIの実行時間が半分になった話 - クラウドワークス エンジニアブログ](http://engineer.crowdworks.jp/entry/2017/04/04/202719)