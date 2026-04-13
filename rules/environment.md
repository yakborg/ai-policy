# 環境構成

## シェル環境

- シェル: **zsh** / 設定: `~/.zshrc`

### zsh プラグイン構成（sheldon 管理）

| プラグイン | 用途 | 読み込み |
|---|---|---|
| zsh-defer | 遅延読み込みの基盤 | 即時 |
| zsh-autosuggestions | 入力予測 | 即時 |
| zsh-syntax-highlighting | シンタックスハイライト | defer |
| zsh-completions | 補完強化 | defer |
| ohmyzsh/git | Git エイリアス | defer |

## ランタイムマネージャー（mise）

- 設定: `~/.config/mise/config.toml`
- 管理対象: `deno` / `neovim` / `node` / `python`（すべて latest）
- バージョン変更は `mise install` 経由。直接 PATH を書き換えない

## プロンプト（starship）

`~/.zshrc` 末尾の `eval "$(starship init zsh)"` で初期化。

## ツール追加の優先順位

```
1. ランタイム（言語系）      → mise
2. zsh プラグイン           → sheldon の plugins.toml に追記
3. グローバル CLI ツール     → mise 経由または ~/.local/bin
4. システムパッケージ（apt） → 最終手段
```

## 開発ディレクトリ

- 開発リポジトリ・MCP サーバーはすべて `~/dev/<name>/` に配置する
- `~/projects/` や `~/mcp-servers/` は廃止済み

---

## WSL 固有ルール

- OS: Ubuntu on WSL2（カーネル: 6.6.87.2-microsoft-standard-WSL2）
- ホスト: Windows 11 / Windows username: `tecon`

### パス規則

| 領域 | パス |
|---|---|
| ホームディレクトリ | `/home/noda`（`~`） |
| ユーザーローカルバイナリ | `~/.local/bin` |
| mise 管理バイナリ | `~/.local/share/mise/` |
| Windows ドライブ | `/mnt/c/`、`/mnt/d/` など |

**作業ファイルは必ず Linux 側（`/home/noda/` 以下）に置く。**
`/mnt/` 以下は I/O が遅く、パーミッションも異なるため書き込みを避ける。

### 注意事項

- シェル環境が必要なコマンドは `wsl zsh -ic "<command>"` でラップする
- シンボリックリンクは `/mnt/` 以下では動作しない場合がある
- Windows 環境変数には依存しない（PATH は `.zshrc` で明示管理）
- `localhost` は WSL2 内を指す（Windows 側サービスとは別）

---

## git push の委譲

### 制約の背景

Codex は MCP 経由サブプロセスとして起動するため `SSH_AUTH_SOCK` が継承されず、
SSH 認証による `git push` が失敗する（Codex CLI 一般の仕様ではなくこの実行経路固有の制約）。
Claude Code はターミナル起動のため `SSH_AUTH_SOCK` を継承でき、`git push` を正常に実行できる。

### ルール

- Codex は `git push` を自分では実行しない
- commit 完了後、Claude Code の `Bash` ツールに `git push origin <branch>` を委譲する
- push 結果（成功/失敗）を Codex に返し、Codex がユーザーへ報告する
- ユーザーが「自分で push する」と明示した場合は委譲不要
