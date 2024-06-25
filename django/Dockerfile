# Python 3.12のイメージを使用
FROM python:3.12-slim

# 作業ディレクトリを設定
WORKDIR /code

# 必要なパッケージをインストール
RUN apt-get update && apt-get install -y \
  gcc \
  libmariadb-dev \
  pkg-config \
  default-libmysqlclient-dev \
  build-essential \
  && rm -rf /var/lib/apt/lists/*

# 依存関係ファイルをコピー
COPY requirements.txt .

# Pythonパッケージをインストール
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# プロジェクトファイルをコピー
COPY . .

# uWSGIを実行
CMD ["uwsgi", "--socket", ":8001", "--module", "Djangoプロジェクト名.wsgi", "--py-autoreload", "1", "--logto", "/tmp/mylog.log"]
