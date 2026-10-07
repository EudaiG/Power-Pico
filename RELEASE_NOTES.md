# 1.2.0 Stable Build

## Changes

- Refined the Modern UI into a rounded, card-based instrument layout with
  clearer voltage, current, power, brightness, and focus states.
- Added a selectable Modern theme page with multiple accent palettes and
  swatches, while retaining the Classic UI as an alternate build option.
- Split fixed-voltage PD control from PPS control into separate workflows.
  The fixed-voltage page dynamically lists the charger’s advertised fixed PD
  voltage PDOs, while PPS remains available through its own capability-aware
  workflow.
- Fixed immediate language refresh so Chinese/English changes apply without
  rebooting. Reworked page refresh/lifetime handling to avoid the previous
  intermittent language-switch lockups and screen corruption during page
  transitions.
- Improved charger cold-start compatibility so the display/application can
  initialize more reliably when power is connected through different ports or
  chargers.
- Preserved the CMake application layout and OTA/vector-address fix that
  allows CMake-built images to upload through the existing Bootloader and
  client path.
- Disabled the unused LVGL Chart module, reducing the Modern image by 5,376
  bytes without changing the active UI or protocol behavior.
- Modern UI alongside the retained Classic build option.
- Local PD fixed-voltage and PPS workflows, input-startup compatibility changes.
- Upstream 1.1.7 CMD commands and wire-format calibration compatibility.
- Dedicated calibration EEPROM region separate from settings and update flag.
- USB receive buffering now accepts fragmented `A5 5A` CMD frames with
  bounded backpressure; transmit buffering snapshots caller data, prioritizes
  CMD responses, and retains the latest pending measurement packet.
- Two-entry CMD RX/TX queues, bounded receive batches, and CMD RX task
  priority above the ADC sender.
- CMD TX-ready wakeup and two-entry UI measurement queue.
- Added EEPROM write/readback verification and explicit CMD EEPROM-error
  reporting while retaining legacy `update\r\n` OTA compatibility.

This version number does not indicate official upstream release status.

## Release Image

Filename: `firmware/PowerPico_Firmware_v1.2.0.bin`

SHA256: `E229043E0F34DA95F139D456041998CC05327760C1E9450CA0EDE06EFCD97303`

Image size: 444572 bytes. Application flash budget: 458752 bytes.
Remaining application flash: 14180 bytes.
Linker RAM reservation: 114264 of 131072 bytes.
The RAM figure includes reserved heap pools; it is not a runtime heap/stack
free-space measurement.

## Validation

- The release image was rebuilt from the cleaned source tree on October 7, 2026.
- The previously hardware-tested firmware used the same application baseline and
  was uploaded successfully through the existing Bootloader/OTA path.
- Fragmented CMD regression: 80/80 cases passed.
- CMD plus continuous ADC duplex regression: 200/200 replies passed, with no
  missing or unexpected frames.
- The Chart cleanup does not change the active protocol, task scheduling,
  EEPROM layout, or UI behavior.
