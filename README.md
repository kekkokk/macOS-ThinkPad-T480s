# macOS on Lenovo ThinkPad T480s

This repository contains a sample configuration to run macOS (Currently Mojave `10.14`) on a Lenovo ThinkPad T480s

## Used Hardware Configuration

- Lenovo ThinkPad T480s
  - Intel i5-8250U
  - 8GB RAM onboard + Crucial DDR4 2400-SODIMM
  - Samsung 970 evo NVMe SSD
  - Dell DW1560 Wireless (original Intel AC8265 not working)
    - Wi-Fi device ID [`14e4:43b1`], shows as Apple Airport Extreme due to `AirportBrcmFixup.kext`
    - Bluetooth device ID [`0a5c:216f`], chipset `20702A3` with firmware `v14 c5882` using `BrcmPatchRAM2.kext`
  - Realtek ALC257 by `AppleALC.kext` with `layout-id` 11 (requies a [patch][alc], already patched in this repo)
  - Intel UHD Graphics 620 (Nvidia MX150 disabled, Optimus not supported by macOS)
  - Power management and battery status by ACPI hotpatching
  - Integrated camera (works out of the box)
  - Keyboard/Elan Touchpad (PS/2) using `VodooPS2Controller.kext` + `VodooSMBus.kext` modified for t480s / P52 by leo-labs
    - You can also use `ApplePS2SmartTouchPad.kext` that is inside backup folder if you encounter problems but you should disable trackpoint since it's not supported
- Disabled devices
  - WWAN (no module)
- Untested devices
  - SD card reader
  - Fingerprint scanner
  - Thunderbolt 3 (USB type-c works)
- Firmware Revisions
  - BIOS version `1.26`

## Preparation

* (**Important**) You need to generate a proper `config.plist` with unique serial numbers:
  - Run `./tools/gen.sh` (macOS) or `tools\gen.bat` (Windows) to generate `config.plist`.
  - Add `-f` or `--force` flag to forcibly regenerate `config.plist` with new serial numbers.
* All SSDT hotpatches are located at `EFI/CLOVER/ACPI/dsl`. You can update the compiled `.aml` binaries by running `update.sh` (macOS) or `update.bat` (Windows).
* The `SSDT-KBD.aml` is tuned for `VodooPS2Controller.kext`. If you want to switch to `ApplePS2SmartTouchPad.kext`, use `SSDT-KBD.aml` in `backup` folder instead.
* The PrintScr keyboard key will disable/enable the trackpad

## Credits

- [OS-X-Clover-Laptop-Config (Hot-patching)](https://github.com/RehabMan/OS-X-Clover-Laptop-Config)
- [Dell XPS 13 9360 Guide](https://github.com/the-darkvoid/XPS9360-macOS)
- [ThinkPad X1 Carbon Gen 6 Guide](https://github.com/tylernguyen/x1c6-hackintosh)
- [VodooSMBus i2c-i801 driver port for macOS X + ELAN SMBus macOS X driver for Thinkpad T480s, P52 by leo-labs](https://github.com/leo-labs/VoodooSMBus)

[alc]: https://github.com/acidanthera/AppleALC/pull/324
[clover]: https://www.tonymacx86.com/threads/guide-booting-the-os-x-installer-on-laptops-with-clover.148093/
[uuid]: https://www.uuidgenerator.net/
[macserial]: https://github.com/acidanthera/macserial
