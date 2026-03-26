# AGENTS.md — ai-policy

## 概要

このリポジトリは Claude / Gemini / Codex で共有する AI エージェントのポリシーとルールを管理します。
このリポジトリで作業するすべてのエージェントは以下のルールに従ってください。

---

## 正として扱うべきファイル

- `rules/` 配下がポリシー内容の正（source of truth）です。
- `CLAUDE.md` と `GEMINI.md` は `rules/` を参照する薄いエントリポイントです。
- `rules/` の外にポリシー内容を重複して記述しないでください。

現在の構成（この構造を維持してください）：

```
ai-policy/
├── CLAUDE.md           # Claude エントリポイント（15行以内）
├── GEMINI.md           # Gemini エントリポイント（15行以内）
├── rules/
│   ├── environment.md
│   ├── safety.md
│   └── mcp.md
└── agents/
    └── orchestrator.md
```

---

## 変更してはいけないもの

- `rules/safety.md` に記述されたポリシーの意味・意図
- 上記のディレクトリ構造全体
- `CLAUDE.md` / `GEMINI.md` と `rules/` の参照関係
- `agents/orchestrator.md` の構成（分割・再編禁止）

---

## 単一タスクのスコープ外

明示的に指示された場合を除き、以下は**常に対象外**です。

- MCP 連携や MCP サーバーの設定
- 大規模なディレクトリ再編・リネーム
- `orchestrator.md` の複数ファイルへの分割
- `shared/` の導入やリポジトリをまたいだ再設計
- dotfiles 固有のライブパスルールをこのリポジトリに持ち込むこと

---

## Codex / Claude の整合性

- このリポジトリに追加する Codex 向けのルールは、既存の Claude / Gemini 向けルールと整合を保ってください。
- 新しいルールを追加する場合は、先に `rules/safety.md` との矛盾がないか確認してください。
- 既存ファイルの拡張を優先し、新規ファイルの作成は最小限にしてください。

---

## 変更スコープ

- タスクに必要な**最小限の変更**のみ行ってください。
- タスクに直接関係しないファイルは変更しないでください。
- 既存の指示ソース間で曖昧さがある場合は、現在の階層を維持し最も影響の少ない変更を選んでください。

---

## 動作環境

- このリポジトリは **Windows 11 上の WSL2 (Ubuntu)** で管理しています。
- Codex / Claude Code は **WSL 内で直接起動**します。
- シンボリックリンク: `~/.claude/CLAUDE.md` → `~/ai-policy/CLAUDE.md` / `~/.gemini/GEMINI.md` → `~/ai-policy/GEMINI.md`

---

## 変更後の出力フォーマット

1. 調査した内容
2. 変更した内容（unified diff）
3. 検証結果（ファイル存在確認・構造確認）
4. 既存のリポジトリ構造との整合性
5. 残課題・懸念事項
