Wordpress Infra
==

# 概要
Wordpressのインフラ設定などの調査結果をまとめる

# インストール
dockerでのインストールは[公式のページ](https://hub.docker.com/_/wordpress)よりMySQLとWordpressのイメージをpullし構築する。

## 実行方法

```
docker-compose up -d
```

# Wordpressの設定

`/var/www/html`に各種設定が格納されている。確認のため、ローカルにマウントさせる。

```
  db:
    image: mysql:5.7
    volumes:
      - ./mount/db:/var/lib/mysql
...

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - ./mount/wp-config:/var/www/html

```

docker-compose.yamlのファイルがあるディレクトリにmountディレクトリを作成し、コンテナをマウントさせている。

## 環境変数の設定項目
Wordpressイメージは起動時に以下の環境変数を渡し、設定することが可能。

| 環境変数名                 | 具体内容                              |
| ---                        | ---                                   |
| WORDPRESS_DB_HOST          | MySQLサーバーのホスト                 |
| WORDPRESS_DB_USER          | MySQLサーバーへのログインするユーザー |
| WORDPRESS_DB_PASSWORD      | MySQLサーバーへのアクセスパスワード   |
| WORDPRESS_DB_NAME          | 起動しているMySQLサーバー名           |
| WORDPRESS_TABLE_PREFIX     |                                       |
| WORDPRESS_AUTH_KEY         |                                       |
| WORDPRESS_SECURE_AUTH_KEY  |                                       |
| WORDPRESS_LOGGED_IN_KEY    |                                       |
| WORDPEPSS_NONCE_KEY        |                                       |
| WORDPEPSS_AUTH_SALT        |                                       |
| WORDPRESS_SECURE_AUTH_SALT |                                       |
| WORDPRESS_LOGGED_IN_SALT   |                                       |
| WORDPRESS_NONCE_SALT       |                                       |
| WORDPRESS_DEBUG            |                                       |
| WORDPRESS_CONFIG_EXTRA     |                                       |

## 各種設定項目

| 目的             | PATH                             |
| --               | --                               |
| テーマの設定     | /var/www/html/wp-content/themes/ |
| プラグインの設定 | /var/www/html/wp-content/plugins/ |

# 参照ページ

- [Docker Compose Wordpress サンプル](https://docs.docker.jp/compose/wordpress.html)
