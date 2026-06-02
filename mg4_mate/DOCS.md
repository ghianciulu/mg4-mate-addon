# MG4 Mate

Trip tracking, charge logging and statistics for MG4 vehicles using Home Assistant entities from the SAIC/MG MQTT Gateway.

## Before You Start

Install and configure the SAIC MQTT Gateway first. The MG4 device should already be visible in Home Assistant with entities such as:

```text
sensor.<prefix>_soc
sensor.<prefix>_range
sensor.<prefix>_mileage
device_tracker.<prefix>_vehicle_position
binary_sensor.<prefix>_vehicle_running
binary_sensor.<prefix>_battery_charging
```

The `<prefix>` is usually the lower-case VIN used in entity ids.

## Configuration

Set these add-on options:

```yaml
log_level: info
VEHICLE_SOURCE: homeassistant
HA_URL: http://192.168.x.x:8123
HA_TOKEN: your_home_assistant_long_lived_access_token
HA_ENTITY_PREFIX: your_lowercase_vin_prefix
```

Use a local Home Assistant URL when possible. It avoids public DNS and HTTPS endpoint issues.

Create `HA_TOKEN` from your Home Assistant profile under **Long-Lived Access Tokens**. Do not use your MG/iSMART password here.

## Data & Persistence

The add-on writes trip, charge, position and statistics data into a SQLite database in the persistent `/data` directory. It reuses the Mate web UI for overview, trips, charges and statistics.

## Notes

- This fork reads Home Assistant states; it does not call the MG/iSMART cloud directly.
- Trip map quality depends on the refresh interval configured in the SAIC MQTT Gateway.
- Around 30-40 second updates while driving are enough for useful maps and consumption statistics.

Source: https://github.com/ghianciulu/mg4-mate
