# Microsoftが提供する開発用コンテナイメージ（Python 3.11）
FROM mcr.microsoft.com/devcontainers/python:1-3.11-bullseye

# 必要なツールがあればここでapt-get installする（今回は特になし）
# RUN apt-get update && apt-get install -y <package-name>

# 作業ディレクトリの設定
WORKDIR /workspace

# ライブラリのインストール
# キャッシュを活用するため、requirements.txtを先にコピー
COPY requirements.txt /tmp/pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
    && rm -rf /tmp/pip-tmp