# ECLIPSE MODULE — Changelog

All notable changes to this module are documented here.

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
