# ai-policy

Claude Code / Gemini CLI / Copilot などの
AIエージェントに対する振る舞いポリシーを管理するリポジトリ。

## 構成

```
policy/
├── global.md                 # 全AI共通ルール
├── master/
│   ├── 00-principles.md      # シェル・ランタイム・基本方針
│   ├── 10-platform-wsl.md    # WSL固有ルール
│   └── 20-safety.md          # 安全ルール・禁止操作
└── agents/
    ├── claude-code.md
    ├── gemini-cli.md
    └── copilot.md

CLAUDE.md      # Claude Code エントリポイント
GEMINI.md      # Gemini CLI エントリポイント
templates/     # 新規プロジェクト用 CLAUDE.md テンプレート
```

## セットアップ（新しいマシン）

```bash
# リポジトリをクローン
git clone git@github.com:yakborg/ai-policy.git ~/ai-policy

# シンボリックリンクを作成
ln -sf ~/ai-policy/CLAUDE.md ~/.claude/CLAUDE.md
ln -sf ~/ai-policy/GEMINI.md ~/.gemini/GEMINI.md
```
