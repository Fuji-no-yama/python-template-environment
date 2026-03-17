# Python Devcontainer + uv Template

`devcontainer` と `uv` を使って、Python 開発をすぐ始めるための最小テンプレートです。

## 含まれるもの

- Python 3.10 ベースの Dev Container
- `uv` による仮想環境作成と依存同期
- `ruff` による lint / format 設定
- VS Code 設定（保存時フォーマット、import 整理）
- `astral-sh.ty` 拡張による Language Server 利用

## クイックスタート

### Dev Container で使う（推奨）

1. VS Code でこのフォルダを開く
2. `Dev Containers: Reopen in Container` を実行
3. 初回起動時に `postCreateCommand` で以下が実行される
   - `uv venv --clear`
   - `uv sync`

### ローカルで使う

```bash
uv venv
source .venv/bin/activate
uv sync
```

## 日常コマンド

```bash
# lint
uv run ruff check .

# lint 自動修正
uv run ruff check --fix .

# format
uv run ruff format .
```

## 補足（Language Server）

- Language Server は `astral-sh.ty` の VS Code 拡張で提供する想定です。
- そのため、コンテナ内に `ty` バイナリを別途インストールしない構成になっています。

## テンプレート利用時の初期変更

1. `pyproject.toml` の `project.name` を変更
2. 必要な依存を `dependencies` に追加
3. 必要なら `requires-python` を変更
4. 新規リポジトリとして使う場合は `.git` を作り直す

## 構成

```text
.
├── .devcontainer/
│   ├── devcontainer.json
│   ├── docker-compose.yml
│   └── Dockerfile.work
├── .vscode/
│   └── settings.json
├── pyproject.toml
└── ReadMe.md
```
