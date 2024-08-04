---
id: 173
title: 簡単ステップでプロジェクト開始！GitとGitHub入門
date: '2024-05-27T21:28:46+09:00'
author: '宮川　剛'
layout: post
guid: 'https://miyasols.com/?p=173'
permalink: /github/git_github_initialization/
image: /wp-content/uploads/2024/05/github.jpg
categories:
    - GitHub
---

こんにちは、今回は初めて GitHub でプロジェクト管理を始める初心者プログラマーに向けて、仮想環境の構築からリポジトリの作成、GitHub へのプッシュまでの一連の手順を説明します。具体例として Python 3.12 と Flask を使用していますが、この手順は他のプログラミング言語やフレームワークにも応用できます。これにより、プロジェクトのバージョン管理が容易になり、チームメンバーと協力しやすくなります。

**前提条件**

- git がインストールされていること
- GitHub アカウントを持っていること
- Python 3.12 がインストールされていること

## <span class="ez-toc-section" id="%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E3%81%AE%E4%BD%9C%E6%88%90"></span>プロジェクトディレクトリの作成<span class="ez-toc-section-end"></span>

まず、プロジェクト用のディレクトリを作成し、そのディレクトリに移動します。

```
`mkdir my-new-projectcd my-new-project`
```

## <span class="ez-toc-section" id="git_%E3%81%AE%E5%88%9D%E6%9C%9F%E5%8C%96"></span>git の初期化<span class="ez-toc-section-end"></span>

次に、git を初期化します。これにより、新しいリポジトリが作成され、プロジェクトの変更を追跡できるようになります。

```
`git init`
```

## <span class="ez-toc-section" id="%E4%BB%AE%E6%83%B3%E7%92%B0%E5%A2%83%E3%81%AE%E6%A7%8B%E7%AF%89"></span>仮想環境の構築<span class="ez-toc-section-end"></span>

仮想環境を構築し、アクティブにします。以下のコマンドは Unix 系 (Linux, macOS) の場合です。

```
`python3.12 -m venv venvsource venv/bin/activate`
```

Windows の場合は以下のように仮想環境を構築し、アクティブにします。

```
python -m venv venv
venv\Scripts\activate
```

```
<strong>注意:</strong> ここでは venv で仮想環境を構築しましたが、Docker 環境を使用することもできます。また、最悪仮想環境が無くてもプロジェクトを進めることは可能です。ただし、仮想環境や Docker を使用することで、依存関係の管理がしやすくなりますので、可能であれば使用することをお勧めします。<br></br><br></br>今回は Python を例に取り上げましたが、同様の手順は他の言語でも適用できます。例えば、PHP や Ruby on Rails などのプロジェクトでも、仮想環境や Docker を使用して依存関係を管理することが推奨されます。言語やフレームワークに関わらず、プロジェクトのセットアップと管理は、適切なツールと手順を用いることでより効率的に行うことができます。
```

## <span class="ez-toc-section" id="Flask_%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB"></span>Flask のインストール<span class="ez-toc-section-end"></span>

仮想環境内に Flask をインストールします。

```
`pip install Flask`
```

## <span class="ez-toc-section" id="%E3%82%B7%E3%83%B3%E3%83%97%E3%83%AB%E3%81%AA_Flask_%E3%82%A2%E3%83%97%E3%83%AA%E3%81%AE%E4%BD%9C%E6%88%90"></span>シンプルな Flask アプリの作成<span class="ez-toc-section-end"></span>

ここで作成する Flask アプリは非常にシンプルなものです。この内容は Python に限らず、他の言語やフレームワークでも同様の手順でプロジェクトを進めることができます。Flask を使わない場合でも、このステップはあなたのプロジェクトに応じて適切に置き換えることができます。

以下の内容で `app.py` ファイルを作成します。

```
`from flask import Flaskapp = Flask(__name__)@app.route('/')def hello():    return 'Hello, World!'if __name__ == '__main__':    app.run()`
```

