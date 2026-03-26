# MCP サーバー管理

再インストール・再登録の手順は `/mcp-reinstall` スキルを使う。

## 登録済み MCP サーバー

### google-analytics（GA4）

- リポジトリ: `~/dev/google-analytics-mcp/`
- 認証: `~/.secrets/gcp/ga4-mcp-key.json`

### chatwork

- リポジトリ: `~/dev/chatwork-tools/`
- 認証: `~/.secrets/env/yakborg.secret`（`CHATWORK_API_TOKEN`）
- 起動: `deno run --allow-net --allow-env src/mcp/server.ts`

## 配置規則

- 場所: `~/dev/<name>/`（プロジェクトも MCP サーバーもすべて `~/dev/` に統合）
- 認証情報: `~/.secrets/gcp/` または `~/.secrets/env/`
- `.venv` は `.gitignore` に追加してリポジトリに含めない
