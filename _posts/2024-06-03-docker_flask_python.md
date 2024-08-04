---
id: 186
title: 'Dockerで始めるPython開発: 仮想環境(venv)なしで簡単にセットアップ'
date: '2024-06-03T21:29:07+09:00'
author: '宮川　剛'
layout: post
guid: 'https://miyasols.com/?p=186'
permalink: /docker/docker_flask_python/
image: /wp-content/uploads/2024/06/virtualReality.jpg
categories:
    - Docker
    - Python
---

Dockerを利用する際、仮想環境 (venv) を使うことは一般的ではありません。Dockerコンテナ自体が仮想環境の役割を果たしているため、仮想環境を追加で作成する必要はありません。以下に、その理由とDockerを使った典型的なPython開発環境の設定方法を説明します。

## <span class="ez-toc-section" id="Docker%E3%82%92%E4%BD%BF%E7%94%A8%E3%81%99%E3%82%8B%E7%90%86%E7%94%B1"></span>Dockerを使用する理由<span class="ez-toc-section-end"></span>

### <span class="ez-toc-section" id="%E9%9A%94%E9%9B%A2%E3%81%95%E3%82%8C%E3%81%9F%E7%92%B0%E5%A2%83"></span>隔離された環境<span class="ez-toc-section-end"></span>

Dockerコンテナは独立した環境を提供し、ホストシステムと分離された環境でアプリケーションを実行します。これにより、依存関係の衝突や環境の違いによる問題が回避されます。

### <span class="ez-toc-section" id="%E8%BB%BD%E9%87%8F%E5%8C%96"></span>軽量化<span class="ez-toc-section-end"></span>

仮想環境 (venv) は通常、ホストシステム上でPythonの依存関係を管理するために使用されますが、Dockerコンテナ内では不要です。Dockerイメージ内で必要なPythonパッケージを直接インストールすることで、よりシンプルで効率的な設定が可能になります。

## <span class="ez-toc-section" id="%E5%89%8D%E6%8F%90%E6%9D%A1%E4%BB%B6"></span>前提条件<span class="ez-toc-section-end"></span>

以下のツールがインストールされていることが前提となります。

- Python 3.12.2がインストールされていること。
- Docker Desktop for Windows または Docker Desktop for Mac がインストールされており、かつ起動していること。
- Visual Studio Code (VSCode) がインストールされていること。

## <span class="ez-toc-section" id="Docker%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%9FPython%E9%96%8B%E7%99%BA%E7%92%B0%E5%A2%83%E3%81%AE%E8%A8%AD%E5%AE%9A%E6%96%B9%E6%B3%95"></span>Dockerを使ったPython開発環境の設定方法<span class="ez-toc-section-end"></span>

以下の手順で、仮想環境 (venv) を使わずにDockerのみでPython開発環境を設定します。

### <span class="ez-toc-section" id="%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E3%81%AE%E6%BA%96%E5%82%99"></span>プロジェクトディレクトリの準備<span class="ez-toc-section-end"></span>

まず、プロジェクトディレクトリを以下のように構成します。

```
project/
├── apps/
│   ├── __init__.py
│   └── app.py
├── Dockerfile
├── docker-compose.yml
└── requirements.txt
```

### <span class="ez-toc-section" id="Flask%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E4%BD%9C%E6%88%90"></span>Flaskアプリケーションの作成<span class="ez-toc-section-end"></span>

`apps/app.py` ファイルに以下の Python コードを追加します。

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

`apps/__init__.py` ファイルは空のままで構いません。

### <span class="ez-toc-section" id="Dockerfile%E3%81%AE%E4%BD%9C%E6%88%90"></span>Dockerfileの作成<span class="ez-toc-section-end"></span>

プロジェクトディレクトリに `Dockerfile` を作成し、以下の内容を追加します。

```
# Use the official Python image from the Docker Hub
FROM python:3.12.2-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements.txt file into the container at /app
COPY requirements.txt /app/

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the current directory contents into the container at /app
COPY . /app

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Run blogapp.py when the container launches
CMD ["python", "apps/blogapp.py"]
```

### <span class="ez-toc-section" id="requirementstxt%E3%81%AE%E4%BD%9C%E6%88%90"></span>requirements.txtの作成<span class="ez-toc-section-end"></span>

`requirements.txt` ファイルを作成し、以下を追加します。

```
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
```

この設定により、ホストマシンのカレントディレクトリ（`blogproject`）がコンテナの `/app` ディレクトリと同期されます。

