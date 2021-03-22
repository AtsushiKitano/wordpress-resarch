Wordpress Infra
==

# 概要
Wordpressのインフラ設定などの調査結果をまとめる

# インストール
dockerでのインストールは[公式のページ](https://hub.docker.com/_/wordpress)よりMySQLとWordpressのイメージをpullし構築

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

# 参照ページ

- [Docker Compose Wordpress サンプル](https://docs.docker.jp/compose/wordpress.html)
