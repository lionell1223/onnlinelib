
# ECLIPSE MODULE — Changelog

---

## [5.0.2] — 2026-11-19

### Added
- Volume Up and Volume Down both open and close the menu. Either button works.

### Changed
- Menu Settings tab streamlined — key status panel, re-verify button, and footer removed.
- Key verification now reports the real reason when it fails instead of looping back to "not found".

### Fixed
- Key file sometimes not being created on first launch.
- Device ID regenerating every session on fresh installs, causing valid keys to fail.
- Hide Stream making the menu itself invisible while active.
- Ghost overlay left on screen after turning Hide Stream off.

### Removed
- Unused key-type and expiry tracking.

### Compatibility
- Magisk v24+ (Zygisk required).
- arm64-v8a only.
- CODM build target.
