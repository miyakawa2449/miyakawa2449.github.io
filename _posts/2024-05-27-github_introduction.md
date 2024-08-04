---
id: 163
title: '初めてのGitHub: プログラマーが知っておくべきコツとトリック'
date: '2024-05-27T15:14:30+09:00'
author: '宮川　剛'
excerpt: Gitはバージョン管理システムとして非常に強力ですが、GitHubはそのGitを活用したコラボレーションプラットフォームです。GitHubを使うことで、チームメンバーと効率的に共同作業ができるだけでなく、オープンソースプロジェクトへの貢献やポートフォリオの公開なども簡単に行えます。本記事では、Gitを使ってプロジェクト管理をしていたプログラマーが初めてGitHubを利用する際の手順を詳しく解説します。
layout: post
guid: 'https://miyasols.com/?p=163'
permalink: /github/github_introduction/
image: /wp-content/uploads/2024/05/github.jpg
categories:
    - GitHub
---

Gitはバージョン管理システムとして非常に強力ですが、GitHubはそのGitを活用したコラボレーションプラットフォームです。GitHubを使うことで、チームメンバーと効率的に共同作業ができるだけでなく、オープンソースプロジェクトへの貢献やポートフォリオの公開なども簡単に行えます。本記事では、Gitを使ってプロジェクト管理をしていたプログラマーが初めてGitHubを利用する際の手順を詳しく解説します。

## <span class="ez-toc-section" id="GitHub%E3%82%A2%E3%82%AB%E3%82%A6%E3%83%B3%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90"></span>GitHubアカウントの作成<span class="ez-toc-section-end"></span>

まずはGitHubの公式サイトにアクセスし、アカウントを作成します。以下の手順を参考にしてください。

