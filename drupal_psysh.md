# Talking with Drupal

psyshでの対話型デバッグ


Tomotsugu Kaneko
[@snize](https://twitter.com/snize)<br>
kaneko@zerobase.jp<br>


ところで、Drupalのテーマ作成とかモジュール作るときの変数やメソッドの確認、つまりデバッグどうしてますか？


- Develモジュール
- プリントデバッグ(echo, var_dump...)
- Xdebug
- REPL
<!-- .element: class="fragment highlight-red" data-fragment-index="1" -->

僕は普段はXdebug派です
<!-- .element: class="fragment" data-fragment-index="2" -->


## REPL
Read-eval-print loop：読んで評価して表示を繰り返す


今日はPHPのREPL環境のひとつ、[PsySH](http://psysh.org/)のデモをします



## Drupalの準備


### Composerでプロジェクトの作成

必要なファイルのダウンロードと配置を以下のコマンドで行う

```
composer create-project drupal-composer/drupal-project:8.x-dev demo_drupal-psysh --stability dev --no-interaction
```

詳しくは：[Using Composer to manage Drupal site dependencies | Drupal.org](https://www.drupal.org/node/2718229)


### Drupalのインストール

Drupal ConsoleでのDBの作成とDrupalの初期設定の書き込み

```
drupal site:install
```

今日はここまで準備済み



## Demo

### 前提あるいは状況

今日はあまり**Drupal 8についての知識がない状態**で、テーマ開発を行う状況にあると思ってください。テーマファイルの`mytheme.theme`でTwigのに渡す変数を探している。


### ダミーのタクソノミータームを生成

drupal consoleで生成（便利！）

```
drupal create:terms tags
```

Note:
ここで新規ターミナルを開いて実際に生成しておく


## PsySH


## PsySHとDrushの関係

- Drushコアの機能 [^[drush/CliCommands.php at 226a7d4020630969ba9d48b3390e841b1ccbe758 · drush-ops/drush](https://github.com/drush-ops/drush/blob/226a7d4020630969ba9d48b3390e841b1ccbe758/src/Drupal/Commands/core/CliCommands.php)]
- [REPL (a custom shell for Drupal) - Drush docs](http://www.drush.org/en/master/repl/)

```
drush help core-cli
Open an interactive shell on a Drupal site.

Options:
 --version-history                         Use command history based on Drupal version (Default is per site).

Topics:
 docs-repl                                 repl.md

Aliases: php
```


### PsySHを起動

Drushコマンドから起動、Drushを経由してDrupalをブートストラップしてPsySHを起動するからPsySHからDrupalの機能が呼び出せるようになる

```
drush php
```

よく使うコマンド　`help`　, `ls -la`, `show`



## デモ中

### （おさらい）前提あるいは状況

今日はあまり**Drupal 8についての知識がない状態**で、テーマ開発を行う状況にあると思ってください。テーマファイルの`mytheme.theme`でTwigのに渡す変数を探している。

Note:
```
\Drupal::entityTypeManager()->getStorage('taxonomy_term')
$termStorage = \Drupal::entityTypeManager()->getStorage('taxonomy_term')
ls -la $termStorage
show $termStorage::loadTree
$termStorage->loadTree('tags')
$termStorage->loadTree('tags', 0, NULL, TRUE)
$term = $termStorage->loadTree('tags', 0, NULL, TRUE)[0]
$term->getName()
$term->url()
```

```
//start local site
drupal server
drupal user:login:url
```

```
// start rec
asciinema rec
```


## 以上です、ありがとうございました<br /> (｡･ω･｡)ﾉ

- このデモのリポジトリ [snize/demo_drupal-psysh](https://github.com/snize/demo_drupal-psysh)


### 過去の発表

- [CONFIGURATION MANAGEMENT WITH DRUPAL - Drupalでの構成管理](https://www.slideshare.net/snize/configuration-management-with-drupal)

### コンタクト

- [@snize](https://twitter.com/snize) ← フォローお願いします
- kaneko@zerobase.jp
