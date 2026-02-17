# Changelog

All notable changes to this project are documented here.

## [1.1.0] - 2026-02-17

### Added
- Docker support for `search`, `pull`, and `installed`.
- `pull iou/iol` warning when license fields appear missing in GNS3 controller config.

### Changed
- Version bumped to `1.1.0`.
- Cross-type search now includes Docker entries when present in index data.
- Type-specific search now safely handles missing sections in index data.

## [1.0.0] - 2026-02-17

### Added
- `license-check` command to validate IOU/IOL license fields in GNS3 controller config.
- `cleanup` command to remove stale `.gns3-ipull-*` staging directories.
- `SMOKE_TEST_CHECKLIST.md` for release verification workflow.

### Changed
- Version bumped to `1.0.0`.
- QEMU pull flow normalizes extracted disk images to top-level files in `/opt/gns3/images/QEMU`.
- URL-encoded filenames are decoded during install.
- `.md5sum` sidecar payload files are skipped during installation.
- Pull output now includes installed file paths and clearer post-install guidance.
