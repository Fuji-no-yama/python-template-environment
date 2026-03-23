# Python Devcontainer + uv Template

`devcontainer` と `uv` を使って、Python 開発をすぐ始めるための最小テンプレートです。

## 含まれるもの

- Python 3.13 ベースの Dev Container
- `uv` による仮想環境作成と依存同期
- `uv` 管理の `ruff` による lint / format 設定
- コンテナ内で使える `codex` CLI
- VS Code 設定（保存時フォーマット、import 整理）
- `astral-sh.ty` 拡張による Language Server 利用

## クイックスタート

### Dev Container で使う（推奨）

1. VS Code でこのフォルダを開く
2. `Dev Containers: Reopen in Container` を実行
3. 初回起動時に `postCreateCommand` で以下が実行される
   - `uv venv --clear`
   - `uv sync`
4. `codex` を使う場合は、必要に応じてコンテナ内で認証する
   - `codex login`
   - または `OPENAI_API_KEY` を環境変数に設定する

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

## Codex CLI

このテンプレートでは、Dev Container のイメージビルド時に `codex` CLI をインストールします。

```bash
codex --version
codex login
codex
```

- ホストの `~/.codex` はコンテナの `/root/.codex` にマウントされるため、認証情報や設定を共有できます。
- API キーを使う場合は、`OPENAI_API_KEY` をコンテナ内の環境変数に設定してください。

## 補足（Language Server）

- Language Server は `astral-sh.ty` の VS Code 拡張で提供する想定です。
- そのため、コンテナ内に `ty` バイナリを別途インストールしない構成になっています。
- `ruff` 本体は VS Code 拡張ではなく `uv` の開発依存（`[dependency-groups].dev`）で管理します。

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
└── README.md
```
