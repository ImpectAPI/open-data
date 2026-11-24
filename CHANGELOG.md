# Changelog

All notable changes to the IMPECT open dataset are documented here. Each version is available as a [GitHub release](https://github.com/ImpectAPI/open-data/releases) and git tag, so analyses can be pinned to a specific version of the data.

## v2.0 (2026-11-24)

All 306 matches of the Bundesliga 2023/24 were recalculated with the current IMPECT data pipeline. Results computed on v1.0 will not reproduce exactly on v2.0.

> **Note:** v2.0 currently lives on the [`v2`](https://github.com/ImpectAPI/open-data/tree/v2) branch. `main` and `kloppy.impect.load_open_data()` still serve v1.0 until a kloppy release that supports the v2.0 data is available ([PySport/kloppy#666](https://github.com/PySport/kloppy/pull/666)).

### Breaking changes

- **New event IDs.** All event IDs were regenerated. Event IDs from v1.0 do not exist in v2.0, so joins on `eventId` against v1.0 data no longer work.
- **`pass` can be `null`.** For pass-like events (`PASS`, `KICK_OFF`, `THROW_IN`, `FREE_KICK`, `GOAL_KICK`, `CORNER`), the `pass` object is now `null` whenever the pass has no end location (`end` is `null`), e.g. when it is followed by no video or interrupted by a foul or offside. In v1.0 these events had an empty object (`{"distance": 0.0, "angle": null, "receiver": null}`).

### Changed

- **Events:** event attributes were recalculated, e.g. `sequenceIndex`, set piece assignments, `action`/`actionType` and end locations of some events.
- **Event KPIs:** values were recalculated. The following KPIs are now included on event level: `SHOT_XG_FROM_PASSES` (1693), `SHOT_CREATING_ACTIONS` (1694), `PRE_ASSISTS` (1715), `SHOT_ASSISTS` (1780), `EXPECTED_SHOT_ASSISTS` (1781), `EXPECTED_GOAL_ASSISTS` (1782), `EXPECTED_PASSES` (1783).
- **Player KPIs:** match aggregates were recalculated accordingly.
- **KPI definitions:** updated descriptions for about 40 KPIs.
- **Countries:** corrected Chinese Taipei (now `TWN`/`TPE`), added FIFA names and codes for Kosovo, Curaçao and South Sudan, and removed the obsolete entries Sansibar (422), Swasiland (482) and Mazedonien (483).

### Added

- `kpi_definitions.json`: `inverted` flag marking KPIs where a lower value is better.
- `matches/`: `goals` (per period), `result`, `resultType` and `stadiumId`.
- `players/`: `height`.
- `lineups/`: `stadiumId`.
- `iterations.json`: `competition.ageGroup`.

## v1.0

Initial release of the Bundesliga 2023/24 open dataset: event data, event KPIs, player KPIs (match aggregates), lineups, match, player, squad, country, iteration and KPI definition data.
