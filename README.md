# p4-flightdeck-ota

Firmware releases for a Waveshare ESP32-P4 7" flight-deck build. The deck
updates itself over Wi-Fi: on boot it reads `fw.txt`, compares `ver=` against the
running image, and pulls `firmware.bin` into the inactive OTA slot.

## Two assets per release

| asset | content |
| --- | --- |
| `firmware.bin` | the app image, flashed to `ota_0`/`ota_1` |
| `fw.txt` | `ver=` / `size=` / `md5=` — the manifest the deck reads first |

`releases/latest/download` always points at the newest pair, so the deck can use
one base URL for the life of the project.

## Publishing from the build machine

```
python tools/publish_fw.py            # copies the build + writes _data/fw.txt
python tools/publish_release.py       # creates/updates the GitHub release
```

Bumping `FDK_FW_VER` in `main/fw_ver.h` is mandatory: an identical version
string makes the deck skip the download.
