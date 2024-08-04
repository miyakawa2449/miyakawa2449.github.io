---
id: 180
title: GitHubでのブランチ活用術：安全にコードを改修する方法
date: '2024-05-28T19:31:50+09:00'
author: '宮川　剛'
layout: post
guid: 'https://miyasols.com/?p=180'
permalink: /github/github_branch/
image: /wp-content/uploads/2024/05/github_branch.jpg
categories:
    - GitHub
---

こんにちは！GitHub初心者の皆さん、今日はプロジェクトに参加している場合でも、自分のプロジェクトに対しても安全に機能追加や改修を行う方法についてお話しします。

動いているプログラムをいきなり変更するのはリスクが伴いますよね。そんなときに役立つのが、GitHubのブランチ機能です。

ブランチを活用すれば、メインのプログラムに影響を与えることなく、安全に新しい機能を追加したり、バグを修正したりすることができます。

## <span class="ez-toc-section" id="GitHub%E3%81%A7%E3%81%AE%E6%A9%9F%E8%83%BD%E8%BF%BD%E5%8A%A0%E4%BD%9C%E6%A5%AD%E3%81%AE%E6%B5%81%E3%82%8C"></span>GitHubでの機能追加作業の流れ<span class="ez-toc-section-end"></span>

### <span class="ez-toc-section" id="%E6%96%B0%E3%81%97%E3%81%84%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%82%92%E4%BD%9C%E6%88%90"></span>新しいブランチを作成<span class="ez-toc-section-end"></span>

まずは、新しい機能を追加するために新しいブランチを作成します。ブランチ名は `feature/` プレフィックスを使うことが一般的です。

```
`git checkout -b feature/new-feature`
```

### <span class="ez-toc-section" id="%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%81%A7%E4%BD%9C%E6%A5%AD%E3%81%99%E3%82%8B"></span>ブランチで作業する<span class="ez-toc-section-end"></span>

作成したブランチでコードを改編し、変更をコミットします。

```
# ファイルを編集後
`git add .git commit -m "Add new feature"`
```

### <span class="ez-toc-section" id="%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AB%E3%83%97%E3%83%83%E3%82%B7%E3%83%A5"></span>リモートリポジトリにプッシュ<span class="ez-toc-section-end"></span>

変更をリモートリポジトリにプッシュします。

```
`git push origin feature/new-feature`
```

### <span class="ez-toc-section" id="%E3%83%97%E3%83%AB%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88_Pull_Request_%E3%82%92%E4%BD%9C%E6%88%90"></span>プルリクエスト (Pull Request) を作成<span class="ez-toc-section-end"></span>

GitHub上でプルリクエストを作成し、変更をメインブランチにマージするようにリクエストします。

1. GitHubのリポジトリページにアクセス
2. `Pull requests` タブをクリック
3. `New pull request` ボタンをクリック
4. `base` ブランチに `main`（または `develop` など）、`compare` ブランチに `feature/new-feature` を選択
5. プルリクエストのタイトルと説明を記入して作成

### <span class="ez-toc-section" id="%E3%82%B3%E3%83%BC%E3%83%89%E3%83%AC%E3%83%93%E3%83%A5%E3%83%BC%E3%81%A8%E3%83%86%E3%82%B9%E3%83%88"></span>コードレビューとテスト<span class="ez-toc-section-end"></span>

プルリクエストを通じて他の開発者にコードレビューを依頼し、必要な修正を行います。自動テストも含めて、テストを行います。

### <span class="ez-toc-section" id="%E3%83%9E%E3%83%BC%E3%82%B8"></span>マージ<span class="ez-toc-section-end"></span>

コードレビューとテストが完了したら、プルリクエストをマージします。

1. プルリクエストページで `Merge pull request` ボタンをクリック
2. 必要に応じて、マージメソッド（`Create a merge commit`、`Squash and merge`、`Rebase and merge`）を選択

### <span class="ez-toc-section" id="%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%81%AE%E3%83%A1%E3%82%A4%E3%83%B3%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%82%92%E6%9B%B4%E6%96%B0"></span>ローカルのメインブランチを更新<span class="ez-toc-section-end"></span>

