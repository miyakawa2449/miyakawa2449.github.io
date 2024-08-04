---
id: 156
title: DockerとFlaskで簡単に始める！VSCodeを使ったWebアプリケーション開発入門
date: '2024-05-24T13:53:19+09:00'
author: '宮川　剛'
layout: post
guid: 'https://miyasols.com/?p=156'
permalink: /docker/docker_flask_app_dev_intro/
image: /wp-content/uploads/2024/05/programerDT.jpg
categories:
    - Docker
---

ウェブアプリケーションの開発を始める際、環境設定や依存関係の管理は非常に重要です。しかし、複雑で手間のかかる作業でもあります。そこで、Dockerを使用することで、ホストマシンと分離された一貫性のある開発環境を提供し、依存関係の衝突や環境の違いによる問題を回避することができます。このブログでは、人気の高いフレームワークであるFlaskを使って、Docker環境で簡単にウェブアプリケーションを構築する方法をステップバイステップで解説します。特にVSCode（Visual Studio Code）を利用した開発方法に焦点を当て、初めてDockerを使う方でも分かりやすい内容を目指します。

#### <span class="ez-toc-section" id="%E5%BF%85%E8%A6%81%E3%81%AA%E3%83%84%E3%83%BC%E3%83%AB%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB"></span>必要なツールのインストール<span class="ez-toc-section-end"></span>

まず、以下のツールをインストールします。

