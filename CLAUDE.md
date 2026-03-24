# CLAUDE.md

このファイルは Claude Code がプロジェクト（dotfiles）を操作する際に参照する指示書です。

## 参照するポリシー

以下のファイルを必ず読み込んでから作業を開始してください。

### 全AI共通ルール

- [`policy/global.md`](policy/global.md) — 回答スタイル・環境概要・禁止事項

### 共通ルール（すべてのエージェント共通）

- [`policy/master/00-principles.md`](policy/master/00-principles.md) — シェル・ランタイム・ツール管理の基本方針
- [`policy/master/10-platform-wsl.md`](policy/master/10-platform-wsl.md) — WSL 固有のパス・設定ルール
- [`policy/master/20-safety.md`](policy/master/20-safety.md) — 編集前確認・禁止操作・ツール追加ルール

### Claude Code 固有ルール

- [`policy/agents/claude-code.md`](policy/agents/claude-code.md) — ツール優先順位・コード生成・git 操作・応答スタイル

## この dotfiles リポジトリについて

このリポジトリは `/home/noda` 環境の設定管理方針を文書化したものです。

- **シェル**: zsh
- **ランタイムマネージャー**: mise
- **プラグインマネージャー**: sheldon
- **プロンプト**: starship
- **プラットフォーム**: WSL2 (Linux 6.6.87.2-microsoft-standard-WSL2)

## 重要な制約

- `~/.zshrc` や `~/.config/mise/config.toml` などの**既存設定ファイルを直接編集しない**
- 詳細は `policy/master/20-safety.md` の「絶対に編集しないファイル」を参照
