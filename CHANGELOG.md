# Changelog

## v0.3.0-beta

Hardware-tested M5Stack Unit C6L DualBoot release.

### Added

- Radio Rain procedural startup animation
- 5-second animation duration
- reduced rain density
- staggered falling columns
- DualBoot OLED startup menu
- persistent default-system selection
- 10-second inactivity auto-start
- live START feedback
- live SET DEF feedback
- default-system indicator
- improved OLED menu spacing

### USER controls

- short press - switch MeshCore / Meshtastic
- hold 1–3 seconds - start selected system
- hold >=3 seconds - save selected system as default

### MeshCore

- Companion Radio BLE
- M5Stack Unit C6L OLED support
- dedicated `mc_spiffs`
- corrected SPIFFS partition handling
- configuration import verified
- persistent settings verified
- LoRa RX/TX verified

### Meshtastic

- M5Stack Unit C6L DualBoot environment
- 16 MB DIO board definition
- dedicated DualBoot partition layout
- OTA-slot switching integration

### DualBoot

- app0 - MeshCore
- app1 - Meshtastic
- native ESP-IDF OTA selection
- no separate boot-menu application

## v0.2.2

Development milestone:

- DualBoot menu and menu sounds
- MeshCore `mc_spiffs` storage fix
- configuration persistence verified
- radio operation verified

## v0.2.0

Development milestone:

- startup menu hosted by MeshCore
- USER selection of MeshCore or Meshtastic

## v0.1.0

Initial proven DualBoot architecture:

- MeshCore in app0
- Meshtastic in app1
- reboot-based OTA-slot switching
