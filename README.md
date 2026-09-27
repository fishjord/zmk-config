# ZMK Config

This repository contains Ness's personal ZMK firmware configuration, keymaps, and shields used to build **wireless** (Bluetooth) firmware for custom split keyboards, powered by controllers like the nice!nano (with support for nice!view and ZMK Studio).

## Related Repositories

- **Keyboard PCBs & Design Files**: [nest_keyboards](https://github.com/fishjord/nest_keyboards) — Hardware designs, schematics, KiCad PCB files, Ergogen configs, and 3D-printable cases/plates for the Nest keyboard family.
- **Wired Firmware (QMK)**: [qmk_userspace](https://github.com/fishjord/qmk_userspace) — Custom QMK userspace configuration, keymaps, and keyboard definitions for building wired QMK firmware.

## Supported Keyboards & Targets

Build targets configured in [`build.yaml`](build.yaml) include:

- **Egret**: Compact split ergonomic keyboard with nice!view display shields and ZMK Studio support (`egret_left`, `egret_right`).
- **Nest (Crane)**: Split keyboard with ZMK Studio support (`nest_left`, `nest_right`).
- **Settings Reset**: Utility firmware to clear paired Bluetooth bonds (`settings_reset`).

## Building Firmware

### Automated (GitHub Actions)

Firmware images (`.uf2`) are automatically compiled via GitHub Actions workflows on push according to the matrix defined in [`build.yaml`](build.yaml). The resulting firmware binaries can be downloaded directly from the GitHub Actions run artifacts or Releases.

### Local (West)

To build locally using the Zephyr/ZMK toolchain:

```bash
# Initialize west workspace pointing to local config
west init -l config
west update
west zephyr-export

# Example: Build left half of Egret with nice!view and ZMK Studio
west build -s zmk/app -b nice_nano -- -DSHIELD="egret_left nice_view" -DSNIPPET=studio-rpc-usb-uart -DCONFIG_ZMK_STUDIO=y
```
