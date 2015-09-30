# Docker with No Dockerfile

株式会社スタイルレシピ

山内雅浩

---

## この発表の対象

デプロイスクリプトを書きたいんじゃなくてアプリを書きたいみなさまを対象にしています。

---

## まだ Dockerfile で消耗してるの？

もう Dockerfile を書かなくてもいいんだよ。

---

## Dokku-alt で Dockerfile を1行も書かないで Docker 環境が簡単に作れます！

---

## Dokku-alt とは？

Dokku-alt is a Docker powered mini-Heroku.
Heroku で提供しているアプリケーションのビルド(buildpack)に対応しています。

--

## Dokku-alt で出来ること

1. Docker コンテナにアプリを構築する
2. Nginx による NAT
3. Nginx によるサーバ名の割当

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

あらかじめアプリケーションを作成して git で管理してあるものとします。

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

## dokku-alt のデプロイファイル

実は Dokku-alt 環境の構築に Dockerfile も使えます。

| ファイルの種類 | 長所 | 短所 |
| ---- | ---- | ---- |
| Procfile | 記述がシンプル | 毎回ビルドに時間がかかる |
| Dockerfile | 差分ビルドできるのでビルド時間を短縮できる | 記述するのが面倒 |

---

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

終わり

