# Latency Manager

A Procon plugin for managing player latency on Battlefield game servers (BF3, BF4, BF Hardline).

## Features

### Country-Based Kicking
- Allow or disallow players from specific countries
- Uses PunkBuster player info for country detection
- Configurable kick message with `%country%` placeholder
- Option to ignore whitelist for country kicks
- Option to ignore player threshold for country kicks

### Ping-Based Kicking
- Two methods: **Instant kick** or **Average ping**
- Average mode samples pings over time before deciding to kick
- Configurable ping limit, sample size, and minimum samples before kicking
- Option to kick players with no/missing ping data
- Configurable delay before checking for missing pings
- Configurable kick message with `%ping%` placeholder

### General Settings
- Player count threshold before rules are enforced
- Player whitelist to exempt specific players
- In-game notifications (Yell or Say)
- Debug message logging
- Automatic plugin update notifications

## Installation

1. Download the latest release from the [Releases](../../releases) page
2. Extract `CLatencyManager.cs` to your Procon plugins directory under the appropriate game folder
3. Restart Procon or reload plugins
4. Configure settings through the Procon plugin interface

## Configuration

All settings are configurable through the Procon plugin settings interface, organized into sections:

- **Country Functions** -- Enable/disable country kicking, select allowed/disallowed countries
- **Ping Functions** -- Enable/disable ping kicking, set limits and methods
- **Settings** -- Debug output, whitelist, player thresholds, in-game messages

## License

GPLv3 -- see [LICENSE](LICENSE) for details.

## Credits

- **Zaeed** (Matt Green) -- original author
- **EBassie** -- missing ping detection, whitelist/threshold bypass options
