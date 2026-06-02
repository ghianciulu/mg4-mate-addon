# Changelog

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
