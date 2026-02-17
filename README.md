# gns3-ipull (v1.0.0)

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

Install directly from GitHub using `wget`:

```bash
sudo wget -O /usr/local/bin/gns3-ipull "https://raw.githubusercontent.com/Khang-Phung-0812/gns3-ipull/main/gns3-ipull" && sudo chmod +x /usr/local/bin/gns3-ipull && gns3-ipull --help
```

Install from a local clone:

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
gns3-ipull license-check
sudo gns3-ipull cleanup
```

Examples:

```bash
gns3-ipull search qemu vios
gns3-ipull search forti
sudo gns3-ipull pull qemu 123
sudo gns3-ipull pull iou 12 --overwrite
gns3-ipull installed all
gns3-ipull license-check
sudo gns3-ipull cleanup
```

## Notes

- `pull` requires root.
- The tool fetches `labhub.json` from `ishare2-org/mirrors` latest release.
- Integrity checks are performed (size, SHA1, MD5 where available).
- URL-encoded filenames are decoded on install (for example `%5B` -> `[`).
- `.md5sum` sidecar payload files are skipped.
- QEMU pulls are normalized to top-level disk files in `/opt/gns3/images/QEMU` so they are visible in template creation.
- `license-check` validates whether IOU/IOL license fields are present in `gns3_controller.conf`.
- `cleanup` removes stale `.gns3-ipull-*` staging directories.
- Docker templates/images are intentionally out of scope in v1.
