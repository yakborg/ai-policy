# ai-policy

Claude Code / Gemini CLI などの AI エージェントに対する振る舞いポリシーを管理するリポジトリ。

## 構成

```
CLAUDE.md          # Claude Code エントリポイント（最小限・常時読み込み）
GEMINI.md          # Gemini CLI エントリポイント（最小限・常時読み込み）
rules/
├── environment.md # 環境構成（WSL・mise・シェル）
├── safety.md      # 安全ルール・Claude Code 固有ルール
└── mcp.md         # MCP サーバー管理
agents/
└── orchestrator.md # Orchestrator 固有ルール
commands/
├── mcp-reinstall.md # /mcp-reinstall スキル
└── new-project.md   # /new-project スキル
```

## シンボリックリンク

```bash
~/.claude/CLAUDE.md  → ~/ai-policy/CLAUDE.md
~/.claude/agents/    → ~/ai-policy/agents/
~/.claude/commands/  → ~/ai-policy/commands/
~/.gemini/GEMINI.md  → ~/ai-policy/GEMINI.md
```

## セットアップ（新しいマシン）

```bash
git clone git@github.com:yakborg/ai-policy.git ~/ai-policy

ln -sf ~/ai-policy/CLAUDE.md  ~/.claude/CLAUDE.md
ln -sf ~/ai-policy/agents     ~/.claude/agents
ln -sf ~/ai-policy/commands   ~/.claude/commands
ln -sf ~/ai-policy/GEMINI.md  ~/.gemini/GEMINI.md
```

## よく行う作業

| 作業 | 対象ファイル |
|---|---|
| 環境・ツール構成の変更 | `rules/environment.md` |
| 安全ルール・Claude Code 固有ルールの変更 | `rules/safety.md` |
| MCP サーバーの追加・変更 | `rules/mcp.md` |
| Orchestrator ルールの変更 | `agents/orchestrator.md` |
| スキルの追加・変更 | `commands/` 以下 |
| エントリポイントの変更 | `CLAUDE.md` / `GEMINI.md` |

## 編集上の注意

- シンボリックリンク先ではなく、必ずリポジトリ本体（`~/ai-policy/`）を直接編集する
- ポリシー変更は影響範囲を確認してから行う（複数エージェントに波及する場合がある）
- `git push` は必ずユーザー確認を取ってから実行する
