# WikiGen

A CLI that writes and maintains agent documentation for your codebase. Built in Rust.

Inspired by [OpenWiki](https://github.com/langchain-ai/openwiki).

## Features

- **Agent-driven documentation** — LLM explores your codebase, reads files, searches for patterns, and writes structured docs
- **Multiple providers** — OpenAI, Anthropic, DeepSeek, OpenRouter, or local `opencode` (no API key needed)
- **Tool-calling agent loop** — `list_files`, `read_file`, `search`, `write_doc`
- **Incremental updates** — `--update` refreshes only what changed
- **AGENTS.md integration** — appends a reference block so coding agents know where the docs live
- **GitHub Actions ready** — one-shot `-p` mode works in CI

## Install

```bash
cargo install --git https://github.com/sonyarianto/wikigen.git
```

Or build from source:

```bash
git clone https://github.com/sonyarianto/wikigen.git
cd wikigen
cargo build --release
```

## Quick Start

```bash
# Configure your LLM provider
wikigen --init

# Generate documentation (interactive)
wikigen

# One-shot non-interactive
wikigen -p "Summarize the architecture of this project"

# Update existing documentation
wikigen --update
```

## Usage

```
wikigen [OPTIONS] [PROMPT]

Options:
      --init     Configure provider, API key, and model
  -p, --print    Non-interactive one-shot mode
      --update   Refresh existing wikigen/ docs
  -h, --help     Show help
```

### Provider Options

| Provider | API Key Required | Notes |
|----------|-----------------|-------|
| OpenAI | Yes | GPT-4, GPT-4o |
| Anthropic | Yes | Claude Sonnet |
| DeepSeek | Yes | OpenAI-compatible API |
| OpenRouter | Yes | Unified API gateway |
| opencode | **No** | Uses local `opencode` CLI |
| Custom | Yes | Any OpenAI-compatible endpoint |

### opencode provider

If you already use [opencode](https://github.com/anomalyco/opencode), you can run wikigen with zero API keys:

```bash
wikigen --init    # select "opencode"
wikigen           # uses your existing opencode setup
```

## Output

```
wikigen/
├── index.md            # Project overview
├── architecture.md     # High-level architecture
├── ...                 # Additional module docs
└── .wikigen.json      # Metadata for incremental updates
```

An `AGENTS.md` file is created (or appended) with a reference block pointing agents to `wikigen/`.

## GitHub Action

Add this workflow to auto-update docs daily via PR:

```yaml
name: wikigen update
on:
  schedule:
    - cron: '0 0 * * *'
  workflow_dispatch:

jobs:
  update:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions-rust-lang/setup-rust-toolchain@v1
      - run: cargo install --git https://github.com/sonyarianto/wikigen.git
      - run: wikigen --update
        env:
          WIKIGEN_PROVIDER: ${{ secrets.WIKIGEN_PROVIDER }}
          WIKIGEN_API_KEY: ${{ secrets.WIKIGEN_API_KEY }}
          WIKIGEN_MODEL: ${{ secrets.WIKIGEN_MODEL }}
      - uses: peter-evans/create-pull-request@v6
        with:
          title: 'docs: update wikigen documentation'
          branch: wikigen-update
```

## Configuration

Config is stored in `~/.wikigen/.env`:

```
WIKIGEN_PROVIDER=openai
WIKIGEN_API_KEY=sk-...
WIKIGEN_MODEL=gpt-4o
WIKIGEN_BASE_URL=https://api.openai.com/v1
```

You can also set these as environment variables directly.

## License

MIT — see [LICENSE](LICENSE).
