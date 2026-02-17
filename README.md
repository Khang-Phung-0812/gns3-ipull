# gns3ipull (v1.1.2)

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
sudo wget -O /usr/local/bin/gns3ipull "https://raw.githubusercontent.com/Khang-Phung-0812/gns3-ipull/main/gns3-ipull" && sudo chmod +x /usr/local/bin/gns3ipull && gns3ipull --help
```

Install by cloning the repository:

```bash
git clone https://github.com/Khang-Phung-0812/gns3-ipull.git
cd gns3-ipull
sudo cp gns3-ipull /usr/local/bin/gns3ipull
sudo chmod +x /usr/local/bin/gns3ipull
```

## How To Use

1. Update the image index:

```bash
gns3ipull update-index
```

2. Search for images and note the ID:

```bash
gns3ipull search qemu vios
gns3ipull search iou
gns3ipull search dynamips c7200
```

3. Pull the image by type and ID:

```bash
sudo gns3ipull pull qemu <QEMU_ID>
sudo gns3ipull pull iou <IOL_ID>
sudo gns3ipull pull dynamips <DYNAMIPS_ID>
```

4. Verify installed files:

```bash
gns3ipull installed all
```

5. Validate IOU/IOL license state (recommended before using IOU nodes):

```bash
gns3ipull license-check
```

6. Create templates in GNS3:

- For QEMU: `New Template -> QEMU VM`, then select the installed disk image.
- For IOU/IOL: `New Template -> IOU Device`, then pick your pulled binary.
- For Dynamips: `New Template -> Dynamips IOS router`, then pick your pulled image.

7. Clean stale staging directories if needed:

```bash
sudo gns3ipull cleanup
```

## Command Reference

```bash
gns3ipull search <type> [keyword]
gns3ipull search <keyword>
gns3ipull pull <type> <id> [--overwrite]
gns3ipull installed <type|all>
gns3ipull update-index
gns3ipull license-check
sudo gns3ipull cleanup
```

Examples:

```bash
gns3ipull search qemu vios
gns3ipull search forti
sudo gns3ipull pull qemu 123
sudo gns3ipull pull iou 12 --overwrite
gns3ipull installed all
gns3ipull license-check
sudo gns3ipull cleanup
```

## Notes

- `pull` requires root.
- The tool fetches `labhub.json` from `ishare2-org/mirrors` latest release.
- Integrity checks are performed (size, SHA1, MD5 where available).
- URL-encoded filenames are decoded on install (for example `%5B` -> `[`).
- `.md5sum` sidecar payload files are skipped.
- QEMU pulls are normalized to top-level disk files in `/opt/gns3/images/QEMU` so they are visible in template creation.
- `pull iou` warns when IOU/IOL license fields appear missing.
- `license-check` validates whether IOU/IOL license fields are present in `gns3_controller.conf`.
- `cleanup` removes stale `.gns3-ipull-*` staging directories.

## Credits

- Original concept and ecosystem inspiration: [ishare2-cli](https://github.com/ishare2-org/ishare2-cli)
