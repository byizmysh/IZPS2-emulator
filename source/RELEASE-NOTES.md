# IZPS2 emulator 0.5.0

IZPS2 runs PlayStation 2 games on Nintendo Switch 2 through [IZ2S](https://github.com/byizmysh/IZ2S-Platform).

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
