# T1D Bridge cli

GameSir T1d (Tello one) as a gamepad on linux. This connects over BLE and
exposes a virtual controller through /dev/uinput. It runs as a systemd service.

## Install

    tar xzf t1d-bridge-cli.tar.gz
    cd t1d-bridge-cli
    bash install.sh

Turn your controller on and check `journalctl -fu t1d-bridge-cli`.

## Requirements

Any Debian-based system with systemd, BlueZ, a Bluetooth 4.0+ (BLE) adapter and
Python 3.7 or newer (RetroPie on Buster, Bullseye or Bookworm is fine). The
installer uses `apt`; on Python 3.7 it installs bleak automatically.

## Pairing

By default the bridge connects to any T1d in range. If you want to lock it to one
controller (useful if there are multiple ones nearby):

    sudo systemctl stop t1d-bridge-cli
    sudo /opt/t1d-bridge-cli/venv/bin/python /opt/t1d-bridge-cli/t1d_bridge_cli.py --pair
    sudo systemctl start t1d-bridge-cli

It scans, lets you pick if more than one is found, waits for a button press
to confirm the link works Then it saves the address in the config.
`--forget` clears it. No Bluetooth bonding is involved, since the T1d doesn't need it.

## Config

`/etc/t1d-bridge-cli.conf`, then `sudo systemctl restart t1d-bridge-cli`.
Swap buttons in `[buttons]`, flip sticks with `invert_*`.

## Debugging

    sudo systemctl stop t1d-bridge-cli
    sudo /opt/t1d-bridge-cli/venv/bin/python /opt/t1d-bridge-cli/t1d_bridge_cli.py --scan
    sudo /opt/t1d-bridge-cli/venv/bin/python /opt/t1d-bridge-cli/t1d_bridge_cli.py --dump

## License

PolyForm Noncommercial 1.0.0 (see `LICENSE`). Free for personal and other
non-commercial use. Commercial use needs permission from the author.

Required Notice: Copyright 2026 Tuhholainen

Credit: packet decoding is derived from https://github.com/pors/gamesir_t1d
(MIT). See `NOTICE` for the license text.

Not affiliated with or endorsed by GameSir or Microsoft. All product names
are trademarks of their respective owners and are used only to describe
compatibility.
