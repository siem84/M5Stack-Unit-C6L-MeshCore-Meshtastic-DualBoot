# Technical details

## Hardware

M5Stack Unit C6L:

- ESP32-C6
- SX1262 LoRa radio
- 16 MB flash
- OLED display

## DualBoot architecture

The project uses native ESP-IDF OTA application slots.

There is no third boot-menu firmware.

| OTA slot | Firmware |
|---|---|
| app0 / ota_0 | MeshCore |
| app1 / ota_1 | Meshtastic |

MeshCore hosts the startup menu.

When Meshtastic is selected, MeshCore selects the Meshtastic OTA partition and restarts.

Meshtastic is configured so its next normal reboot returns to MeshCore and the startup menu.

## Partition layout

| Partition | Offset | Size |
|---|---:|---:|
| nvs | `0x009000` | `0x005000` |
| otadata | `0x00E000` | `0x002000` |
| app0 - MeshCore | `0x010000` | `0x640000` |
| app1 - Meshtastic | `0x650000` | `0x640000` |
| spiffs - Meshtastic | `0xC90000` | `0x300000` |
| mc_spiffs - MeshCore | `0xF90000` | `0x060000` |
| coredump | `0xFF0000` | `0x010000` |

Flash end:

`0x1000000` = 16 MB

## Flash mode

`DIO`

## MeshCore

### Lineage

The MeshCore side of this project continues the previously developed **M5Stack Unit C6L MeshCore port by siem84**.

Development lineage:

`official MeshCore dev/ac7d88e`
→ `siem84 M5Stack Unit C6L MeshCore port`
→ `current C6L DualBoot version`

The published patch is intentionally based against upstream MeshCore `dev / ac7d88e`, so it contains both the earlier C6L-port changes and the later DualBoot-specific modifications.

Upstream reference revision:

`dev / ac7d88e`

PlatformIO environment:

`M5Stack_Unit_C6L_companion_radio_ble_dualboot`

Configuration:

- Companion Radio
- BLE transport
- M5Stack Unit C6L OLED support
- DualBoot integration

### MeshCore filesystem

MeshCore uses:

`mc_spiffs`

The C6L DualBoot storage modification ensures SPIFFS garbage collection operates on the `mc_spiffs` partition rather than the default Meshtastic SPIFFS partition.

Hardware testing confirmed:

- configuration import
- preference persistence
- LoRa RX
- LoRa TX

## Meshtastic

Reference:

- version `2.7.26`
- commit `54e0d8d`

PlatformIO environment:

`m5stack-unitc6l-dualboot`

The Meshtastic modification contains:

- dedicated 16 MB DIO board definition
- DualBoot partition table
- OTA-slot switching integration

## Startup sequence

1. Radio Rain - approximately 5 seconds
2. DualBoot menu
3. USER interaction or 10-second inactivity timeout
4. selected/default system starts

There is no visible countdown.

## Default system

The saved default is stored in NVS namespace:

`c6l_dualboot`

Values:

- `0` - MeshCore
- `1` - Meshtastic

A clean installation defaults to MeshCore.

## OLED menu

The menu provides live feedback:

- `START: MC`
- `START: MT`
- `SET DEF: MC`
- `SET DEF: MT`
- `DEF: MC`
- `DEF: MT`
