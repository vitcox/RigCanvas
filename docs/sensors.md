# Sensor reference

[← Back to the README](../README.md) · [Theme guide](themes.md) · [User guide](user-guide.md) · [Troubleshooting](troubleshooting.md)

Every value a theme can show has a **sensor key**. You pick it in the editor (the *Sensor* field of a widget, grouped by category), or type it into label text as a [placeholder](themes.md#placeholders): `CPU {cpu.temp}°C`.

What's available depends on your hardware and on what's running. A value that can't be read right now shows as `--`.

**Where the values come from**

| Source | Needed for | Setup |
|---|---|---|
| LibreHardwareMonitor | CPU, GPU, RAM, disks, motherboard | Built in. CPU temperature / power and motherboard fans need the free [PawnIO](https://pawnio.eu/) driver |
| Windows | Network, uptime, "now playing", audio, hardware names | Built in |
| [Open-Meteo](https://open-meteo.com/) | Weather | Type a place in **Settings → Weather** |
| RivaTuner Statistics Server | Game FPS | Optional; must be running (it comes with MSI Afterburner) |
| HWiNFO from Thermalright TRCC | GPU 16-pin / PCIe power, named board fans | Optional; only if TRCC is installed (**Settings → TRCC compatibility**) |

## Hardware names (text)

| Key | Example |
|---|---|
| `cpu.name` | AMD Ryzen 7 5800X3D |
| `cpu.model` | Ryzen 7 5800X3D |
| `cpu.vendor` | AMD |
| `gpu.name` | NVIDIA GeForce RTX 5070 Ti |
| `gpu.model` | RTX 5070 Ti |
| `gpu.vendor` | NVIDIA |

Use these in labels (`{gpu.model|upper}`) instead of typing your own model, so a theme looks right on every PC.

## GPU

| Key | Unit | Notes |
|---|---|---|
| `gpu.temp` | °C | Core temperature |
| `gpu.hotspot` | °C | Not reported by every GPU (RTX 50 series doesn't) |
| `gpu.vram.temp` | °C | Memory junction |
| `gpu.load` | % | |
| `gpu.power` | W | Total board power |
| `gpu.power.16pin` | W | 12VHPWR / 12V-2x6 connector (HWiNFO only) |
| `gpu.power.pcie` | W | PCIe slot +12 V (HWiNFO only) |
| `gpu.power.percent` | % | Of the power limit |
| `gpu.clock` | MHz | |
| `gpu.vram.used`, `gpu.vram.free` | GB | |
| `gpu.vram.percent` | % | |
| `gpu.fan.rpm`, `gpu.fan.percent` | RPM, % | |

## CPU

| Key | Unit | Notes |
|---|---|---|
| `cpu.temp` | °C | Tctl/Tdie on AMD, package on Intel (needs PawnIO) |
| `cpu.load` | % | Same calculation as Task Manager |
| `cpu.power` | W | Package power (needs PawnIO) |
| `cpu.clock` | GHz | Average core clock |

## Motherboard and cooling

| Key | Unit | Notes |
|---|---|---|
| `mb.temp`, `chipset.temp` | °C | Need HWiNFO or a [mapping](#mapping-board-sensors) |
| `coolant.temp` | °C | Only if your AIO or board has a coolant sensor |
| `fan.cpu` | RPM | Automatic on Nuvoton boards (fan input #2) |
| `fan.pump` | RPM | |
| `fan.chassis1` | RPM | Automatic on Nuvoton boards (fan input #1) |
| `fan.chassis2`, `fan.chassis3` | RPM | Need HWiNFO or a mapping |

### Mapping board sensors
Motherboards name their inputs generically (`Fan #1`, `Temperature #2` …), and which header is which differs from board to board. **Settings → Sensor mapping** lets you point every key in the table above at a specific input; each input is listed with its live reading, so you can match it against what the BIOS shows. A mapping wins over HWiNFO and the automatic guesses.

## Memory and storage

| Key | Unit | Notes |
|---|---|---|
| `ram.used`, `ram.free` | GB | |
| `ram.percent` | % | |
| `disk.temp` | °C | First drive (same as `disk1.temp`) |
| `disk.used.percent` | % | First drive (same as `disk1.used.percent`) |
| `disk.read`, `disk.write` | MB/s | All drives together |
| `disk1.name` … `disk4.name` | text | Up to four drives, in the order Windows lists them |
| `disk1.temp` … `disk4.temp` | °C | |
| `disk1.read`, `disk1.write` … | MB/s | |
| `disk1.used.percent` … | % | |

## Network

Physical adapters are added together (virtual adapters and VPNs are left out).

| Key | Unit | Notes |
|---|---|---|
| `net.down`, `net.up` | MB/s | |
| `net.down.mbit`, `net.up.mbit` | Mbit/s | |
| `net.down.auto`, `net.up.auto` | text | Picks the unit: `850 KB/s`, `12.4 MB/s` |
| `net.total.down`, `net.total.up` | GB | Since the app started |
| `net.ping` | ms | Set a host in **Settings → Telemetry** first; pinged every 5 s |

## System

| Key | Example |
|---|---|
| `sys.uptime` | `3d 04:12` (text) |
| `sys.uptime.hours` | 76.2 |

## Games (RivaTuner Statistics Server)

| Key | Unit | Notes |
|---|---|---|
| `game.fps` | FPS | The game in the foreground, otherwise the most recent one |
| `game.frametime` | ms | |
| `game.fps.min` | FPS | Lowest over the last minute |
| `game.name` | text | Process name |

## Now playing and audio

| Key | Notes |
|---|---|
| `media.title`, `media.artist`, `media.album` | From Windows' media controls (Spotify, browsers, most players) |
| `media.app` | The app that's playing |
| `media.status` | ▶ or ⏸ |
| `audio.level`, `audio.bass`, `audio.mid`, `audio.treble` | 0–100 %, what the PC is playing right now |

The album cover is an *Image* widget with the file `media:cover`. Audio is only measured while a theme on the screen uses it; nothing is recorded.

## Weather

Needs a place in **Settings → Weather**. Temperatures follow the °C / °F choice there.

| Key | Unit | Notes |
|---|---|---|
| `weather.temp`, `weather.feels` | ° | Now, and "feels like" |
| `weather.temp.max`, `weather.temp.min` | ° | Today |
| `weather.humidity` | % | |
| `weather.wind` | km/h | |
| `weather.pressure` | hPa | |
| `weather.precip` | % | Chance of rain |
| `weather.code` | | Conditions, for the *Weather icon* widget |
| `weather.desc` | text | "Light rain" (in the UI language) |
| `weather.city` | text | The place's name |
| `weather.sunrise`, `weather.sunset`, `weather.updated` | text | Times |
| `weather.h1.*` … `weather.h6.*` | | Forecast every 3 hours (+3 h … +18 h): `.time`, `.temp`, `.code`, `.precip` |
| `weather.d1.*` … `weather.d3.*` | | The next three days: `.day`, `.max`, `.min`, `.code`, `.precip` |

## Time

| Key | Example |
|---|---|
| `clock.time` | 13:50:22 |
| `clock.time.short` | 13:50 |
| `clock.date` | 31.10.2026 |
| `clock.day` | SATURDAY (in the UI language) |

## Raw sensors

Besides the keys above, every reading is available under its own name:

- **`lhm:<hardware>/<type>/<name>`**: everything LibreHardwareMonitor sees, listed in the editor under *LHM · …*. Example: `lhm:Nuvoton NCT6798D/Fan/Fan #3`.
- **`hwi:<sensor name>`**: everything HWiNFO reports, if it runs, listed under *HWiNFO · …*. Duplicates get ` (2)`, ` (3)` …. Example: `hwi:CPU Package Power`.

Pick raw sensors in a widget's *Sensor* field, or use them in label text like any other key: `{lhm:Nuvoton NCT6798D/Fan/Fan #3} RPM`.

To list everything LibreHardwareMonitor finds on your PC, run this in an administrator terminal:

```powershell
& "$env:ProgramFiles\RigCanvas\RigCanvas.exe" sensors
```
