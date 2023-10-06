# Zenn CLI

- [📘 How to use](https://zenn.dev/zenn/articles/zenn-cli-guide)

## コマンドチートシート

| コマンド | 説明 |
| --- | --- |
| `npx zenn new:article` | Markdownファイルを作成します。作成されたファイルには記事の設定（Front Matter）が含まれています。 |
| `npx zenn new:article --slug 記事のスラッグ --title タイトル --type idea --emoji ✨` | コマンド実行時に記事の Front Matter をオプションで指定して記事を作成します。 |
| `npx zenn preview` | ブラウザでプレビューを開始します。 |
| `npx zenn new:book` | 本の雛形を作成します。 |
| `npx zenn new:book --slug ここにスラッグ` | スラッグを指定して本の雛形を作成します。 |

## 記事の設定

| 設定項目 | 説明 |
| --- | --- |
| `title` | 記事のタイトルを指定します。 |
| `emoji` | アイキャッチとして使われる絵文字を指定します（1文字だけ）。 |
| `type` | 記事のタイプを指定します（"tech"は技術記事、"idea"はアイデア記事）。 |
| `topics` | タグを指定します（例：["markdown", "rust", "aws"]）。 |
| `published` | 公開設定を指定します（falseにすると下書き）。 |

## 本の設定

| 設定項目 | 説明 |
| --- | --- |
| `title` | 本のタイトルを指定します。 |
| `summary` | 本の紹介文を指定します。 |
| `topics` | トピック（タグ）を5つまで指定します。 |
| `published` | 公開する場合はtrueにします。 |
| `price` | 本の価格を指定します（200〜5000の間で100円単位）。 |
| `chapters` | チャプターの並び順を配列で指定します。 |
| `toc_depth` | 目次の深さを指定します（0〜3の範囲）。 |


