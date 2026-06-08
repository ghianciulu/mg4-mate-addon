# Changelog



- Added maintenance tracker: MG4-specific 10-item service schedule (tires, brake fluid, cabin filter, A/C, HV battery, full inspection, etc.) with overdue/upcoming/OK status, inline "Log service" form, and full service history log.
- Added trip comparison: "Similar trips" section on the trip detail page surfaces past trips with the same route (haversine start/end proximity ≤ 5 km), comparable distance (±40%), and similar time-of-day (±4 h), scored 0–100 with efficiency delta colour-coded green/red.
- Refactored DB migration system: replaced 40-line ad-hoc `ALTER TABLE` block in `poller/db.py.__init__` with a versioned `MIGRATIONS` list + `schema_migrations` table, making future schema changes one-liner additions.

# Changelog




- Fixed trip distance when SAIC gateway was inactive: `finalize_trip` now uses `max(GPS haversine, odometer delta)` so trips where the gateway didn't update speed/position still record the correct distance.
- Hidden sub-0.1 km trips from the trips list and overview: micro-trips created by `vehicle_running` oscillation while the gateway is inactive no longer appear in the UI.
- Fixed stale open trip being resumed on addon restart: `_resume_or_close` now checks the last recorded GPS point timestamp; if older than `trip_merge_gap_min`, the orphan is closed and a fresh trip is created instead of continuing the old one.
- Fixed ghost trip being used as merge candidate: `get_recent_ended_trip` now excludes `untracked=1` trips so the next real drive is never merged into a ghost trip record.
- Fixed SQLite timestamp comparison: `get_recent_ended_trip` cutoff now uses `T` separator (ISO format) instead of space, preventing `'2026-06-05T11:45...'` from comparing as newer than `'2026-06-05 13:39...'`.

# Changelog




- Added ghost trip detection: when the odometer increases while the car is parked (missed by the SAIC gateway), MG4 Mate automatically creates an untracked trip record with the estimated distance. Untracked trips are shown with a ⚠️ badge in the trips list.
- Added `ha_automations/saic_gateway_commute_boost.yaml`: one-shot HA script to permanently lower `gateway_inactive_refresh_period` from 86400 s (24 h) to 120 s, preventing the SAIC gateway from missing trip starts when the car wakes from sleep.

# Changelog



- Added ghost trip detection: when the odometer increases while the car is parked (missed by the SAIC gateway), MG4 Mate automatically creates an untracked trip record with the estimated distance. Untracked trips are shown with a ⚠️ badge in the trips list.

# Changelog



- Fixed timezone display (improved): timezone now fetched from HA `/api/config` at startup and stored as `display_timezone` setting; `ZoneInfo` used for accurate conversion even when the host OS runs UTC. Added `tzdata` Python package so `ZoneInfo` works in slim Docker containers.

# Changelog



- Fixed timezone display: all trip/charge timestamps were shown in UTC instead of local time. SQLite queries now use the `'localtime'` modifier; Python formatting uses `astimezone()`; Jinja2 templates use a new `localts` filter.

# Changelog



- Added Charts page (`/charts`) with four analytical sections:
  - SOC history linechart with 7d / 30d / 90d / all-time period selector.
  - Monthly charge costs stacked bar chart grouped by charge type (Home / AC / Fast / HPC).
  - Efficiency vs outside temperature scatter chart with linear regression trend line.
  - All-trips polyline map (last 200 trips), colour-coded by efficiency; click for details.

# Changelog



- Replaced battery temperature with outside temperature on overview status card; AC target temperature kept.

# Changelog



- Expanded vehicle page: individual door states, bonnet, 12V aux battery, lights on/off, compass heading — fetched from HA and stored in positions table.
- Added tyre pressure sensors (FL/FR/RL/RR) with SVG top-down car visualization; wheels colour-coded green/amber/red by pressure; low-pressure warning banner.

# Changelog



- Auto-correct charge start SOC: when poller wakes up during an active charge (PARKED_SLEEP gap), use the last pre-plug-in position SOC instead of the current (already-charging) SOC.
- Added manual charge edit: each charge card now has an inline edit panel to correct start/end times and SOC values; derived fields (duration, energy, cost) are recalculated automatically.

# Changelog




- Fixed trip merge: stale WAL read caused merged trips to appear unchanged after redirect.
- Fixed trip merge: added hx-swap="none" to merge forms to prevent HTMX swap interference.
- Added 9 unit tests covering merge correctness and WAL cache invalidation.

# Changelog




- Fixed 500 error on trips page caused by `get_trips_grouped()` converting days dict to list after SQL rewrite.
- Added regression test for trips grouped structure.

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
