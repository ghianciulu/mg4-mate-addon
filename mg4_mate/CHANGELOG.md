# Changelog

## 1.2.0

- Added auto-merge for trips separated by a short gap (configurable, default 5 min).
- Added manual merge button on trip detail page to combine adjacent trips.
- Added IT/EN translations for all new merge UI strings.

## 1.1.2

- Fixed `urllib.error` import missing in HA client (would crash poller on 404).
- Fixed regen energy accumulation to use real elapsed time between polls instead of hardcoded 10 s.
- Removed dead `_conn()` function from web DB layer.
- Live map on overview now refreshes every 30 s together with the status card via HTMX.
- Optimised trip tree query: aggregation moved to SQLite, reducing Python memory use.

## 1.1.1

- Persistent SQLite connections in web layer (no more per-request `connect()`).
- Distance-weighted average efficiency in statistics summary.
- Targeted Home Assistant entity fetch: 27 individual calls in parallel instead of loading all states.
- Raised charge history default limit from 50 to 500.

## 1.1.0

- Removed broken car-picture card from overview; map now spans full width.
- Fixed HA history import to use proper DB methods instead of direct SQLite access.
- Improved mobile layout across trips, charges, statistics and trip detail pages.

## 1.0.9

- Adds Settings language selection for English and Italian.
- Ships interface translations as file-based JSON locales.
- Pins the add-on build to MG4 Mate commit `7280fb4`.

## 1.0.8

- Adds Home Assistant history import for existing MG4 positions, trips and charge sessions.
- Improves mobile layout for the remote controls page.
- Pins the add-on build to MG4 Mate commit `f9c42fc`.

## 1.0.7

- Adds the MG4 Mate remote controls page backed by Home Assistant services.
- Includes controls for locks, climate, defrosters, charging, target SOC, charge current limit, heated seats and find-my-car when exposed by Home Assistant.
- Pins the add-on build to MG4 Mate commit `9a341fc`.

## 1.0.6

- Pins the add-on build to MG4 Mate commit `a0ba8ba`.
- Makes the web server create the static directory before mounting it.

## 1.0.5

- Rebuilds against MG4 Mate with the required `web/static` directory included.

## 1.0.4

- Rebranded the add-on repository as MG4 Mate.
- Installs MG4 Mate from `https://github.com/ghianciulu/mg4-mate`.
- Uses Home Assistant entities from the SAIC MQTT Gateway as the only vehicle source.
- Removes cloud login, setup wizard and remote-command references.
