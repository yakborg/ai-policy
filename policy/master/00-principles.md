# 00 - 基本方針

## シェル環境

- シェル: **zsh**
- 設定ファイル: `~/.zshrc`（編集前に必ずバックアップを確認すること）

### zsh プラグイン構成（sheldon 管理）

| プラグイン | 用途 | 読み込み方式 |
|---|---|---|
| zsh-defer | 遅延読み込みの基盤 | 即時（source） |
| zsh-autosuggestions | 入力予測 | 即時 |
| zsh-syntax-highlighting | シンタックスハイライト | defer |
| zsh-completions | 補完強化 | defer |
| ohmyzsh/git | Git エイリアス | defer |

## ランタイムマネージャー

- ツール: **mise**
- 設定ファイル: `~/.config/mise/config.toml`

### 管理対象ランタイム

```toml
[tools]
deno   = "latest"
neovim = "latest"
node   = "latest"
python = "latest"
```

- mise が PATH を管理するため、ツールのバージョン変更は `mise install` 経由で行う
- 直接 PATH を書き換えてランタイムを差し込まない

## プロンプト

- ツール: **starship**
- `.zshrc` の末尾で `eval "$(starship init zsh)"` により初期化される

## パッケージ・ツールの追加方針

1. ランタイム（言語系）→ `mise` で管理
2. zsh プラグイン → `sheldon` の `plugins.toml` に追記
3. グローバル CLI ツール → 原則 mise 経由または `~/.local/bin` に配置
4. システムパッケージ（apt）→ 最小限に抑える

## 基本ルール

- 設定変更は小さく、確認しながら進める
- 既存の動作する設定を不用意に上書きしない
- 変更前に現状を把握してから手を加える
