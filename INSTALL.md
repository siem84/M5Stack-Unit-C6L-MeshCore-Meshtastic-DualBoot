# Installation

## Hardware

Target device:

**M5Stack Unit C6L**

- ESP32-C6
- SX1262
- 16 MB flash
- OLED display

## Firmware images

Each release contains two image types.

### Standard BIN

Use the standard `.bin` to update MeshCore on an existing compatible DualBoot installation.

It is flashed to:

`0x10000`

This updates the MeshCore `app0` application only.

### Merged BIN

Use the `-merged.bin` image for a clean / first-time DualBoot installation.

It is flashed to:

`0x0`

The merged image contains the complete 16 MB flash layout.

WARNING: flashing a full merged image can overwrite existing NVS and filesystem data.

## First installation

Example esptool command:

~~~powershell
python esptool.py `
  --chip esp32c6 `
  --port COM8 `
  --baud 460800 `
  write_flash `
  --flash_mode dio `
  --flash_size 16MB `
  0x0 "<firmware>-merged.bin"
~~~

After flashing:

1. Disconnect power.
2. Wait a few seconds.
3. Reconnect power.
4. Radio Rain is displayed.
5. The DualBoot menu appears.

## Updating MeshCore only

~~~powershell
python esptool.py `
  --chip esp32c6 `
  --port COM8 `
  --baud 460800 `
  write_flash `
  --flash_mode dio `
  --flash_size 16MB `
  0x10000 "<firmware>.bin"
~~~

## USER button

- short press: change MeshCore / Meshtastic selection
- hold 1–3 seconds: start selected system
- hold 3 seconds or longer: save selected system as default
- 10 seconds without input: start saved default system

## Download mode

The physical RESET button can be used to enter ESP32-C6 download mode when required.

RESET and the front USER button are separate controls.

## Checksums

Verify the SHA256 checksum before flashing a downloaded release image.
