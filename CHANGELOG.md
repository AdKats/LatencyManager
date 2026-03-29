# Changelog

## v2.0.0 (Procon v2 Refactor)

- Converted from `.inc` + game-variant stubs to single `.cs` in `src/`
- Removed `BF3/`, `BF4/`, `BFHL/` game-variant directories
- Converted code style to System types (`String`, `Int32`, `Boolean`, etc.)
- Added `.editorconfig` and `CLatencyManager.csproj` for CI format checks
- Added CI and release GitHub Actions workflows
- Added `CLAUDE.md`, `README.md`, `CHANGELOG.md`, `LICENSE`, `.gitignore`

## v1.0.1.16 (Legacy)

- Last release of the Procon v1 version (see `legacy` branch)
- Country-based and ping-based player kicking
- Average ping sampling with configurable thresholds
- Missing ping detection with configurable delay (EBassie)
- Whitelist bypass options for country kicker (EBassie)
- Player threshold bypass option for country kicker (EBassie)
