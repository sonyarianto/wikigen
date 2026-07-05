# Changelog

All notable changes to this project will be documented in this file.

## [0.1.4] - 2026-07-05

### Added
- Animated spinner with status messages during LLM API calls ("Generating documentation...", "Updating documentation...", "Thinking...")
- Tool call progress output in one-shot (`-p`) and update (`--update`) modes
- 120-second timeout on all provider HTTP requests (OpenAI, Anthropic, custom)
- 120-second timeout on opencode subprocess calls

### Changed
- VitePress documentation site added

## [0.1.3] - 2026-06-29

### Changed
- Renamed project from wikigen to wakawiki

### Fixed
- npm binary wrapper renamed to wakawiki

## [0.1.2] - 2026-06-29

### Changed
- Node.js version bumped to 24 in CI

## [0.1.1] - 2026-06-29

### Added
- npm package distribution
- Multi-platform binary release CI workflow

## [0.1.0] - 2026-06-28

### Added
- Initial release
- Interactive documentation generation with LLM agents
- One-shot mode (`-p`) for non-interactive use
- Update mode (`--update`) for refreshing existing docs
- Multi-provider support: OpenAI, Anthropic, DeepSeek, OpenRouter, opencode
- Filesystem scanner with list, read, search, and hash operations
- Metadata tracking for incremental updates
- Comprehensive test suite (40 tests)
- GitHub Actions CI