このコードはシンプルな Flask アプリを定義しています。`http://127.0.0.1:5000` にアクセスすると、`Hello, World!` と表示されるはずです。

## <span class="ez-toc-section" id="Flask_%E3%82%A2%E3%83%97%E3%83%AA%E3%81%AE%E5%AE%9F%E8%A1%8C"></span>Flask アプリの実行<span class="ez-toc-section-end"></span>

Flask アプリケーションを実行し、ブラウザで動作を確認します。

```
`python app.py`
```

ブラウザで `http://127.0.0.1:5000` にアクセスして、`Hello, World!` と表示されることを確認します。

```
注意: このステップで実際にエラーが発生せずに動作するプロジェクトを作成することが重要です。何か問題が発生した場合は、エラーメッセージを確認し、必要な修正を行ってください。
```

## <span class="ez-toc-section" id="gitignore_%E3%81%AE%E8%A8%AD%E5%AE%9A"></span> .gitignore の設定<span class="ez-toc-section-end"></span>

プロジェクトのルートディレクトリに `.gitignore` ファイルを作成し、不要なファイルやディレクトリを除外します。これにより、バージョン管理の対象から除外するファイルを指定し、リポジトリをクリーンに保つことができます。

`.gitignore` ファイルに含めるべき一般的なファイルとディレクトリには以下のようなものがあります：

- 仮想環境のディレクトリ (`venv/`)
- Python のコンパイル済みファイル (`__pycache__/`, `*.pyc`, `*.pyo`, `*.pyd`)
- OS 特有のファイル (`.DS_Store` など)
- IDE やエディタの設定ファイル (`.idea/`, `.vscode/`)
- 環境変数ファイル (`.env`)
- その他の一時ファイルやログファイル (`*.log`, `*.swp`)

以下の内容は Python プロジェクトに適した `.gitignore` ファイルの例です。

```
venv/
pycache/
*.pyc
*.pyo
*.pyd
.Python
*.db
*.sqlite3
*.log
.DS_Store
*.swp
.idea/
.vscode/
.env
*.egg-info/
```

この設定により、指定されたファイルやディレクトリは git によって追跡されず、リポジトリに追加されることがなくなります。

## <span class="ez-toc-section" id="%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%81%AE%E8%BF%BD%E5%8A%A0%E3%81%A8%E3%82%B3%E3%83%9F%E3%83%83%E3%83%88"></span>ファイルの追加とコミット<span class="ez-toc-section-end"></span>

プロジェクトのファイルをリポジトリに追加し、最初のコミットを行います。

```
git add .
```

このコマンドは、現在のディレクトリ内のすべてのファイルとディレクトリをステージングエリアに追加します。ステージングエリアとは、次にコミットされる変更を一時的に保存する場所です。このコマンドを実行することで、git にどのファイルが追跡され、コミットされるかを指示しています。

<div aria-hidden="true" class="wp-block-spacer" style="height:20px"></div>```
git commit -m "Initial commit with Flask setup"
```

このコマンドは、ステージングエリアに追加されたファイルのスナップショットを取り、ローカルリポジトリに保存します。`-m` オプションを使ってコミットメッセージを指定できます。ここでは「Initial commit with Flask setup」（Flask 設定を含む最初のコミット）としています。これにより、プロジェクトの現在の状態を保存し、将来的にこの状態に戻すことができます。

<div aria-hidden="true" class="wp-block-spacer" style="height:20px"></div>## <span class="ez-toc-section" id="%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E5%90%8D%E3%81%AE%E5%A4%89%E6%9B%B4"></span>ローカルブランチ名の変更<span class="ez-toc-section-end"></span>

デフォルトブランチ名を `master` から `main` に変更します。

```
git branch -M main
```

このコマンドは、現在のブランチの名前を `main` に変更します。`-M` オプションは強制的に名前を変更することを意味します。

