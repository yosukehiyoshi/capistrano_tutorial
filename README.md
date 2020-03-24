## Capistranoチュートリアル

社内AWS勉強会で使用するCapistrano設定用のリポジトリです。

## Dependencies

- Ruby 2.7.0
  - bundler 2.1.2
- node 12.10.0
  - yarn 1.22.4
- MySQL 5.7.28

## セットアップ

### Dockerを使用する方

`docker/docker-compose.yml` をリポジトリ直下にコピーし `$ docker-compose build` を実行。

※ RailsのDockerサービス名は `app` としています。

### インストール、設定

Dockerを使用する方は、Railsコンテナ（ `app` ）に接続して進めていってください。

#### bundleインストール

```
$ bundle config set path 'vendor/bundle'
$ bundle install
```

#### yarnインストール

```
$ yarn install
```

#### DB設定 & 作成

```
$ cp config/database.yml.default config/database.yml
$ bin/rails db:create
```

#### Rails起動（foreman）

```
$ bundle exec foreman start
```

#### 環境変数設定

AWSアクセスキー、デプロイ時SSH秘密鍵の設定

※ Docker使用の場合は `docker-compose.yml` の `environment` に書くのがオススメです。

```
$ export DEPLOY_SSH_KEYS="SSH秘密鍵のパス"
$ export AWS_ACCESS_KEY_ID="AWSアクセスキーID"
$ export AWS_SECRET_ACCESS_KEY="AWSアクセスシークレット"
```
