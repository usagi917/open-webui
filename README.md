# Open WebUI

[![English](https://img.shields.io/badge/lang-English-blue.svg)](README.en.md)
[![PyPI version](https://img.shields.io/pypi/v/open-webui.svg)](https://pypi.org/project/open-webui/)
[![License](https://img.shields.io/github/license/open-webui/open-webui.svg)](LICENSE)
[![Discord](https://img.shields.io/badge/Discord-Open_WebUI-blue?logo=discord&logoColor=white)](https://discord.gg/5rJgQTnV4s)

![Open WebUI Banner](./banner.png)

> オフラインで動作する、拡張可能で機能豊富なセルフホスト型AIプラットフォーム。OllamaやOpenAI互換APIに対応し、RAG用の推論エンジンを内蔵しています。

このREADMEはローカル開発とDockerベースのテスト開発に焦点を当てています。運用/導入はドキュメントを参照してください。

- ドキュメント: https://docs.openwebui.com/
- トラブルシューティング: https://docs.openwebui.com/troubleshooting/
- コミュニティ: https://discord.gg/5rJgQTnV4s
- エンタープライズ: https://docs.openwebui.com/enterprise

![Open WebUI Demo](./demo.png)

## 前提条件

- Node.js: `>=18.13.0 <=22.x.x`
- パッケージマネージャー: pnpm (推奨) / npm
- Python: `>=3.11 <3.13.0a1`
- Pythonパッケージマネージャー: uv (推奨) / pip
- Docker + Docker Compose (Docker開発/テスト時)

## ローカル開発 (フロント/バック分離)

### バックエンド

```bash
cd backend
uv pip install -r requirements.txt
./dev.sh
```

```bash
# uvを使わない場合
cd backend
pip install -r requirements.txt
./dev.sh
```

バックエンドは既定で http://localhost:8080 で起動します。

### フロントエンド

```bash
pnpm install
pnpm dev
```

Viteの開発サーバーは既定で http://localhost:5173 で起動します。

```bash
# pnpmを使わない場合
npm install
npm run dev
```

### 環境変数

```bash
cp .env.example .env
```

`OLLAMA_BASE_URL` や `OPENAI_API_KEY` を必要に応じて設定してください。

## Dockerでの開発/テスト

### フルスタック起動

```bash
./run-compose.sh --build
```
 docker compose up -d

Web UIは既定で http://localhost:3000 に公開されます。

### 代表的なオプション

```bash
./run-compose.sh --enable-gpu[count=all] --build
./run-compose.sh --enable-api[port=11435]
./run-compose.sh --data[folder=./ollama-data]
./run-compose.sh --playwright
./run-compose.sh --drop
```

### 停止

```bash
docker compose down --remove-orphans
```

### Dockerのクリーンアップ

```bash
docker compose down --remove-orphans --rmi local -v
```

※ `-v` はボリュームも削除するため、保存済みデータは失われます。

### 画像生成の統合テスト (AUTOMATIC1111)

`docker-compose.a1111-test.yaml` は統合テスト用のオーバーレイです。運用には使用しないでください。

```bash
docker compose -f docker-compose.yaml -f docker-compose.a1111-test.yaml up -d --build
```

## テスト/静的解析

```bash
pnpm run test:frontend
```

```bash
pnpm run cy:open
```

```bash
pnpm run lint
```

## コントリビュート

- 参加方法: `docs/CONTRIBUTING.md`
- 行動規範: `CODE_OF_CONDUCT.md`
- CLA: `CONTRIBUTOR_LICENSE_AGREEMENT`

## ライセンス

`LICENSE` と `LICENSE_HISTORY` を参照してください。
