# ECLIPSE MODULE — Changelog

All notable changes to this module are documented here.

---

## [v6.0.3] — 2026-11-22

### Added
-drag handle at bottom of screen — pull up to open menu, push down to close.
- Stream Proof toggle in Settings — ESP hides instantly when enabled.

### Changed
- Menu redesigned as a bottom sheet with live FPS in header.

### Fixed
- Key input reachable on first launch.
- Ghost overlay left after disabling Stream Proof.

### Compatibility
- Magisk v24+ (Zygisk required).
- arm64-v8a only.
- CODM build target.

### Known limitations
- No armv7 / x86 support yet.

---

## [v1.0.0] — 2026-11-16

### Initial release

### Added
- Zygisk core (`zygisk/arm64-v8a.so`) with Eclipse loading pipeline.
- Magisk module structure with standard installer (`update-binary` / `updater-script`).
- Custom ASCII banner on flash.
- `module.prop` with Eclipse branding (name, author, description).
- Online update support via `updateJson`.
- `banner.png` module card for Magisk manager.
- Optional `icon.png` for manager display.
- `update.json` with `zipUrl` + `changelog` pointers.

### Compatibility
- Magisk v24+ (Zygisk required).
- arm64-v8a only.
- CODM build target (as designed).

### Known limitations
- No armv7 / x86 support yet.
- Banner shown only during flash, not in-module.

---

## Format

`[version] — YYYY-MM-DD`
Sections: `Added`, `Changed`, `Fixed`, `Removed`, `Compatibility`, `Known limitations`.
