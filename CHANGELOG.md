# Changelog

All notable changes to this project are documented here.

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
