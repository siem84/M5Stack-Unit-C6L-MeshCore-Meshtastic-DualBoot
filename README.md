[English](README.md) | [Polski](README_PL.md)

# M5Stack Unit C6L — MeshCore + Meshtastic DualBoot
## About this project

M5Stack Unit C6L is a small LoRa device that can be used with different mesh systems. This project was created so you do not have to choose only one of them. Instead of reflashing the device every time, it can start either MeshCore or Meshtastic, selected directly from a simple on-screen menu.

The project builds on my earlier **[MeshCore-M5Stack-Unit-C6L-UI](https://github.com/siem84/MeshCore-M5Stack-Unit-C6L-UI)** project, developed specifically for the M5Stack Unit C6L and originally based on the official MeshCore project. Official Meshtastic was then added together with a DualBoot mechanism that allows both systems to be used on the same device.

The idea is simple: **one C6L, two mesh systems, and an easy way to switch between them without reflashing the device.**

Have fun!  
**siem84 (siemkowsky)**


DualBoot firmware for the **M5Stack Unit C6L** combining:

- **MeshCore Companion Radio BLE**
- **Meshtastic**
- native ESP32-C6 OTA partition switching
- OLED startup menu
- Radio Rain boot animation
- persistent default-system selection

## Current release

**v0.3.0-beta**

Tested on real M5Stack Unit C6L hardware.

### Project lineage

| Component | Base |
|---|---|
| MeshCore for C6L | previous M5Stack Unit C6L MeshCore port/project by `siem84` |
| Original MeshCore upstream base | `dev` / `ac7d88e` |
| Meshtastic | official `2.7.26` / `54e0d8d` |
| C6L DualBoot UI | `v0.3.0` |

The MeshCore firmware used in this DualBoot project is **not a fresh port made directly from stock MeshCore**.

It continues the previously developed **M5Stack Unit C6L MeshCore port by siem84**, which itself was originally derived from the official MeshCore project. The current DualBoot project builds on that working C6L version and adds the DualBoot integration, startup menu, Radio Rain, persistent default-system selection and storage-related changes.

The public MeshCore patch is provided against the stated upstream MeshCore revision so the complete C6L + DualBoot modification set can be reproduced from the official source base.

## Startup

After power-on:

1. **Radio Rain** animation runs for approximately 5 seconds.
2. DualBoot menu appears.
3. USER button controls the selection.

### USER button

- short press: switch `MeshCore / Meshtastic`
- hold **1–3 seconds**: start selected system
- hold **3 seconds or longer**: save selected system as default
- no input for **10 seconds**: automatically start the saved default

The OLED displays:

- `START: MC` / `START: MT`
- `SET DEF: MC` / `SET DEF: MT`
- `DEF: MC` / `DEF: MT`

The default after a clean installation is **MeshCore**.

## DualBoot architecture

No separate boot-menu application is used.

The ESP32-C6 native OTA layout is used:

- `ota_0` / `app0` → MeshCore
- `ota_1` / `app1` → Meshtastic

MeshCore hosts the startup menu. Meshtastic returns the next normal reboot to MeshCore.

## Storage

MeshCore and Meshtastic use separate SPIFFS partitions:

- Meshtastic: `spiffs`
- MeshCore: `mc_spiffs`

MeshCore includes a C6L DualBoot storage fix so preferences, configuration import and persistent settings operate on the correct `mc_spiffs` partition.

## Installation

See [INSTALL.md](INSTALL.md).

## Technical details

See [TECHNICAL.md](TECHNICAL.md).

## Source modifications

Clean source patches are provided in:

`patches/`

These patches are intended to be applied to the corresponding upstream revisions.

## Project status

Hardware verified:

- MeshCore BLE operation
- MeshCore configuration import
- persistent MeshCore settings
- MeshCore LoRa RX/TX
- Meshtastic startup
- MC ↔ MT switching
- persistent default-system selection
- 10-second automatic startup
- OLED menu and Radio Rain animation

## Upstream projects

- MeshCore: https://github.com/meshcore-dev/MeshCore
- Meshtastic firmware: https://github.com/meshtastic/firmware

This project is an independent community modification and is not an official release of either upstream project.

## License

See [LICENSES.md](LICENSES.md).

