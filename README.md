# gns3ipull

[![Version](https://img.shields.io/badge/version-1.1.5-2ea44f.svg)](./CHANGELOG.md)
[![Platform](https://img.shields.io/badge/platform-GNS3%20VM-1f6feb.svg)](https://www.gns3.com/)
[![Shell](https://img.shields.io/badge/language-bash-f59e0b.svg)](./gns3-ipull)

Minimal CLI to search, pull, manage, and verify network emulator images for GNS3 VM.

## Table Of Contents

- [Overview](#overview)
- [Supported Types](#supported-types)
- [Install](#install)
- [Quick Workflow](#quick-workflow)
- [Commands](#commands)
- [Examples](#examples)
- [Important Notes](#important-notes)
- [Credits](#credits)

## Overview

`gns3ipull` is focused on image operations for GNS3 VM:

- search indexed images
- pull and verify images
- list installed images
- validate IOU/IOL license presence
- cleanup stale staging folders
- delete installed images
- self-update the tool

Out of scope:

- labs automation
- relicense generation
- VM/server upgrade orchestration
- GUI
- Docker image workflow

## Supported Types

| Type Input | Internal Type | Install Path |
|---|---|---|
| `qemu` | `QEMU` | `/opt/gns3/images/QEMU` |
| `iou`, `iol`, `bin` | `IOL` | `/opt/gns3/images/IOU` |
| `dynamips`, `ios` | `DYNAMIPS` | `/opt/gns3/images/IOS` |

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

## Quick Workflow

1. Update index:

```bash
gns3ipull update-index
```

2. Update tool:

```bash
sudo gns3ipull update-self
```

3. Search and note image ID:

```bash
gns3ipull search qemu vios
gns3ipull search iou
gns3ipull search dynamips c7200
```

4. Pull by type and ID:

```bash
sudo gns3ipull pull qemu <QEMU_ID>
sudo gns3ipull pull iou <IOL_ID>
sudo gns3ipull pull dynamips <DYNAMIPS_ID>
```

5. Validate and inspect:

```bash
gns3ipull installed all
gns3ipull license-check
```

6. Optional maintenance:

```bash
sudo gns3ipull cleanup
```

Template creation in GNS3:
- QEMU: `New Template -> QEMU VM`
- IOU/IOL: `New Template -> IOU Device`
- Dynamips: `New Template -> Dynamips IOS router`

## Commands

| Command | Purpose |
|---|---|
| `gns3ipull search <type> [keyword]` | Search indexed images by type |
| `gns3ipull search <keyword>` | Search across supported types |
| `gns3ipull pull <type> <id> [--overwrite]` | Download and install image |
| `sudo gns3ipull delete [--id] <type> <name\|id> [--yes]` | Delete installed image(s) |
| `gns3ipull installed <type\|all>` | Show installed images |
| `gns3ipull update-index` | Refresh index cache |
| `sudo gns3ipull update-self` | Update tool from GitHub |
| `gns3ipull license-check` | Check IOU/IOL license config fields |
| `sudo gns3ipull cleanup` | Remove stale staging dirs |

## Examples

```bash
gns3ipull search qemu vios
gns3ipull search forti
sudo gns3ipull pull qemu 123
sudo gns3ipull pull iou 12 --overwrite
sudo gns3ipull delete qemu linux-kali-2018.1-amd64.qcow2 --yes
sudo gns3ipull delete --id qemu 872 --yes
gns3ipull installed all
sudo gns3ipull update-self
gns3ipull license-check
sudo gns3ipull cleanup
```

## Important Notes

- `pull`, `delete`, `update-self`, and `cleanup` require root.
- Index source: latest `labhub.json` release from `ishare2-org/mirrors`.
- Integrity checks include size, SHA1, and MD5 (when available).
- For `qcow/qcow2`, if indexed size differs but checksum passes, install continues with a warning.
- URL-encoded filenames are decoded on install (for example `%5B` -> `[`).
- `.md5sum` sidecar payload files are skipped during pull.
- `delete` also removes matching `.md5sum` sidecar files when present.
- QEMU pulls are normalized to top-level disk files in `/opt/gns3/images/QEMU`.
- `pull iou` warns if IOU/IOL license fields appear missing.
- `license-check` validates IOU/IOL license keys in `gns3_controller.conf`.

## Credits

- Original concept and ecosystem inspiration: [ishare2-cli](https://github.com/ishare2-org/ishare2-cli)
