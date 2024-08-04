---
id: 60
title: WordPressの魔法：子テーマで安全にサイトをカスタマイズする方法
date: '2024-05-20T13:11:48+09:00'
author: '宮川　剛'
layout: post
guid: 'https://miyasols.com/?p=60'
permalink: /wordpress/childtheme-functions/
image: /wp-content/uploads/2024/05/DALL·E-2024-05-20-22.20.28-A-visually-appealing-image-representing-a-WordPress-blog-with-the-title-WordPressの魔法：子テーマで安全にサイトをカスタマイズする方法-in-both-English-and-Japanese.-The-image-.webp
categories:
    - WordPress
---

WordPressサイトを運営していると、カスタマイズしたい部分が多々出てきます。しかし、直接テーマのファイルを変更すると、テーマのアップデート時にカスタマイズが失われてしまう可能性があります。そこで登場するのが「子テーマ」です。子テーマを使うことで、親テーマの更新に影響されずに独自のカスタマイズを維持できます。

この記事では、親テーマ「Twenty Twenty-Four」に対する子テーマを作成する方法を詳しく解説します。


子テーマを作成する主な理由は以下の通りです：

1. **テーマのアップデートを安全に行うため**： 親テーマのアップデートがあっても、子テーマに加えたカスタマイズはそのまま残ります。
2. **親テーマの機能を拡張するため**： 親テーマの機能を変更したり、新しい機能を追加したりできます。
3. **テーマのデバッグやテストを行うため**： 子テーマを使って新しいカスタマイズをテストすることで、親テーマを直接変更するリスクを避けられます。

## <span class="ez-toc-section" id="Step_1_%E5%AD%90%E3%83%86%E3%83%BC%E3%83%9E%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E3%81%AE%E4%BD%9C%E6%88%90"></span>Step 1: 子テーマディレクトリの作成<span class="ez-toc-section-end"></span>

親テーマのディレクトリは `/var/www/wordpress/wp-content/themes/twentytwentyfour` です。まず、子テーマ用のディレクトリを作成します。

```
`mkdir /var/www/wordpress/wp-content/themes/twentytwentyfour-child`
```

## <span class="ez-toc-section" id="Step_2_%E5%AD%90%E3%83%86%E3%83%BC%E3%83%9E%E3%81%AE%E3%82%B9%E3%82%BF%E3%82%A4%E3%83%AB%E3%82%B7%E3%83%BC%E3%83%88_stylecss_%E3%81%AE%E4%BD%9C%E6%88%90"></span>Step 2: 子テーマのスタイルシート (style.css) の作成<span class="ez-toc-section-end"></span>

子テーマのディレクトリに `style.css` ファイルを作成します。

```
`vim /var/www/wordpress/wp-content/themes/twentytwentyfour-child/style.css`
```

以下の内容を `style.css` に追加します。

```
`/* Theme Name:   Twenty Twenty-Four Child Theme URI:    https://example.com/twentytwentyfour-child Description:  Twenty Twenty-Fourの子テーマ Author:       あなたの名前 Author URI:   https://example.com Template:     twentytwentyfour Version:      1.0.0*//* 親テーマのスタイルをインポート */@import url("../twentytwentyfour/style.css");/* ここにカスタムスタイルを追加 */`
```

## <span class="ez-toc-section" id="Step_3_%E5%AD%90%E3%83%86%E3%83%BC%E3%83%9E%E3%81%AE_functionsphp_%E3%81%AE%E4%BD%9C%E6%88%90"></span>Step 3: 子テーマの functions.php の作成<span class="ez-toc-section-end"></span>

次に、子テーマのディレクトリに `functions.php` ファイルを作成します。

```
`vim /var/www/wordpress/wp-content/themes/twentytwentyfour-child/functions.php`
```

以下の内容を `functions.php` に追加します。

