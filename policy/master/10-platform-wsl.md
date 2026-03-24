# 10 - プラットフォーム: WSL 固有ルール

## 動作環境

- OS: Ubuntu on WSL2
- カーネル: Linux 6.6.87.2-microsoft-standard-WSL2
- ホストOS: Windows

## パス規則

### Linux 側（作業の基点）

- ホームディレクトリ: `/home/noda`（`~` で参照）
- ユーザーローカルバイナリ: `~/.local/bin`
- mise 管理バイナリ: `~/.local/share/mise/` 以下（mise が自動管理）

### Windows ファイルシステムへのアクセス

- Windows ドライブは `/mnt/c/`、`/mnt/d/` などにマウントされる
- **作業ファイルは原則 Linux 側（`/home/noda/` 以下）に置く**
- `/mnt/` 以下のファイルへの書き込みは I/O が遅くなるため避ける

## WSL 固有の注意事項

### ファイルパーミッション

- `/mnt/` 以下は Windows のファイルシステムのため、パーミッション設定が Linux と異なる
- スクリプトに実行権限を付与する場合は Linux 側に置くこと

### 環境変数

- Windows の環境変数は WSL から参照できる場合があるが、依存しない
- PATH は `.zshrc` で明示的に設定されたものを使う

### GUI アプリケーション

- WSLg 経由で Linux GUI アプリが動作する
- VSCode は Windows 側の Remote-WSL 拡張経由で接続する

### クリップボード

- Windows のクリップボードと共有される（`/dev/clipboard` または `clip.exe` 経由）

## ネットワーク

- `localhost` は WSL2 内の localhost を指す
- Windows 側のサービスへのアクセスは `$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}')` で取得したホストIP を使う（WSL2 の場合）

## シンボリックリンクの扱い

- Linux 側で作成したシンボリックリンクは `/mnt/` 以下では正常に動作しない場合がある
- dotfiles 管理では Linux 側のホームディレクトリ内に完結させる
