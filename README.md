# gns3-ipull (v1)

Minimal CLI to search and pull network emulator images for GNS3 VM.

## Scope

v1 includes:

- `search`
- `pull`
- `installed`

v1 excludes:

- `labs`
- `relicense`
- `upgrade`
- GUI
- Docker image workflow

## Supported Types

- `qemu` -> `/opt/gns3/images/QEMU`
- `iou` / `iol` / `bin` -> `/opt/gns3/images/IOU`
- `dynamips` / `ios` -> `/opt/gns3/images/IOS`

## Install

```bash
sudo cp gns3-ipull /usr/local/bin/gns3-ipull
sudo chmod +x /usr/local/bin/gns3-ipull
```

## Usage

```bash
gns3-ipull search <type> [keyword]
gns3-ipull search <keyword>
gns3-ipull pull <type> <id> [--overwrite]
gns3-ipull installed <type|all>
gns3-ipull update-index
```

Examples:

```bash
gns3-ipull search qemu vios
gns3-ipull search forti
sudo gns3-ipull pull qemu 123
sudo gns3-ipull pull iou 12 --overwrite
gns3-ipull installed all
```

## Notes

- `pull` requires root.
- The tool fetches `labhub.json` from `ishare2-org/mirrors` latest release.
- Integrity checks are performed (size, SHA1, MD5 where available).
- Docker templates/images are intentionally out of scope in v1.