1. [GitHub公式サイト](https://github.com/)にアクセスし、「Sign up」をクリック。
2. 必要な情報（ユーザー名、メールアドレス、パスワード）を入力し、「Create account」をクリック。
3. アカウントが作成されたら、プロフィール写真や自己紹介文を設定します。これは他のユーザーとの交流を深めるための重要なステップです。

## <span class="ez-toc-section" id="%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AE%E4%BD%9C%E6%88%90"></span>リポジトリの作成<span class="ez-toc-section-end"></span>

GitHubにログイン後、新しいリポジトリを作成します。以下の手順に従ってください。

1. 画面右上の「+」アイコンをクリックし、「New repository」を選択。
2. リポジトリ名を入力し、必要に応じて説明文を追加します。
3. 「Public」または「Private」を選択し、「Create repository」をクリック。

## <span class="ez-toc-section" id="%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%A8GitHub%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%81%AE%E9%80%A3%E6%90%BA"></span>ローカルリポジトリとGitHubリポジトリの連携<span class="ez-toc-section-end"></span>

既存のGitプロジェクトをGitHubにアップロードするためには、リモートリポジトリを設定し、プロジェクトをプッシュします。

### <span class="ez-toc-section" id="1_%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%82%92%E8%BF%BD%E5%8A%A0"></span>1. リモートリポジトリを追加<span class="ez-toc-section-end"></span>

```
git remote add origin https://github.com/ユーザー名/リポジトリ名.git
```

### <span class="ez-toc-section" id="2_%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%81%AE%E5%90%8D%E5%89%8D%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B"></span>2. デフォルトブランチの名前を確認する<span class="ez-toc-section-end"></span>

Gitのバージョンが新しい場合、デフォルトブランチは「main」となっています。ローカルリポジトリのデフォルトブランチ名が「master」の場合、以下のコマンドで「main」に変更します

```
git branch -M main
```

注意事項: このコマンドは、現在チェックアウトされているブランチの名前を main に変更するためのものであり、他のリポジトリには影響を与えません。

### <span class="ez-toc-section" id="3_%E3%83%AA%E3%83%9D%E3%82%B8%E3%83%88%E3%83%AA%E3%82%92%E3%83%97%E3%83%83%E3%82%B7%E3%83%A5"></span>3. リポジトリをプッシュ<span class="ez-toc-section-end"></span>

```
git push -u origin main
```

## <span class="ez-toc-section" id="%E5%9F%BA%E6%9C%AC%E7%9A%84%E3%81%AA%E6%93%8D%E4%BD%9C"></span>基本的な操作<span class="ez-toc-section-end"></span>

GitHubでの基本操作には、クローン、プル、プッシュなどがあります。これらの操作を通じて、ローカルリポジトリとGitHubリポジトリ間でデータを同期します。

### <span class="ez-toc-section" id="%E3%82%AF%E3%83%AD%E3%83%BC%E3%83%B3"></span>クローン<span class="ez-toc-section-end"></span>

- 目的 
    - クローン操作は、GitHub上のリポジトリをローカル環境に複製するためのものです。
- メリット: 
    - GitHub上のプロジェクトを手元で自由に操作できるようになります。  
        自分の環境で変更を加えたり、新しい機能を開発したりできます。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95"></span>操作方法:<span class="ez-toc-section-end"></span>

```
git clone https://github.com/ユーザー名/リポジトリ名.git
```

---

### <span class="ez-toc-section" id="%E3%83%97%E3%83%AB"></span>プル<span class="ez-toc-section-end"></span>

- 目的 
    - プル操作は、リモートリポジトリ（GitHub）上の最新の変更をローカルリポジトリに反映させるためのものです。
- メリット 
    - 他の開発者が加えた変更を自分のローカル環境に取り込むことができます。  
        チーム全体のコードベースを最新の状態に保つことができます。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-2"></span>操作方法<span class="ez-toc-section-end"></span>

```
git pull origin main
```

---

### <span class="ez-toc-section" id="%E3%83%97%E3%83%83%E3%82%B7%E3%83%A5"></span>プッシュ<span class="ez-toc-section-end"></span>

- 目的 
    - プッシュ操作は、ローカルリポジトリの変更をリモートリポジトリ（GitHub）に反映させるためのものです。
- メリット 
    - 自分の変更をチームメンバーと共有できます。リモートリポジトリが最新の状態に保たれ、他のメンバーがその変更を取り込めるようになります。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-3"></span>操作方法<span class="ez-toc-section-end"></span>

```
git push origin main
```

---

### <span class="ez-toc-section" id="%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%81%AE%E4%BD%9C%E6%88%90"></span>ブランチの作成<span class="ez-toc-section-end"></span>

また、ブランチを作成して機能ごとに作業を分ける方法も説明します。

- 目的 
    - ブランチの作成は、新しい機能やバグ修正など、特定の作業を分離して行うためのものです。ブランチを使用することで、メインのコードベースに影響を与えずに作業を進めることができます。
- メリット 
    - 安全に新しい機能や変更を試すことができます。  
        複数の作業が並行して進行でき、コードの衝突を避けることができます。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-4"></span>操作方法<span class="ez-toc-section-end"></span>

```
git checkout -b新しいブランチ名
```

### <span class="ez-toc-section" id="%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%81%AE%E3%83%9E%E3%83%BC%E3%82%B8"></span>ブランチのマージ<span class="ez-toc-section-end"></span>

- 目的 
    - ブランチのマージは、作成したブランチで行った変更をメインのブランチに統合するためのものです。作業が完了したら、その変更を他のチームメンバーと共有するためにマージします。
- メリット 
    - 新しい機能やバグ修正をメインのコードベースに統合できます。  
        チーム全体でコードの一貫性を保ち、全員が最新の変更を利用できます。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-5"></span>操作方法<span class="ez-toc-section-end"></span>

```
git checkout main
git merge 新しいブランチ名
```

## <span class="ez-toc-section" id="%E3%82%B3%E3%83%A9%E3%83%9C%E3%83%AC%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E6%A9%9F%E8%83%BD"></span>コラボレーション機能<span class="ez-toc-section-end"></span>

GitHubの強力なコラボレーション機能には、プルリクエスト、Issues、Projectsがあります。それぞれの機能の目的とメリットを以下に説明します。

### <span class="ez-toc-section" id="%E3%83%97%E3%83%AB%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88"></span>プルリクエスト<span class="ez-toc-section-end"></span>

- 目的 
    - プルリクエストは、他の開発者に対して変更のレビューとマージを依頼するための機能です。これにより、コードの品質を保ちながら複数の開発者が共同で作業することができます。
- メリット 
    - コードレビューを通じて、バグの早期発見やコード品質の向上が図れます。
    - フィードバックを受けることで、チーム全体のスキルアップが期待できます。
    - 変更内容をドキュメントとして残すことで、将来的な参照が容易になります。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-6"></span>操作方法<span class="ez-toc-section-end"></span>

1. リポジトリのページで「Pull requests」タブをクリック。
2. 「New pull request」をクリックし、変更を確認。
3. 「Create pull request」をクリックし、詳細を入力。

### <span class="ez-toc-section" id="Issues"></span>Issues<span class="ez-toc-section-end"></span>

- 目的 
    - Issuesは、バグ報告や機能追加のリクエスト、タスクのトラッキングなど、プロジェクト管理に役立つ機能です。
- メリット 
    - プロジェクトの課題や進行状況を整理し、可視化できます。  
        チームメンバー間でのコミュニケーションが円滑になります。  
        作業の優先順位付けがしやすくなります。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-7"></span>操作方法<span class="ez-toc-section-end"></span>

1. リポジトリのページで「Issues」タブをクリック。
2. 「New issue」をクリックし、詳細を入力。

### <span class="ez-toc-section" id="Projects"></span>Projects<span class="ez-toc-section-end"></span>

- 目的 
    - Projectsは、カンバンボード形式でタスクを管理するための機能です。プロジェクト全体の進行状況を視覚的に把握しやすくなります。
- メリット 
    - タスクのステータス（To do、In progress、Doneなど）を一目で確認できます。
    - チーム全体の進捗状況を管理しやすくなります。
    - 効率的なプロジェクトマネジメントが可能になります。

#### <span class="ez-toc-section" id="%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95-8"></span>操作方法<span class="ez-toc-section-end"></span>

1. リポジトリのページで「Projects」タブをクリック。
2. 「New project」をクリックし、プロジェクトボードを作成。

## <span class="ez-toc-section" id="%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E3%81%A8%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9"></span>セキュリティとベストプラクティス<span class="ez-toc-section-end"></span>

GitHubを利用する際には、セキュリティとベストプラクティスを遵守することが非常に重要です。プロジェクトの安全性を確保し、チーム全体の効率的な作業環境を維持するために、以下の点に注意してください。

### <span class="ez-toc-section" id="%E3%82%A2%E3%82%AF%E3%82%BB%E3%82%B9%E6%A8%A9%E9%99%90%E3%81%AE%E7%AE%A1%E7%90%86"></span>アクセス権限の管理<span class="ez-toc-section-end"></span>

リポジトリのアクセス権限は、メンバーの役割や責任に応じて適切に設定しましょう。例えば、リポジトリの管理者は全ての設定変更が可能ですが、開発者はコードのプッシュやプルリクエストの作成のみを許可するなど、権限を分けることができます。

機密プロジェクトでは、リポジトリをプライベートに設定し、アクセス権を限られたメンバーのみに付与します。また、新しいメンバーが加わる際には、最小限の権限からスタートし、信頼関係が築かれたら必要に応じて権限を拡大することが推奨されます。

---

### <span class="ez-toc-section" id="%E7%A7%98%E5%AF%86%E6%83%85%E5%A0%B1%E3%81%AE%E5%8F%96%E3%82%8A%E6%89%B1%E3%81%84"></span>秘密情報の取り扱い<span class="ez-toc-section-end"></span>

APIキーやパスワードなどの機密情報は、リポジトリに含めないようにしましょう。これらの情報は環境変数や秘密管理サービスを利用して管理するのが一般的です。

具体例: .envファイルを使用して、APIキーやデータベースのパスワードを管理します。このファイルは.gitignoreに追加して、リポジトリにコミットされないようにします。また、GitHub Secretsを利用して、GitHub Actionsで必要な機密情報を安全に管理することも可能です。

---

### <span class="ez-toc-section" id="%E3%82%B3%E3%83%BC%E3%83%89%E3%83%AC%E3%83%93%E3%83%A5%E3%83%BC%E3%81%A8%E3%83%97%E3%83%AB%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%81%AE%E6%B4%BB%E7%94%A8"></span>コードレビューとプルリクエストの活用<span class="ez-toc-section-end"></span>

プルリクエストを通じたコードレビューは、セキュリティの確保と品質向上に役立ちます。全てのコード変更は、少なくとも1人以上のレビューを受けるようにしましょう。

具体例: 大規模なプロジェクトでは、特にセキュリティが重要な部分のコード変更について、セキュリティ専門のメンバーによるレビューを必須とするポリシーを導入します。これにより、潜在的な脆弱性を早期に発見し、対策を講じることができます。

---

### <span class="ez-toc-section" id="%E5%AE%9A%E6%9C%9F%E7%9A%84%E3%81%AA%E3%82%BB%E3%82%AD%E3%83%A5%E3%83%AA%E3%83%86%E3%82%A3%E7%9B%A3%E6%9F%BB"></span>定期的なセキュリティ監査<span class="ez-toc-section-end"></span>

リポジトリのセキュリティを維持するために、定期的にセキュリティ監査を実施しましょう。GitHubのセキュリティ機能を活用して、依存関係の脆弱性をチェックし、問題が発見された場合は速やかに対応します。

具体例: GitHubのDependabotアラートを有効にし、依存パッケージの脆弱性を自動的に検出します。また、定期的にリポジトリの設定を見直し、不必要なアクセス権が付与されていないか確認することも重要です。

---

### <span class="ez-toc-section" id="%E3%83%90%E3%83%83%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E3%81%A8%E3%83%AA%E3%82%AB%E3%83%90%E3%83%AA"></span>バックアップとリカバリ<span class="ez-toc-section-end"></span>

万が一のデータ損失に備えて、定期的にリポジトリのバックアップを行いましょう。GitHubは高い信頼性を提供していますが、独自のバックアップを持つことでさらに安心です。

具体例: GitHubから定期的にリポジトリをクローンし、別の安全な場所にバックアップを保存します。また、重要なリリースごとにタグを付けておくことで、特定のバージョンに容易に戻れるようにします。

## <span class="ez-toc-section" id="%E5%AD%A6%E3%82%93%E3%81%A0%E3%81%93%E3%81%A8%E3%81%AE%E3%81%BE%E3%81%A8%E3%82%81"></span>学んだことのまとめ<span class="ez-toc-section-end"></span>

本記事では、GitHubを初めて利用するプログラマー向けに、以下の5つの主要なテーマについて解説しました。

リポジトリの登録  
GitHubアカウントの作成から、新しいリポジトリの作成方法までを学びました。リポジトリはプロジェクトのバージョン管理とコラボレーションの中心となる場所です。

クローン・プル・プッシュの基本操作  
クローン: GitHub上のリポジトリをローカル環境に複製する操作です。これにより、自分のPC上でリポジトリを操作できます。  
プル: リモートリポジトリの最新の変更をローカルリポジトリに反映する操作です。チームの最新コードを常に保持できます。  
プッシュ: ローカルリポジトリの変更をリモートリポジトリに反映する操作です。これにより、チーム全体と自分の変更を共有できます。

3. ブランチを切る理由  
    ブランチは、新しい機能やバグ修正など、特定の作業を分離して行うためのものです。ブランチを使用することで、メインのコードベースに影響を与えずに作業を進めることができ、安全に新しい機能を試すことができます。作業が完了したら、変更をメインブランチにマージして共有します。

コラボレーション機能  
GitHubのプルリクエスト、Issues、Projectsなどのコラボレーション機能について学びました。

プルリクエスト: コードの変更をレビューし、チームメンバーと共有するための機能です。  
Issues: バグ報告や機能リクエスト、タスクのトラッキングに役立つ機能です。  
Projects: カンバンボード形式でタスクを視覚的に管理できる機能です。  
セキュリティとベストプラクティス  
リポジトリのアクセス権限の管理や秘密情報の適切な取り扱いについて学びました。これにより、プロジェクトのセキュリティを確保し、チーム全体の作業を安全かつ効率的に進めることができます。