- [VSCode](https://code.visualstudio.com/): モダンで強力なコードエディタ。多くの拡張機能により、様々な開発環境をサポート。
- <a>Docker Desktop</a>: コンテナベースの仮想化プラットフォーム。簡単にアプリケーションを分離された環境で実行可能に。

VSCodeには、以下の拡張機能もインストールしておくと便利です。

- Docker
- Python

---

#### <span class="ez-toc-section" id="%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97"></span>プロジェクトのセットアップ<span class="ez-toc-section-end"></span>

まず、VSCodeで新しいプロジェクトディレクトリを作成します。

```
`mkdir flask-docker-appcd flask-docker-app`
```

---

#### <span class="ez-toc-section" id="%E7%92%B0%E5%A2%83%E3%81%AE%E5%88%86%E9%9B%A2%E3%81%A8%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E5%86%85%E3%81%A7%E3%81%AE%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E5%AE%9F%E8%A1%8C"></span>環境の分離とコンテナ内でのコマンド実行<span class="ez-toc-section-end"></span>

**環境の分離**: Dockerを使用することで、ホストマシンと分離された環境でアプリケーションを実行できます。これにより、依存関係の衝突や環境の違いによる問題を回避できます。

**コンテナ内でのコマンド実行**: Flaskコマンドや他の開発ツールを実行する際には、基本的にコンテナ内で実行します。ホストマシンにインストールされているかどうかに依存せず、一貫した環境で作業できます。

---

#### <span class="ez-toc-section" id="Dockerfile%E3%81%AE%E4%BD%9C%E6%88%90"></span>Dockerfileの作成<span class="ez-toc-section-end"></span>

プロジェクトディレクトリ内に`Dockerfile`を作成し、以下の内容を追加します。

```
`FROM python:3.12-slimWORKDIR /appCOPY requirements.txt requirements.txtRUN pip install -r requirements.txtCOPY . .CMD ["flask", "run", "--host=0.0.0.0"]`
```

この`Dockerfile`では、コンテナ内にPythonとFlaskの依存関係をインストールしています。これにより、ローカルマシンではなくコンテナ内でFlaskが実行されます。

---

#### <span class="ez-toc-section" id="docker-composeyml%E3%81%AE%E4%BD%9C%E6%88%90"></span>docker-compose.ymlの作成<span class="ez-toc-section-end"></span>

次に、`docker-compose.yml`ファイルを作成し、以下の内容を追加します。

```
`version: '3.8'services:  web:    build: .    ports:      - "5000:5000"    volumes:      - .:/app    environment:      FLASK_ENV: development      FLASK_APP: app.py`
```

---

#### <span class="ez-toc-section" id="Flask%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E4%BD%9C%E6%88%90"></span>Flaskアプリケーションの作成<span class="ez-toc-section-end"></span>

`requirements.txt`ファイルを作成し、Flaskの依存関係を追加します。

```
`Flask==2.3.2`
```

次に、`app.py`ファイルを作成し、シンプルなFlaskアプリケーションを記述します。

```
`from flask import Flaskapp = Flask(__name__)@app.route('/')def hello_flask():    return 'Hello, Flask!'@app.route('/hello')def hello_world():    return 'Hello, World!'if __name__ == '__main__':    app.run(debug=True)`
```

このステップで作成した`requirements.txt`と`app.py`は、`Dockerfile`で指定した通り、コンテナ内にコピーされます。これにより、Flaskの依存関係がコンテナ内にインストールされ、Flaskアプリケーションがコンテナ内で実行されるようになります。

---

#### <span class="ez-toc-section" id="%E3%83%9C%E3%83%AA%E3%83%A5%E3%83%BC%E3%83%A0%E3%83%9E%E3%82%A6%E3%83%B3%E3%83%88"></span>ボリュームマウント<span class="ez-toc-section-end"></span>

ローカルのプロジェクトディレクトリをコンテナにマウントすることで、コードの変更を即座にコンテナに反映させることができます。これにより、開発サイクルがスムーズになります。`docker-compose.yml`で以下の設定を確認してください。

```
`volumes:  - .:/app`
```

---

#### <span class="ez-toc-section" id="%E3%83%AD%E3%82%B0%E3%81%A8%E3%83%87%E3%83%90%E3%83%83%E3%82%B0"></span>ログとデバッグ<span class="ez-toc-section-end"></span>

コンテナのログを確認することで、エラーやデバッグ情報を簡単に取得できます。以下のコマンドを使用します。

- `docker logs` コマンド

```
docker logs <container_id_or_name>
```

- `docker-compose logs` コマンド

```
docker-compose logs
```

---

#### <span class="ez-toc-section" id="Docker%E3%82%B3%E3%83%B3%E3%83%86%E3%83%8A%E5%86%85%E3%81%A7Flask%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%82%92%E5%AE%9F%E8%A1%8C"></span>Dockerコンテナ内でFlaskコマンドを実行<span class="ez-toc-section-end"></span>

VSCodeのターミナルを使用して、以下のコマンドを実行します。

- Dockerコンテナをビルドして起動します。

```
`docker-compose up -d`
```

- 実行中のコンテナを確認します。

```
`docker ps`
```

ここで、実行中のコンテナのIDまたは名前を確認します。

- 対象のコンテナに接続します。

```
`docker exec -it <container_id_or_name> /bin/bash`
```

このコマンドを実行すると、指定したコンテナの内部にシェルが開きます。これにより、まるでSSHでリモートサーバーに接続するかのように、コンテナ内の環境にアクセスできます。

- コンテナ内でFlaskコマンドを実行します。

```
`flask routes`
```

これで、FlaskアプリケーションがDockerコンテナ内で正常に動作していることを確認できます。

— 表示例 —

```
PS C:\Users\name\projects\> docker exec -it 385c43332f91 /bin/bash
root@385c43332f91:/apps/minimalapp# ls
<strong>init</strong>.py app.py
root@385c43332f91:/apps/minimalapp# flask routes
Endpoint        Methods Rule
--------------- ------- -----------------------
hello_flask     GET     /
hello_world     GET     /hello
static          GET     /static/
```

---

#### <span class="ez-toc-section" id="%E3%81%BE%E3%81%A8%E3%82%81"></span>まとめ<span class="ez-toc-section-end"></span>

このブログでは、VSCodeを使用してDocker上でFlaskアプリケーションをセットアップする方法について詳しく説明しました。Dockerを使用することで、開発環境を一貫して管理でき、依存関係の問題を回避することができます。FlaskとDockerの基本を理解し、さらに応用していくための第一歩として、ぜひ試してみてください。

Dockerは、Flaskだけでなく、他のWebアプリケーションフレームワーク（例：Django、Rails）を使用する際にも非常に有用です。今回のガイドを通じて、Dockerの基礎を学び、効率的な開発環境を手に入れてください。次回は、さらに進んだDockerの使い方や、Flaskアプリケーションのデプロイ方法についても触れていきたいと思います。お楽しみに！

---

以上で、DockerとFlaskを使った簡単なWebアプリケーション開発の基本的な流れを紹介しました。今後の開発プロジェクトに役立てていただければ幸いです。Happy Coding!
