# Docker with No Dockerfile

株式会社スタイルレシピ  
山内雅浩  
@algas  

---

## この発表の対象

「デプロイスクリプトを書きたいんじゃない、  
アプリを書きたいんだ」  
というみなさまを対象にしています。

---

### まだ Dockerfile で消耗してるの？

--

## もう Dockerfile を書かなくてもいいんだよ

Dokku-alt で Dockerfile を1行も書かないで  
Docker 環境が簡単に作れます！

---

## Dokku-alt とは？

Dokku-alt is a Docker powered mini-Heroku.  
https://github.com/dokku-alt/dokku-alt

1. Docker コンテナにアプリを構築する
2. Nginx による NAT
3. Nginx によるサーバ名の割当

---

## Dokku-alt で出来ること

---

## Dokku-alt のセットアップ

Dokku-alt をインストールする Ubuntu を用意します。

--

### 1. dokku-alt のインストール

```
sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/dokku-alt/dokku-alt/master/bootstrap.sh)"
```

--

### 2. ssh 公開鍵の登録

```
cat ~/.ssh/id_rsa.pub | ssh your-dokku-host sudo dokku access:add
```

--

### 以上！

---

## アプリケーションのデプロイ

あらかじめアプリケーションを作成して  
git で管理してあるものとします。

--

### 1. Procfile の作成

Procfile (node.js の場合の例)
```
web: node index.js
```

git に追加
```
git add Procfile && git commit -m "Add Procfile"
```

--

### 2. Git remote の設定

```
git remote add dokku dokku@your-dokku-host:node-js-example
git remote -v
```

--

### 3. Push

```
git push dokku your-branch:master
```

--

### デプロイ完了！

---

## デプロイの仕組み

Heroku で提供しているアプリケーションのビルド(buildpack)に対応しています。

--

## デプロイファイルの比較

実は Dokku-alt 環境の構築に Dockerfile も使えます。

| ファイルの種類 | 長所 | 短所 |
| ---- | ---- | ---- |
| Procfile | 記述がシンプル | 毎回ビルドに時間がかかる |
| Dockerfile | 差分ビルドできるのでビルド時間を短縮できる | 記述するのが面倒 |

---

## 基本コマンド

* コンテナ自体の操作  
dokku start/stop/status/rebuild/delete (app)
* アプリ一覧  
dokku apps:list
* 環境変数設定  
dokku config:set (app) foo=bar
* アプリのURL  
dokku url (app)
* コマンド実行  
dokku enter/exec/run (app)
* ログ出力  
dokku logs (app)

--

## 他にこんなこともできちゃいます

* ssl (https) 対応
* サーバ名の割当
* ボリュームコンテナの作成と管理
* 永続的ボリューム(ホストのディレクトリ)の作成と管理
* DB (MariaDB, PostgreSQL, MongoDB, Redis) の Docker コンテナ作成と管理
* Basic 認証
* アプリごとのデプロイユーザ(公開鍵)の制限
* コンテナの無停止更新

---

## 発展的な話題

--

### 本番環境でも使いたい

Beanstalk で Docker コンテナを扱う。  
Docker Hub に push して Beanstalk 設定のための  
json ファイルを書くだけの簡単なお仕事。

--

### コンテナのログ出力を永続化したい

デプロイの度に古いログが消失してしまう。
→fluentd でログを集約する。

3つの設置方法
1. ホストにfluentdをインストールする
2. コンテナにfluentdを含める
3. fluentdコンテナを作成する

---

## 弊社サービスの紹介

株式会社スタイルレシピは  
日本最大のファッションレシピサービス「スタレピ」  
を開発・運用しています。

一言でいうと Cookpad のファッション版です。

---

### 優秀なエンジニアを募集しています！

株式会社スタイルレシピ

recruit@stylerecipe.co.jp

![Cooporate image](img-stylerecipe.jpg)
