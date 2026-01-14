# Open WebUI

[![日本語](https://img.shields.io/badge/lang-日本語-green.svg)](README.md)
[![PyPI version](https://img.shields.io/pypi/v/open-webui.svg)](https://pypi.org/project/open-webui/)
[![License](https://img.shields.io/github/license/open-webui/open-webui.svg)](LICENSE)
[![Discord](https://img.shields.io/badge/Discord-Open_WebUI-blue?logo=discord&logoColor=white)](https://discord.gg/5rJgQTnV4s)

![Open WebUI Banner](./banner.png)

> An extensible, feature-rich, self-hosted AI platform that runs fully offline. Works with Ollama and OpenAI-compatible APIs and includes a built-in RAG inference engine.

This README focuses on Docker-based development and testing. For deployment, see the docs.

- Docs: https://docs.openwebui.com/
- Troubleshooting: https://docs.openwebui.com/troubleshooting/
- Community: https://discord.gg/5rJgQTnV4s
- Enterprise: https://docs.openwebui.com/enterprise

![Open WebUI Demo](./demo.png)

## Prerequisites

- Docker + Docker Compose

## Environment Variables

```bash
cp .env.example .env
```

Set `OLLAMA_BASE_URL` and `OPENAI_API_KEY` as needed.

## Docker Dev/Test

### Start the full stack

```bash
./run-compose.sh --build
```

The Web UI is exposed at http://localhost:3000 by default.

### Common options

```bash
./run-compose.sh --enable-gpu[count=all] --build
./run-compose.sh --enable-api[port=11435]
./run-compose.sh --data[folder=./ollama-data]
./run-compose.sh --playwright
./run-compose.sh --drop
```

### Stop

```bash
docker compose down --remove-orphans
```

### Clean up Docker

```bash
docker compose down --remove-orphans --rmi local -v
```

Note: `-v` removes volumes, so persisted data will be deleted.

### Image generation integration test (AUTOMATIC1111)

`docker-compose.a1111-test.yaml` is an overlay for integration testing only. Do not use it in production.

```bash
docker compose -f docker-compose.yaml -f docker-compose.a1111-test.yaml up -d --build
```

## Tests and Linting

```bash
pnpm run test:frontend
```

```bash
pnpm run cy:open
```

```bash
pnpm run lint
```

## Contributing

- How to contribute: `docs/CONTRIBUTING.md`
- Code of conduct: `CODE_OF_CONDUCT.md`
- CLA: `CONTRIBUTOR_LICENSE_AGREEMENT`

## License

See `LICENSE` and `LICENSE_HISTORY`.
