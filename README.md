# MG4 Mate — Home Assistant Add-on

Home Assistant add-on for MG4 trip tracking, charge logging and live vehicle status. Reads data from Home Assistant entities published by the [SAIC MQTT Gateway](https://github.com/SAIC-iSmart-API/saic-python-mqtt-gateway).

> 🇮🇹 Versione italiana più sotto.

---

## What it does

| Section | Description |
|---|---|
| **Overview** | Live SOC, range, odometer, temperatures, charge state, last position on map |
| **Trips** | Automatic detection, GPS route, distance, duration, efficiency — auto & manual merge |
| **Charges** | Sessions with SOC gain, energy, peak power, cost by type, manual correction |
| **Statistics** | Distance, energy, efficiency and regen summaries |
| **Vehicle** | Tyre pressure SVG diagram, individual doors, bonnet, lights, heading, 12 V battery |
| **Controls** | Remote lock, climate, charging, target SOC — relayed via Home Assistant |

---

## Prerequisites

Before installing MG4 Mate you need:

1. **SAIC MQTT Gateway** running and publishing your MG4 entities to Home Assistant.
   Install it from: [github.com/SAIC-iSmart-API/saic-python-mqtt-gateway](https://github.com/SAIC-iSmart-API/saic-python-mqtt-gateway)

2. A **Home Assistant long-lived access token**.
   Generate one under **Profile → Long-lived access tokens**.

---

## Installation

1. In Home Assistant go to **Settings → Add-ons → Add-on Store**.
2. Click the **⋮** menu (top right) → **Repositories**.
3. Add this URL and click **Add**:
   ```
   https://github.com/ghianciulu/mg4-mate-addon
   ```
4. Find **MG4 Mate** in the store and click **Install**.
5. Go to the add-on **Configuration** tab and fill in the options.
6. Click **Start**, then **Open Web UI**.

---

## Configuration

| Option | Required | Description |
|---|---|---|
| `VEHICLE_SOURCE` | ✅ | Always `homeassistant` |
| `HA_URL` | ✅ | Local URL of your HA instance — use the LAN IP, e.g. `http://192.168.1.10:8123` |
| `HA_TOKEN` | ✅ | Your long-lived access token |
| `HA_ENTITY_PREFIX` | ✅ | Lower-case VIN prefix used in entity IDs |

### How to find your entity prefix

In Home Assistant go to **Developer Tools → States** and search for your VIN. You will find entities like:

```
sensor.lsjwh4097rnxxxxxx_soc
sensor.lsjwh4097rnxxxxxx_range
```

The prefix is everything before `_soc` (or any other suffix):

```
HA_ENTITY_PREFIX = lsjwh4097rnxxxxxx
```

> **Tip:** Use the local LAN IP in `HA_URL`, not `homeassistant.local`. This avoids mDNS resolution issues inside the add-on container.

---

## License

[GNU AGPL-3.0](./LICENSE) © Angelo La Mazza

---
---

# MG4 Mate — Add-on Home Assistant 🇮🇹

Add-on Home Assistant per tracciamento viaggi, sessioni di ricarica e stato del veicolo MG4. Legge i dati dalle entità Home Assistant pubblicate dal [SAIC MQTT Gateway](https://github.com/SAIC-iSmart-API/saic-python-mqtt-gateway).

---

## Cosa fa

| Sezione | Descrizione |
|---|---|
| **Panoramica** | SOC in tempo reale, autonomia, odometro, temperature, stato ricarica, ultima posizione su mappa |
| **Viaggi** | Rilevamento automatico, mappa GPS, distanza, durata, efficienza — unione automatica e manuale |
| **Ricariche** | Sessioni con guadagno SOC, energia, potenza picco, costo per tipo, correzione manuale |
| **Statistiche** | Riepiloghi distanza, energia, efficienza e regen |
| **Veicolo** | Diagramma SVG pressione gomme, stato porte singole, cofano, luci, direzione, batteria 12 V |
| **Comandi** | Blocco remoto, clima, ricarica, target SOC — eseguiti tramite Home Assistant |

---

## Prerequisiti

Prima di installare MG4 Mate ti serve:

1. **SAIC MQTT Gateway** attivo e che pubblica le entità MG4 su Home Assistant.
   Installalo da: [github.com/SAIC-iSmart-API/saic-python-mqtt-gateway](https://github.com/SAIC-iSmart-API/saic-python-mqtt-gateway)

2. Un **token di accesso di lunga durata** di Home Assistant.
   Generalo da **Profilo → Token di accesso di lunga durata**.

---

## Installazione

1. In Home Assistant vai su **Impostazioni → Add-on → Store**.
2. Menu **⋮** (in alto a destra) → **Repository**.
3. Aggiungi questo URL e clicca **Aggiungi**:
   ```
   https://github.com/ghianciulu/mg4-mate-addon
   ```
4. Trova **MG4 Mate** nello store e clicca **Installa**.
5. Vai nella scheda **Configurazione** dell'add-on e compila le opzioni.
6. Clicca **Avvia**, poi **Apri interfaccia web**.

---

## Configurazione

| Opzione | Richiesta | Descrizione |
|---|---|---|
| `VEHICLE_SOURCE` | ✅ | Sempre `homeassistant` |
| `HA_URL` | ✅ | URL locale di Home Assistant — usa l'IP LAN, es. `http://192.168.1.10:8123` |
| `HA_TOKEN` | ✅ | Il tuo token di accesso |
| `HA_ENTITY_PREFIX` | ✅ | Prefisso VIN minuscolo usato negli ID entità |

### Come trovare il prefisso entità

In Home Assistant vai su **Strumenti per sviluppatori → Stati** e cerca il tuo VIN. Troverai entità come:

```
sensor.lsjwh4097rnxxxxxx_soc
sensor.lsjwh4097rnxxxxxx_range
```

Il prefisso è tutto quello prima di `_soc` (o qualsiasi altro suffisso):

```
HA_ENTITY_PREFIX = lsjwh4097rnxxxxxx
```

> **Suggerimento:** Usa l'IP LAN in `HA_URL`, non `homeassistant.local`. Evita problemi di risoluzione mDNS all'interno del container dell'add-on.

---

## Licenza

[GNU AGPL-3.0](./LICENSE) © Angelo La Mazza
