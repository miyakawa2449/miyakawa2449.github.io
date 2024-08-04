---
id: 137
title: 'CentOS 9でVPSサーバー間バックアップをrsyncで完全自動化する方法'
date: '2024-05-21T17:58:57+09:00'
author: '宮川　剛'
layout: post
guid: 'https://miyasols.com/?p=137'
permalink: /server/rsync_remote_backup/
image: /wp-content/uploads/2024/05/rsync.jpg
categories:
    - Server
---

こんにちは！今回は、CentOS 9でVPSサーバー間のバックアップを自動化する方法について解説します。この記事は、rsyncを使ってリモートサーバーに手動でバックアップを覚えたばかりの初心者エンジニアの方に向けています。

手動でバックアップを行う場合、バックアップディレクトリが増えると手間がかかり、パスフレーズを何度も入力することの不便さに悩まされることがあります。この記事では、これらの問題を解決するために、rsyncを使ってサーバー間でバックアップを自動化する方法をステップバイステップでご紹介します。

バックアップはサーバー運用において非常に重要な部分です。特に、新しく構築したVPSサーバーのデータを保護するために、効率的で確実なバックアップ方法を知りたいと考えている方にとって、このガイドは役立つでしょう。これから、手間を省きつつ安全にデータを保護するための手順を詳しく説明していきます。

### 前提条件

- **SSH鍵認証の設定**: 
    - バックアップ元サーバとバックアップ先サーバの間でSSH鍵認証が設定されていること。
    - バックアップ元サーバのユーザーのホームディレクトリにSSH秘密鍵が配置されていること。
    - バックアップ先サーバのユーザーのホームディレクトリに公開鍵が配置され、適切な権限が設定されていること。
- **バックアップ先サーバのディレクトリ構造**: 
    - バックアップ先サーバに必要なバックアップディレクトリが用意されていること。
    - 例えば、以下のようなディレクトリ構造を事前に作成しておきます。

```
backup/etc/
backup/home/
backup/www/
backup/mysql/
backup/log/
```

- **rsyncのインストールと設定**: 
    - バックアップ元サーバおよびバックアップ先サーバに`rsync`がインストールされていること。
    - 両方のサーバで`rsync`の動作確認が完了していること。

### ステップ1：バックアップリストの作成

まず、バックアップ対象のディレクトリとリモートサーバのバックアップ先ディレクトリを指定するリストを作成します。

#### `/usr/local/bin/backup_list.txt`

```
`/etc user@remote-server:/backup/etc/home user@remote-server:/backup/home/var/www user@remote-server:/backup/www/var/lib/mysql user@remote-server:/backup/mysql/var/log user@remote-server:/backup/log`
```

### ステップ2：バックアップスクリプトの作成

次に、バックアップリストを読み込み、`rsync`を使ってバックアップを行うスクリプトを作成します。

#### `/usr/local/bin/backup.sh`

```
`#!/bin/bash# バックアップリストファイルBACKUP_LIST="/usr/local/bin/backup_list.txt"LOG_FILE="/var/log/backup.log"SSH_KEY="/home/user/.ssh/id_rsa"# バックアップリストを読み込みwhile IFS=" " read -r SOURCE_DIR DEST_DIR; do    # ディレクトリが存在するか確認    if [[ -d $SOURCE_DIR ]]; then        # バックアップを実行        rsync -avz --delete -e "ssh -i $SSH_KEY" $SOURCE_DIR $DEST_DIR >> $LOG_FILE 2>&1    else        echo "Warning: $SOURCE_DIR does not exist, skipping..." >> $LOG_FILE    fidone < $BACKUP_LIST`
```

### ステップ3：SSHエージェントの設定スクリプトの作成

SSHエージェントを起動し、パスフレーズを入力してSSHキーを追加するスクリプトを作成します。

#### `/usr/local/bin/start_ssh_agent.sh`

```
`#!/bin/bash# SSHエージェントを起動eval "$(ssh-agent -s)"# パスフレーズを使用してSSHキーを追加/usr/local/bin/add_ssh_key.expect# エージェントの環境変数をエクスポートしてbackup.shを実行export SSH_AUTH_SOCKexport SSH_AGENT_PID/usr/local/bin/backup.sh`
```

### ステップ4：パスフレーズを自動入力する`expect`スクリプトの作成

`expect`を使ってパスフレーズを自動的に入力するスクリプトを作成します。ここでの`\r`は改行（送信）を含める意味です。

#### `/usr/local/bin/add_ssh_key.expect`

```
`#!/usr/bin/expect -fspawn ssh-add /home/user/.ssh/id_rsaexpect "Enter passphrase for /home/user/.ssh/id_rsa:"send "dummy_passphrase\r"  # \rは改行（送信）を含める意味ですinteract`
```

### ステップ5：スクリプトのパーミッション設定

作成したスクリプトに実行権限を設定します。

```
`sudo chmod 700 /usr/local/bin/start_ssh_agent.shsudo chown root:root /usr/local/bin/start_ssh_agent.shsudo chmod 700 /usr/local/bin/add_ssh_key.expectsudo chown root:root /usr/local/bin/add_ssh_key.expectsudo chmod 700 /usr/local/bin/backup.shsudo chown root:root /usr/local/bin/backup.sh`
```

### ステップ6：手動でスクリプトをテスト

手動で`start_ssh_agent.sh`スクリプトを実行して、正しく動作するか確認します。

```
`sudo /usr/local/bin/start_ssh_agent.sh`
```

### ステップ7：cronジョブの設定

スクリプトが正常に動作することを確認した後、cronジョブを設定します。まずは17時にテストするために、以下のように設定します。

```
`sudo crontab -e`
```

以下の行を追加します。

```
`0 17 * * * /usr/local/bin/start_ssh_agent.sh`
```

### ステップ8：テスト完了後の設定変更

テストが完了したら、必要に応じて設定を元に戻し、定期的に実行されるようにします。例えば、毎日午前2時に実行する場合、以下のように設定します。

```
`sudo crontab -e`
```

以下の行を追加します。

```
`0 2 * * * /usr/local/bin/start_ssh_agent.sh`
```

### バックアップ結果の確認

バックアップ先にデータが正しくコピーされているかを確認します。例えば、リモートサーバ上のバックアップディレクトリを確認します。

```
`ssh -i /home/user/.ssh/id_rsa user@remote-server "ls /backup/www"`
```

### まとめ

これで、CentOS 9でVPSサーバー間のバックアップを自動化する設定が完了しました。rsyncを使ったバックアップの自動化は、データの保護にとても役立ちます。お試し期間中に設定を行い、安心して運用できる環境を整えてください。
