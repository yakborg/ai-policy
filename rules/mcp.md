# MCP サーバー管理

## セットアップの教訓

- エントリポイントは `pyproject.toml` の `[project.scripts]` で確認する
- `python -m <package>` ではなく `.venv/bin/<script名>` を使う
- ディレクトリ移動後は `.venv` を作り直す（シェバンにパスがハードコードされるため）
- `claude mcp add-json` は **必ず `--scope user` を付ける**（省略すると project スコープになり `claude mcp list` に表示されない）

### venv の再作成手順

```bash
cd ~/mcp-servers/<server>/
rm -rf .venv
python -m venv .venv
.venv/bin/pip install -e .
```

---

## 登録済み MCP サーバー

### google-analytics（GA4）

- リポジトリ: `~/mcp-servers/google-analytics-mcp/`
- 認証: `~/.secrets/gcp/ga4-mcp-key.json`

再登録コマンド:

```bash
claude mcp add-json "google-analytics" \
  '{"command":"/home/noda/mcp-servers/google-analytics-mcp/.venv/bin/analytics-mcp","args":[],"env":{"GOOGLE_APPLICATION_CREDENTIALS":"/home/noda/.secrets/gcp/ga4-mcp-key.json"}}' \
  --scope user
```

---

## 配置規則

- 場所: `~/mcp-servers/<server-name>/`（`~/projects/` には置かない）
- 認証情報: `~/.secrets/gcp/` または `~/.secrets/env/`
- `.venv` は `.gitignore` に追加してリポジトリに含めない