マージ後、ローカルのメインブランチを最新の状態に更新します。

#### <span class="ez-toc-section" id="%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AE%E8%AA%AC%E6%98%8E"></span>コマンドの説明<span class="ez-toc-section-end"></span>

```
`git checkout main`
```

このコマンドは、ローカルリポジトリの `main` ブランチに切り替えます。これにより、現在の作業ブランチから `main` ブランチに戻ることができます。

```
`git pull origin main`
```

このコマンドは、リモートリポジトリ（`origin`）の `main` ブランチの最新の変更をローカルリポジトリに取り込む（取得して統合する）ためのものです。これにより、ローカルの `main` ブランチがリモートの最新の状態と同期されます。

---

## <span class="ez-toc-section" id="%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E5%91%BD%E5%90%8D%E3%81%AE%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9"></span>ブランチ命名のベストプラクティス<span class="ez-toc-section-end"></span>

### <span class="ez-toc-section" id="%E4%B8%80%E8%88%AC%E7%9A%84%E3%81%AA%E6%A9%9F%E8%83%BD%E8%BF%BD%E5%8A%A0%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E5%90%8D%E3%81%AE%E4%BE%8B"></span>一般的な機能追加ブランチ名の例<span class="ez-toc-section-end"></span>

以下のような命名形式がよく使われます：

- `feature/new-feature`
- `feature/add-user-authentication`
- `feature/update-dashboard-ui`

### <span class="ez-toc-section" id="%E5%85%B7%E4%BD%93%E4%BE%8B"></span>具体例<span class="ez-toc-section-end"></span>

例えば、新しい認証機能を追加する場合のブランチ名：

```
`git checkout -b feature/add-authentication`
```

ユーザーインターフェースを更新する場合のブランチ名：

```
`git checkout -b feature/update-ui`
```

### <span class="ez-toc-section" id="%E4%B8%80%E8%88%AC%E7%9A%84%E3%81%AA%E5%91%BD%E5%90%8D%E8%A6%8F%E5%89%87"></span>一般的な命名規則<span class="ez-toc-section-end"></span>

- **`feature/` プレフィックス**: 機能追加であることを明示するために使います。
- **説明的な名前**: 機能の内容を簡潔に説明する名前を付けます。

### <span class="ez-toc-section" id="%E3%81%9D%E3%81%AE%E4%BB%96%E3%81%AE%E5%91%BD%E5%90%8D%E8%A6%8F%E5%89%87"></span>その他の命名規則<span class="ez-toc-section-end"></span>

- **バグ修正**: `bugfix/` を使う (`bugfix/fix-login-issue`)
- **リリース準備**: `release/` を使う (`release/v1.2.0`)
- **緊急修正**: `hotfix/` を使う (`hotfix/urgent-security-patch`)

### <span class="ez-toc-section" id="%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%9E%E3%82%A4%E3%82%BA%E3%81%AE%E4%BE%8B"></span>カスタマイズの例<span class="ez-toc-section-end"></span>

特定のプロジェクトやチームで独自の命名規則を持つことも可能です。例えば、`add/` や `update/` を使うこともできますが、チーム全体で統一した命名規則を決めると良いでしょう。

```
`# 機能追加を明示するために、チームで統一した規則を使用git checkout -b feature/add-new-feature`
```

このようにすることで、ブランチ名が一貫性を持ち、他の開発者にもわかりやすくなります。

---

## <span class="ez-toc-section" id="%E3%81%BE%E3%81%A8%E3%82%81"></span>まとめ<span class="ez-toc-section-end"></span>

ブランチを活用することで、動いているプログラムに直接影響を与えることなく、安全に新しい機能を追加したり、バグを修正したりすることができます。プルリクエストを使って他の開発者にコードレビューを依頼し、テストを通じて変更を確認することで、プロジェクトの品質を保ちながら効率的に作業を進めることができます。ぜひ、今回ご紹介した方法を活用して、GitHubでの開発をより安全かつ効果的に進めてくださいね！
