# MG4 Mate — Home Assistant Add-on

Home Assistant add-on for MG4 trip tracking, charge logging and statistics. It reuses the Mate UI/database and reads MG4 data from Home Assistant entities created by the SAIC MQTT Gateway.

> Italian version below.

## Install

1. In Home Assistant go to **Settings → Add-ons → Add-on Store**.
2. Click the **⋮** menu → **Repositories**.
3. Add this URL:

   ```text
   https://github.com/ghianciulu/mg4-mate-addon
   ```

4. Find **MG4 Mate**, click **Install**, then configure the add-on options.
5. Start the add-on and open its panel.

## Required Options

```yaml
VEHICLE_SOURCE: homeassistant
HA_URL: http://192.168.x.x:8123
HA_TOKEN: your_home_assistant_long_lived_access_token
HA_ENTITY_PREFIX: your_lowercase_vin_prefix
```

The MG4 entity prefix is the part before the sensor suffix. For example:

```text
sensor.lsjwh4097rn111393_soc
```

uses:

```text
HA_ENTITY_PREFIX=lsjwh4097rn111393
```

---

## 🇮🇹 Add-on Home Assistant

Add-on Home Assistant per statistiche, viaggi e ricariche MG4. Riusa UI e database di Mate e legge i dati MG4 dalle entità Home Assistant create da SAIC MQTT Gateway.

### Installazione

1. In Home Assistant vai su **Impostazioni → Add-on → Store**.
2. Menu **⋮** → **Repository**.
3. Aggiungi questo URL:

   ```text
   https://github.com/ghianciulu/mg4-mate-addon
   ```

4. Trova **MG4 Mate**, installa e configura le opzioni.
5. Avvia l'add-on e apri il pannello.

### Opzioni richieste

```yaml
VEHICLE_SOURCE: homeassistant
HA_URL: http://192.168.x.x:8123
HA_TOKEN: token_lungo_home_assistant
HA_ENTITY_PREFIX: prefisso_vin_minuscolo
```

Esempio:

```text
sensor.lsjwh4097rn111393_soc
```

usa:

```text
HA_ENTITY_PREFIX=lsjwh4097rn111393
```

## License

[GNU AGPL-3.0](./LICENSE) © Silvio Bressani.
