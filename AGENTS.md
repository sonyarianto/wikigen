# Agent Instructions

## Releasing a new version

When bumping the version, always update **both** files:

1. `Cargo.toml` — change the `version` field
2. `Cargo.lock` — the version appears in the `[[package]]` entry for `wakawiki`; run `cargo check` after bumping `Cargo.toml` to regenerate it, then commit both

Before committing the release:
- Run `cargo fmt --check`
- Run `cargo clippy -- -D warnings`
- Run `cargo test`
- Ensure no unstaged changes in `Cargo.lock`
- Update `CHANGELOG.md` with the new version's changes

Tag format: `v{version}` (e.g. `v0.1.4`)
<!-- wakawiki:start -->
## wakawiki Documentation

This repository has wakawiki-generated documentation in the `wakawiki/` directory.
When you need context about the codebase, reference the files in `wakawiki/`:
- `wakawiki/index.md` — Project overview
- `wakawiki/architecture.md` — Architecture and design

You can also use the wakawiki CLI to update documentation:
```bash
wakawiki --update
```
<!-- wakawiki:end -->