```
`<?php// 親テーマのスタイルを読み込むfunction twentytwentyfour_child_enqueue_styles() {    wp_enqueue_style('parent-style', get_template_directory_uri() . '/style.css');}add_action('wp_enqueue_scripts', 'twentytwentyfour_child_enqueue_styles');?>`
```

### <span class="ez-toc-section" id="functionsphp_%E3%81%AE%E4%B8%AD%E8%BA%AB%E3%81%AE%E8%A7%A3%E8%AA%AC"></span>functions.php の中身の解説<span class="ez-toc-section-end"></span>

- **`twentytwentyfour_child_enqueue_styles` 関数**: この関数は、親テーマのスタイルシートを子テーマに読み込むためのものです。`wp_enqueue_style` 関数を使って、親テーマのスタイルシートをキューに追加します。
- **`add_action`**: `add_action` は、特定のイベント（この場合は `wp_enqueue_scripts` イベント）が発生したときに指定された関数（`twentytwentyfour_child_enqueue_styles`）を実行します。

### <span class="ez-toc-section" id="functionsphp_%E3%81%AB%E6%A9%9F%E8%83%BD%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B%E4%BE%8B"></span>functions.php に機能を追加する例<span class="ez-toc-section-end"></span>

`functions.php` にさらに機能を追加することで、子テーマのカスタマイズを強化できます。例えば、カスタムウィジェットエリアを追加するコードを紹介します。

```
`<?php// 親テーマのスタイルを読み込むfunction twentytwentyfour_child_enqueue_styles() {    wp_enqueue_style('parent-style', get_template_directory_uri() . '/style.css');}add_action('wp_enqueue_scripts', 'twentytwentyfour_child_enqueue_styles');// カスタムウィジェットエリアを追加function twentytwentyfour_child_widgets_init() {    register_sidebar(array(        'name'          => __('Custom Widget Area', 'twentytwentyfour-child'),        'id'            => 'custom-widget-area',        'before_widget' => '<div class="custom-widget">',        'after_widget'  => '</div>',        'before_title'  => '<h2 class="widget-title">',        'after_title'   => '</h2>',    ));}add_action('widgets_init', 'twentytwentyfour_child_widgets_init');?>`
```

この例では、`widgets_init` アクションにカスタムウィジェットエリアを登録する関数を追加しています。

## <span class="ez-toc-section" id="Step_4_%E3%83%91%E3%83%BC%E3%83%9F%E3%83%83%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AE%E8%AA%BF%E6%95%B4"></span>Step 4: パーミッションの調整<span class="ez-toc-section-end"></span>

`wordpress`ユーザーが新しい子テーマディレクトリとそのファイルにアクセスできるように、適切なパーミッションを設定します。

```
`chown -R wordpress:wordpress /var/www/wordpress/wp-content/themes/twentytwentyfour-childchmod -R 755 /var/www/wordpress/wp-content/themes/twentytwentyfour-child`
```

## <span class="ez-toc-section" id="Step_5_%E5%AD%90%E3%83%86%E3%83%BC%E3%83%9E%E3%81%AE%E6%9C%89%E5%8A%B9%E5%8C%96"></span>Step 5: 子テーマの有効化<span class="ez-toc-section-end"></span>

WordPressの管理画面にログインし、以下の手順で子テーマを有効化します。

1. **外観** &gt; **テーマ** に移動します。
2. 新しく作成した「Twenty Twenty-Four Child」テーマが一覧に表示されていることを確認します。
3. 「Twenty Twenty-Four Child」テーマをクリックし、「有効化」ボタンをクリックします。

## <span class="ez-toc-section" id="%E3%81%BE%E3%81%A8%E3%82%81"></span>まとめ<span class="ez-toc-section-end"></span>

子テーマを作成することで、親テーマのアップデートによるカスタマイズの消失を防ぎ、安心してサイトをカスタマイズできます。この記事の手順に従って、簡単に子テーマを作成し、WordPressサイトを思い通りにカスタマイズしましょう。

---

このガイドを参考にして、WordPressサイトのカスタマイズを安全に楽しんでください。
