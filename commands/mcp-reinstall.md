# MCP サーバー 再インストール・再登録

引数で指定されたサーバー名（省略時は一覧を表示して選択を促す）の MCP サーバーを再インストールし、Claude Code に再登録する。

## 手順

1. 対象サーバーのディレクトリに移動
2. 必要に応じて依存関係を再インストール
3. `claude mcp remove` で既存登録を削除
4. `claude mcp add` で再登録
5. `claude mcp list` で接続を確認

## サーバー別の設定

### google-analytics

- パス: `~/dev/google-analytics-mcp/`
- エントリポイント: `.venv/bin/analytics-mcp`
- 認証: `~/.secrets/gcp/ga4-mcp-key.json`

```bash
# venv 再作成
cd ~/dev/google-analytics-mcp/
rm -rf .venv
python -m venv .venv
.venv/bin/pip install -e .

# 再登録
claude mcp remove "google-analytics" -s user
claude mcp add google-analytics -s user \
  -e GOOGLE_APPLICATION_CREDENTIALS=/home/noda/.secrets/gcp/ga4-mcp-key.json \
  -- /home/noda/dev/google-analytics-mcp/.venv/bin/analytics-mcp
```

### chatwork

- パス: `~/dev/chatwork-tools/`
- エントリポイント: `src/mcp/server.ts`（Deno）
- 認証: `~/.secrets/env/yakborg.secret`（`CHATWORK_API_TOKEN`）

```bash
# 再登録（Deno はインストール不要）
source ~/.secrets/env/yakborg.secret
claude mcp remove "chatwork" -s user
claude mcp add chatwork -s user \
  -e CHATWORK_API_TOKEN="$CHATWORK_API_TOKEN" \
  -- /home/noda/.local/share/mise/installs/deno/2.7.8/bin/deno \
  run --allow-net --allow-env \
  /home/noda/dev/chatwork-tools/src/mcp/server.ts
```

## 注意事項

- `-s user` を必ず付ける（省略すると project スコープになり全プロジェクトで使えない）
- Python venv を再作成した場合、シェバンにパスがハードコードされるため `.venv` を作り直す必要がある
- Deno のパスは `which deno` で確認（mise 管理のため更新時にパスが変わる可能性あり）
- エントリポイント名は `pyproject.toml` の `[project.scripts]` で確認する
