# M5Stack Unit C6L DualBoot v0.3.0-beta

First public beta release of the M5Stack Unit C6L DualBoot firmware combining:

- MeshCore Companion Radio BLE
- Meshtastic
- OLED DualBoot menu
- Radio Rain startup animation
- persistent default-system selection

## Project lineage and base versions

### MeshCore

The MeshCore component continues the previously developed **M5Stack Unit C6L MeshCore port by siem84**.

That earlier C6L project was originally derived from official MeshCore:

- upstream MeshCore base: `dev / ac7d88e`
- C6L port/project: `siem84`
- current project: C6L DualBoot `v0.3.0`

The supplied MeshCore patch is based against the upstream revision and contains the full C6L + DualBoot modification set.

### Meshtastic

- official Meshtastic: `2.7.26 / 54e0d8d`

### DualBoot UI

- C6L DualBoot UI: `v0.3.0`

## USER button

- short press: switch MeshCore / Meshtastic
- hold 1-3 s: start selected system
- hold >=3 s: save selected system as default
- 10 s inactivity: automatically start saved default

## Firmware files

### Standard update image

MeshCore-dev-ac7d88e_Meshtastic-2.7.26-54e0d8d_M5Stack-Unit-C6L_C6L-UI-v0.3.0-beta.bin

Flash at:

0x10000

Use this only with an existing compatible C6L DualBoot installation.

SHA256:

11B4B575243C6785A070F9911FF2A8E6E796D68A1DEEDF533944A4559ABE2461

### Complete merged image

MeshCore-dev-ac7d88e_Meshtastic-2.7.26-54e0d8d_M5Stack-Unit-C6L_C6L-UI-v0.3.0-beta-merged.bin

Flash at:

0x0

This is the complete 16 MB image intended for first-time installation.

WARNING: a full merged flash can overwrite NVS and filesystem data.

SHA256:

87A91D2023D0F033E12A0DD0A47C311461E72588213B277C098DA89814A5EAAB

## Hardware verification

Tested on M5Stack Unit C6L:

- Radio Rain OLED animation
- DualBoot menu
- MeshCore / Meshtastic switching
- persistent default selection
- automatic startup timeout
- MeshCore BLE
- MeshCore configuration import
- persistent MeshCore settings
- MeshCore LoRa RX/TX

## Source

Source modification patches are included in the repository under:

patches/

See README.md, README_PL.md, INSTALL.md and TECHNICAL.md for details.

## Status

This is a beta release intended for wider hardware testing.

The project is an independent community modification and is not an official MeshCore, Meshtastic or M5Stack release.
