# MCP サーバー管理

再インストール・再登録の手順は `/mcp-reinstall` スキルを使う。

## 登録済み MCP サーバー

### google-analytics（GA4）

- リポジトリ: `~/mcp-servers/google-analytics-mcp/`
- 認証: `~/.secrets/gcp/ga4-mcp-key.json`

## 配置規則

- 場所: `~/mcp-servers/<server-name>/`（`~/projects/` には置かない）
- 認証情報: `~/.secrets/gcp/` または `~/.secrets/env/`
- `.venv` は `.gitignore` に追加してリポジトリに含めない
