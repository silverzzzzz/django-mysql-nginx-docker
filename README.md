# django-docker
DjangoのDockerでの開発環境です。
* Django
* MySQL
* Nginx

## ディレクトリ構成
下記のディレクトリ構成になります。
```
.
├── .gitignore
├── .env
├── docker-compose.yml
|
├── django/
|   ├── .env
|   ├── Dockerfile
|   └── requirements.txt
|
├── nginx/
│   ├── nginx.conf
│   └── uwsgi_params
│
├── mysql/
│   └── .env
│
├── sql/
│   └── init.sql
|
├── src/
│   └── ...(Djangoのプロジェクト)
│
└── static/
    └── ... (静的ファイル)
```

## 起動準備
Docker,DockerComposeのインストールを行ってください。

### docker-compose.yml
Djangoプロジェクト名.wsgiの部分をDjangoプロジェクト名で置換してください。
Nginx,MySQLのバージョンを確認してください。

### django/
**Dockerfile**

Djangoプロジェクト名.wsgi の部分を Djangoプロジェクト名で置換してください。

**.env**
Djangoの環境変数です。適宜変更してください。

### mysql/
**.env**
MySQLの設定変数です。適宜変更してください。

### src/
このフォルダ以下にDjangoのprojectを格納してください。

## 起動手順
```
#docker-composeのビルド
docker-compose build

#プロジェクトのの立ち上げ&マイグレーション
docker-compose run --rm django django-admin startproject app .
docker-compose run --rm django python manage.py makemigrations
docker-compose run --rm django python manage.py migrate

#バックグラウンド起動
docker-compose up -d

#停止
docker-compose down -v
```
