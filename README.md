# Talking with Drupal

## スライド

[Talking with Drupal - Drupalと話そう！](https://snize.github.io/demo_drupal-psysh/#/)

## 準備

このリポジトリをクローンまたは[ダウンロード](https://github.com/snize/demo_drupal-psysh/archive/master.zip)

```
git clone git@github.com:snize/demo_drupal-psysh.git
```

### ダウンロードしたディレクトリへ移動し、Composerで必要なコードとツールをダウンロード

composerがインストールされていない場合は要インストール

```
cd demo_drupal-psysh
composer install
```

### Drupalのインストール

Drupal ConsoleでのDBの作成とDrupalの初期設定の書き込み

```
./vendor/bin/drupal site:install
```

[![asciicast](https://asciinema.org/a/exx27odHNEiVi9hys0nqnf4kB.png)](https://asciinema.org/a/exx27odHNEiVi9hys0nqnf4kB)

### ダミーのタクソノミータームを生成

```
./vendor/bin/drupal create:terms tags --limit="25" --name-words="5"
```

### PsySHの起動

```
./vendor/bin/drush php
```