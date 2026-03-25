# GEMINI.md

このファイルは Gemini CLI がグローバル設定として参照する指示書です。

## 参照するポリシー

以下のファイルを作業前に読み込んでください。

- [`policy/global.md`](policy/global.md) — 全AI共通ルール
- [`policy/master/00-principles.md`](policy/master/00-principles.md) — 環境・基本方針
- [`policy/master/10-platform-wsl.md`](policy/master/10-platform-wsl.md) — WSL固有ルール
- [`policy/master/20-safety.md`](policy/master/20-safety.md) — 安全ルール

## 設定ファイルの場所

| ファイル | 用途 |
|---|---|
| `~/.gemini/GEMINI.md` | Gemini CLI へのグローバル指示 |
| `~/.gemini/antigravity/` | Gemini CLI のキャッシュ・ワークスペース |

## ツール使用ルール

- シェルコマンドの実行は必要最小限にとどめる
- ファイル操作はツールが提供する専用機能を優先する
- 副作用のあるコマンド（インストール、削除、送信等）は実行前に確認する

## 確認が必要な操作

以下の操作はユーザーへの確認なしに実行しない。

- ファイルの削除・上書き
- `git push` などリモートへの反映
- 外部 API へのリクエスト
- システムパッケージのインストール（`apt install` 等）

## 応答スタイル

- 応答は明確・簡潔に
- 変更を提案する場合は「何をなぜ変更するか」を先に説明する
- 確信のない操作は実行せずユーザーに確認する

## セキュリティ

- 認証情報・APIキーをファイルや応答に含めない
- `~/.ssh/` や `~/.gnupg/` には絶対に触れない
- コマンドインジェクションとなりうる入力を処理する際は注意する