<div aria-hidden="true" class="wp-block-spacer" style="height:20px"></div>## <span class="ez-toc-section" id="GitHub_%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AE%E4%BD%9C%E6%88%90"></span>GitHub リポジトリの作成<span class="ez-toc-section-end"></span>

次に、GitHub に新しいリポジトリを作成します。

1. [GitHub](https://github.com/) にログインします。
2. 右上のプラスアイコンをクリックし、「New repository」を選択します。
3. 「Repository name」には `my-new-project` と入力します。
4. 必要に応じて説明を追加し、リポジトリをパブリックまたはプライベートに設定します。
5. 「Create repository」ボタンをクリックします。

## <span class="ez-toc-section" id="%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AE%E8%BF%BD%E5%8A%A0"></span>リモートリポジトリの追加<span class="ez-toc-section-end"></span>

GitHub で作成したリポジトリをローカルリポジトリに追加します。

```
`git remote add origin https://github.com/username/my-new-project.git`
```

このコマンドを実行すると、ローカルリポジトリにリモートリポジトリが追加されます。`origin` はリモートリポジトリのデフォルト名であり、リモートリポジトリの URL を指定することで、ローカルの git リポジトリとリモートの GitHub リポジトリがリンクされます。これにより、ローカルでの変更をリモートにプッシュしたり、リモートから変更をプルしたりすることが可能になります。

## <span class="ez-toc-section" id="%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%B8%E3%81%AE%E3%83%97%E3%83%83%E3%82%B7%E3%83%A5"></span>リモートリポジトリへのプッシュ<span class="ez-toc-section-end"></span>

最後に、ローカルリポジトリの内容を GitHub にプッシュします。

```
`git push -u origin main`
```

このコマンドは、ローカルリポジトリの `main` ブランチの内容をリモートリポジトリの `main` ブランチにプッシュします。`-u` オプションを使う。

以上の手順で、新しいプロジェクトの立ち上げから GitHub へのプッシュまでを完了できます。この方法を使用することで、プロジェクトのバージョン管理が容易になり、チームでの共同作業もスムーズに進めることができます。

## <span class="ez-toc-section" id="%E6%B3%A8%E6%84%8F%E7%82%B9%E3%81%A8%E8%BF%B7%E3%81%A3%E3%81%9F%E3%81%A8%E3%81%8D%E3%81%AE%E5%AF%BE%E5%BF%9C"></span>注意点と迷ったときの対応<span class="ez-toc-section-end"></span>

- **仮想環境の利用**： 仮想環境を使うことで、プロジェクトごとの依存関係を管理しやすくなります。これにより、他のプロジェクトやシステム全体に影響を与えずに開発が進められます。
- **エラーメッセージの確認**： プロジェクトのセットアップ中にエラーが発生した場合、エラーメッセージを注意深く読み、必要な修正を行いましょう。エラーの内容を検索することで、多くの解決策が見つかります。
- **ドキュメントの参照**： Flask や git、GitHub の公式ドキュメントを参照することで、正確な情報を得ることができます。特に、新しい機能やベストプラクティスを学ぶためには、公式ドキュメントが最も信頼できるリソースです。
- **コミュニティへの参加**： オンラインフォーラムやコミュニティに参加することで、他の開発者からアドバイスを受けたり、問題を解決するためのヒントを得たりすることができます。

以上が新しいプロジェクトを立ち上げる際の基本的な手順と注意点です。これらのステップを踏むことで、効率的にプロジェクトを開始し、円滑に開発を進めることができるでしょう。お役に立てれば幸いです。

## <span class="ez-toc-section" id="%E5%8F%82%E8%80%83%E6%96%87%E7%8C%AE"></span>参考文献<span class="ez-toc-section-end"></span>

- [Git Documentation](https://git-scm.com/doc) （英語）
- [GitHub Docs](https://docs.github.com/)（日本語）
