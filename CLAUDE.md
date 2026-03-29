# CLatencyManager -- Procon v2 Plugin

## Project Overview

CLatencyManager is a C# latency management plugin for Procon v2 (Battlefield game server administration). It provides two methods for removing players causing lag: country-based kicking and ping-based kicking. The legacy Procon v1 version lives on the `legacy` branch.

- **Language:** C#
- **License:** GPLv3
- **Original Author:** Zaeed (Matt Green), with modifications by EBassie
- **Supported games:** BF3, BF4, BF Hardline
- **Dependencies:** Procon v2 (runtime only)

## Architecture

The plugin is a single file:

| File | Responsibility |
|------|---------------|
| `src/CLatencyManager.cs` | All plugin logic: settings UI, country kicking, ping kicking, PunkBuster integration, version checking |

## Code Style

Style is enforced by `.editorconfig` and checked via `dotnet format` in CI.

**Critical conventions:**
- **Use `String`, `Int32`, `Boolean`, `Double`** -- NOT `string`, `int`, `bool`, `double`. The codebase uses explicit System type names everywhere.
- **Allman brace style** -- opening brace on its own line
- **4 spaces** for indentation, LF line endings
- **Block-scoped namespaces** (not file-scoped)
- **`using` directives outside namespace**, System usings first

## Build & CI

- `CLatencyManager.csproj` at root is a **CI-only artifact** for `dotnet format`. It is NOT a real build file -- Procon v2 assemblies are unavailable for compilation.
- **CI workflow** (`.github/workflows/ci.yml`): runs on push to `master` and PRs. Checks `dotnet format whitespace` and `dotnet format style --exclude-diagnostics IDE1007`.
- **Release workflow** (`.github/workflows/release.yml`): triggered by `v*` tags. Packages `.cs` files from `src/` into a zip and creates a GitHub Release.

### Running style checks locally

```bash
dotnet restore
dotnet format whitespace --verify-no-changes
dotnet format style --verify-no-changes --severity warn --exclude-diagnostics IDE1007
```

## Threading Model

The plugin does not use dedicated threads. It relies on Procon's task scheduler (`procon.protected.tasks.add`) to run periodic checks:
- `CountryCheckerTask` -- runs every 5 seconds, checks new players against country rules
- `PingCheckerTask` -- runs every 30 seconds, checks player pings against threshold

## Event Registrations

The plugin registers for these Procon events:
- `OnVersion` -- detects game type (BF3, BF4, BFHL)
- `OnPunkbusterPlayerInfo` -- retrieves player country via PunkBuster
- `OnPlayerLeft` -- cleans up player tracking data
- `OnPlayerPingedByAdmin` -- records ping samples for average-based kicking
- `OnPlayerJoin` -- triggers country check on join
- `OnListPlayers` -- tracks player list and handles missing-ping detection
- `OnServerInfo` -- tracks player count for threshold enforcement

## Supported Games

- BF3
- BF4
- BF Hardline (BFHL)

## Branch Structure

- `master` -- current development, Procon v2 only
- `legacy` -- archived Procon v1 version, no longer maintained
