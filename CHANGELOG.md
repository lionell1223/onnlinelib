# ECLIPSE MODULE [LOGS]
---

## [v1.0.0] — 2026-11-16

### Initial release

### Added
- Eclipse core loader for CODM Garena (arm64).
- Magisk module structure with standard installer (`update-binary` / `updater-script`).
- Custom ASCII banner on flash.
- `module.prop` with Eclipse branding (name, author, description).
- Online update support via `updateJson`.
- `banner.png` module card for Magisk manager.
- Optional `icon.png` for manager display.
- `update.json` with `zipUrl` + `changelog` pointers.
- License panel · ESP · Aim · Memory · Hide root / UBL process mask.

### Compatibility
- Magisk v24+.
- arm64-v8a only.
- CODM Garena build target 1.6.59 GR.

### Known limitations
- No armv7 / x86 support yet.
- Banner shown only during flash, not in-module.

---

## Format

`[version] — YYYY-MM-DD`
Sections: `Added`, `Changed`, `Fixed`, `Removed`, `Compatibility`, `Known limitations`.
