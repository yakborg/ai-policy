# CLAUDE.md

このファイルは Claude Code が ai-policy リポジトリを操作する際に参照する指示書です。

## 参照するポリシー

以下のファイルを必ず読み込んでから作業を開始してください。

### 全AI共通ルール

- [`policy/global.md`](policy/global.md) — 回答スタイル・環境概要・禁止事項

### 共通ルール（すべてのエージェント共通）

- [`policy/master/00-principles.md`](policy/master/00-principles.md) — シェル・ランタイム・ツール管理の基本方針
- [`policy/master/10-platform-wsl.md`](policy/master/10-platform-wsl.md) — WSL 固有のパス・設定ルール
- [`policy/master/20-safety.md`](policy/master/20-safety.md) — 編集前確認・禁止操作・ツール追加ルール

### Claude Code 固有ルール

- [`claude/agents/orchestrator.md`](claude/agents/orchestrator.md) — 自律実行・Subagent起動・並列worktreeルール

## Claude Code 固有ルール（インライン）

### ツール使用の優先順位

専用ツールが存在する場合は Bash コマンドより専用ツールを優先する。

| 操作 | 優先ツール | Bash は使わない例 |
|---|---|---|
| ファイル読み取り | `Read` | `cat`, `head`, `tail` |
| ファイル編集 | `Edit` | `sed`, `awk` |
| ファイル作成 | `Write` | `echo >`, `cat <<EOF` |
| ファイル検索 | `Glob` | `find`, `ls` |
| 内容検索 | `Grep` | `grep`, `rg` |

### ファイル操作ルール

- 既存ファイルを編集する前に必ず `Read` ツールで内容を確認する
- 不要なファイル（README.md、ドキュメント類）を勝手に作成しない
- 絵文字を使わない（明示的に求められた場合のみ）

### コード生成ルール

- セキュリティ脆弱性（SQLインジェクション、XSS、コマンドインジェクション等）を含むコードを生成しない
- 過剰な実装をしない（求められた以上の機能追加・リファクタリング・コメント追加を避ける）
- エラーハンドリングは実際に起こりうるケースのみ実装する

### 確認が必要な操作

以下の操作はユーザーへの確認なしに実行しない。

- `git push`（リモートへの反映）
- `git reset --hard`（変更の破棄）
- ファイルの削除
- GitHub PR / Issue の作成・コメント
- 外部サービスへのリクエスト（Slack、メール等）
- CI/CD パイプラインの変更

### git 操作ルール

- コミットはユーザーから明示的に求められた場合のみ行う
- コミットメッセージは変更の「why」を中心に書く
- `--no-verify` や `--no-gpg-sign` は使わない
- `git add -A` や `git add .` より個別ファイルの指定を優先する

### 応答スタイル

- 応答は短く簡潔に
- コードのファイルパスは `ファイルパス:行番号` 形式で示す
- 絵文字は使わない

### メモリ管理

- セッション横断で記憶すべき情報は `~/.claude/projects/` の memory ファイルに保存する
- 一時的な作業内容は記憶しない
- ユーザーに「覚えておいて」と言われた場合のみ永続化する

### 新規プロジェクト作成時のルール

新しいプロジェクトディレクトリを作成する際は、必ずプロジェクトルートに `CLAUDE.md` を作成する。
テンプレートは `~/ai-policy/templates/CLAUDE.md.tmpl` を参照する。

CLAUDE.md に書く内容:
- `@~/.claude/CLAUDE.md`（グローバルpolicyの継承、必ず先頭に記載）
- プロジェクト概要とスタック
- 主要コマンド（dev / build / test）
- ディレクトリ構成の説明
- プロジェクト固有の禁止事項・注意点

## このリポジトリについて

AIエージェント（Claude Code / Gemini CLI / Copilot）に対する振る舞いポリシーを管理するリポジトリ。

- **場所**: `~/ai-policy/`
- **シンボリックリンク**:
  - `~/.claude/CLAUDE.md` → `~/ai-policy/CLAUDE.md`
  - `~/.claude/agents/` → `~/ai-policy/claude/agents/`
  - `~/.gemini/GEMINI.md` → `~/ai-policy/GEMINI.md`

## ディレクトリ構成

```
policy/
├── global.md                 # 全AI共通ルール
├── master/
│   ├── 00-principles.md      # シェル・ランタイム・基本方針
│   ├── 10-platform-wsl.md    # WSL固有ルール
│   └── 20-safety.md          # 安全ルール・禁止操作

claude/
└── agents/
    └── orchestrator.md       # Orchestrator固有ルール

CLAUDE.md      # Claude Code エントリポイント（このファイル）
GEMINI.md      # Gemini CLI エントリポイント
```

## このリポジトリでよく行う作業

| 作業 | 対象ファイル |
|---|---|
| Orchestratorルールの変更 | `claude/agents/orchestrator.md` |
| 全エージェント共通ルールの変更 | `policy/global.md` または `policy/master/` 以下 |
| エントリポイントの更新 | `CLAUDE.md` / `GEMINI.md` |

## 重要な制約

- `~/.zshrc` や `~/.config/mise/config.toml` などの**既存設定ファイルを直接編集しない**
- シンボリックリンク先（`~/.claude/CLAUDE.md` 等）ではなく、**リポジトリ本体（`~/ai-policy/`）を編集する**
- ポリシー変更は影響範囲を確認してから行う（複数エージェントに波及する場合がある）
- `git push` は必ずユーザー確認を取ってから実行する
