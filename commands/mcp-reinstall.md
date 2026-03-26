# MCP サーバー 再インストール・再登録

引数で指定されたサーバー名（省略時は一覧を表示して選択を促す）の MCP サーバーを再インストールし、Claude Code に再登録する。

## 手順

1. 対象サーバーのディレクトリに移動
2. `.venv` を削除して再作成
3. パッケージをインストール
4. `claude mcp add-json --scope user` で再登録
5. `claude mcp list` で登録を確認

## venv 再作成の共通手順

```bash
cd ~/mcp-servers/<server>/
rm -rf .venv
python -m venv .venv
.venv/bin/pip install -e .
```

## サーバー別の設定

### google-analytics

- パス: `~/mcp-servers/google-analytics-mcp/`
- スクリプト: `.venv/bin/analytics-mcp`
- 認証: `~/.secrets/gcp/ga4-mcp-key.json`

```bash
claude mcp add-json "google-analytics" \
  '{"command":"/home/noda/mcp-servers/google-analytics-mcp/.venv/bin/analytics-mcp","args":[],"env":{"GOOGLE_APPLICATION_CREDENTIALS":"/home/noda/.secrets/gcp/ga4-mcp-key.json"}}' \
  --scope user
```

## 注意事項

- `--scope user` を必ず付ける（省略すると project スコープになり `claude mcp list` に出ない）
- ディレクトリを移動した場合は必ず `.venv` を作り直す（シェバンにパスがハードコードされるため）
- エントリポイント名は `pyproject.toml` の `[project.scripts]` で確認する
