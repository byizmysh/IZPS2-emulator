# IZPS2 emulator

IZPS2 runs PlayStation 2 games on Nintendo Switch 2 through IZ2S. It uses the ARM64 core from ARMSX2 and PCSX2 and supports virtual memory cards, controller settings, and per-game save states.

## Compatibility

| Platform | Status |
| --- | --- |
| [**IZ2S**](https://github.com/byizmysh/IZ2S-Platform) | ✅ Works |
| **KaiHEN** | ⏳ Coming soon |

## Install

### Through IZ2S App library

1. Download [`izps2-emulator-0.5.0.iza`](https://github.com/byizmysh/IZPS2-emulator/releases/download/v0.5.0/izps2-emulator-0.5.0.iza).
2. In IZ2S, open **App library**, import the `.iza` file, and install it to the Switch 2 SD card. IZ2S installs the emulator in `SD:/iz2s/modules/izps2/`. The installer includes the launcher, engine, shaders, fonts, and interface assets.

### Directly to the SD card

1. Download [`izps2-emulator-0.5.0.zip`](https://github.com/byizmysh/IZPS2-emulator/releases/download/v0.5.0/izps2-emulator-0.5.0.zip).
2. Extract the ZIP to the root of the Switch 2 SD card. The `iz2s/` folder goes at the top level. The archive includes the emulator files and empty `bios/` and `games/` folders under `SD:/iz2s/modules/izps2/`.

### Add your BIOS and games

1. Copy your 4 MiB PS2 BIOS dump to `SD:/iz2s/modules/izps2/bios/`.
2. Copy your ISO or CHD game images to `SD:/iz2s/modules/izps2/games/`.
3. Open **IZPS2 emulator** in IZ2S and select a game.

Keep your BIOS, games, saves, and settings when updating. Press **Minus** during gameplay for the emulator menu.

## BIOS and games

Copy the files from your own PlayStation 2 and discs to these folders on the Switch 2 SD card. Create the folders if needed.

| File | SD card folder | Format |
| --- | --- | --- |
| **PS2 BIOS** | `SD:/iz2s/modules/izps2/bios/` | Raw **4 MiB** BIOS dump, for example `bios.bin` |
| **PS2 games** | `SD:/iz2s/modules/izps2/games/` | **ISO** (`.iso`) or **CHD** (`.chd`) disc images |

## Source and licenses

The [source tree](source/) includes the code, build recipes, and license notices for developers who want to inspect the code, fix bugs, port it, or build their own version.

See [Building](BUILDING.md), [Changelog](CHANGELOG.md), and [Third-party notices](THIRD_PARTY.md).