### <span class="ez-toc-section" id="Docker%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E3%83%93%E3%83%AB%E3%83%89%E3%81%A8%E8%B5%B7%E5%8B%95"></span>Dockerコンテナのビルドと起動<span class="ez-toc-section-end"></span>

以下のコマンドを使用して、Dockerコンテナをビルドし、起動します。

```
docker-compose build
docker-compose up
```

この構成により、VSCodeでホストマシン上のファイルを編集すると、その変更が即座にコンテナ内に反映されます。また、コンテナ内での変更もホストマシンに反映されるため、ホストマシン上でPythonやFlaskのソースファイルを直接見ることができます。

## <span class="ez-toc-section" id="%E8%BF%BD%E5%8A%A0%E6%83%85%E5%A0%B1"></span>追加情報<span class="ez-toc-section-end"></span>

### <span class="ez-toc-section" id="%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E7%A2%BA%E8%AA%8D"></span>アプリケーションの確認<span class="ez-toc-section-end"></span>

アプリケーションが正しく起動した場合、ブラウザで `http://localhost:5000` にアクセスして「Hello, World!」が表示されることを確認します。

<figure class="wp-block-image size-full is-resized">![](https://i0.wp.com/miyasols.com/wp-content/uploads/2024/06/vscode.png?resize=609%2C120&ssl=1)<figcaption class="wp-element-caption">VSCode で 「docker-compose up」後、プロジェクトが動いた後、 http://127.0.0.1:5000 を CTRL + クリックでブラウザが起動します。</figcaption></figure>### <span class="ez-toc-section" id="Docker%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AE%E3%83%AD%E3%82%B0%EF%BC%8F%E3%82%B9%E3%83%86%E3%83%BC%E3%82%BF%E3%82%B9%E7%A2%BA%E8%AA%8D"></span>Dockerコンテナのログ／ステータス確認<span class="ez-toc-section-end"></span>

Dockerコンテナのログやステータスを確認するには、`docker-compose logs` コマンドを使用します。

### <span class="ez-toc-section" id="%E6%96%B0%E3%81%97%E3%81%84%E3%83%A9%E3%82%A4%E3%83%96%E3%83%A9%E3%83%AA%E3%83%BC%E3%81%AE%E8%BF%BD%E5%8A%A0"></span>新しいライブラリーの追加<span class="ez-toc-section-end"></span>

新しいPythonライブラリを追加したい場合は、`requirements.txt` にそのライブラリを追加し、以下のコマンドを実行します。

```
docker-compose build
docker-compose up
```

または、Dockerコンテナが起動している状態で、コンテナ内に入って直接 `pip install` コマンドを使用してインストールすることもできます。

#### <span class="ez-toc-section" id="%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8AID%E3%82%92%E7%A2%BA%E8%AA%8D"></span>コンテナIDを確認<span class="ez-toc-section-end"></span>

```
docker ps
```

このコマンドは、現在実行中のDockerコンテナの一覧を表示します。`CONTAINER ID` 列にコンテナIDが表示されます。

#### <span class="ez-toc-section" id="%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E3%81%AB%E5%85%A5%E3%82%8A%E3%81%BE%E3%81%99"></span>コンテナに入ります<span class="ez-toc-section-end"></span>

```
docker exec -it <コンテナID> bash
```

`<コンテナID>` には、先ほど確認したコンテナIDを入力します。

#### <span class="ez-toc-section" id="%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%BE%E3%81%99"></span>パッケージをインストールします<span class="ez-toc-section-end"></span>

```
pip install <パッケージ名>
```

<span style="color: rgb(13, 13, 13); font-family: ui-sans-serif, -apple-system, system-ui, "Segoe UI", Roboto, Ubuntu, Cantarell, "Noto Sans", sans-serif, Helvetica, "Apple Color Emoji", Arial, "Segoe UI Emoji", "Segoe UI Symbol"; font-size: 16px; background-color: rgb(255, 255, 255);">例えば、</span>`requests`<span style="color: rgb(13, 13, 13); font-family: ui-sans-serif, -apple-system, system-ui, "Segoe UI", Roboto, Ubuntu, Cantarell, "Noto Sans", sans-serif, Helvetica, "Apple Color Emoji", Arial, "Segoe UI Emoji", "Segoe UI Symbol"; font-size: 16px; background-color: rgb(255, 255, 255);"> パッケージをインストールする場合は以下のようにします。</span>

```
pip install requests
```


この手順を踏むことで、仮想環境 (venv) を使わずに効率的なPython開発環境を構築できます。Dockerの利点を最大限に活用し、依存関係や環境の違いによる問題を回避することで、開発作業をスムーズに進めることができます。
