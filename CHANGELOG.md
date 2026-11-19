# ECLIPSE MODULE — Changelog

All notable changes to this module are documented here.

---

## [5.0.2] — 2026-11-19

### Added
- Volume button toggle — Volume Up and Volume Down both open/close the menu via `AInputQueue_getEvent` hook in `libandroid.so`. Either key works, so a device where one is intercepted still has a working entry point.
- `EnsureKeyDir()` helper — creates `files/key/` via direct `mkdir(2)` syscalls instead of shelling out.
- `SaveKey()` helper — writes `key.txt` and returns write success/failure to the UI.

### Changed
- Keysystem JNI rewritten — every `FindClass` / `NewString` / `NewByteArray` now has a matching `DeleteLocalRef`, every `Call*Method` gets an `ExceptionCheck` + clear, method IDs are null-checked. No pending JNI exceptions carried across calls.
- `Init_Thread` simplified — redundant `bValid = false; g_KeyType.clear(); g_KeyExpiry = 0; g_LoginError.clear();` block collapsed to a single `LoadKey();` since `LoadKey` resets state internally.
- Menu "Verify" button now calls `SaveKey()` and reports `"Failed to write key file"` if the write fails, instead of silently looping back to "key.txt not found".
- Removed the Key Status panel, Re-verify Key button, and module/target/key footer from the Settings tab.
- Removed lifetime branch and `rng` timestamp-window check from `ValidateKey` — auth is now a straight server-response token comparison.

### Fixed
- `"key.txt not found"` intermittent bug — caused by `system("mkdir -p ...")` failing silently on some ROMs (SELinux, no shell, exec denied), so `fopen(path, "w")` returned null and the write never happened. Replaced with direct `mkdir` per path segment, with the same pattern in `GetDeviceID`.
- `device_id.txt` regenerating every session on fresh installs — `ofstream` was writing to a parent directory that didn't exist, silently failing, so a new random ID was generated each boot and tokens never re-validated. Parent dir now created before write.
- Hide Stream not activating when the menu closed — the render path was routing *all* draw data through `ZEL_Render` regardless of menu state, making the menu itself invisible and unusable while the toggle was on. Now gated with `hidingNow = hideStream && !isToggled` so the hidden `SurfaceControl` path only fires while the menu is closed.
- Ghost secure surface left on the compositor after untoggling Hide Stream — `ZEL_Shutdown()` now fires when transitioning out of the hiding state, applying a `remove()`/`hide()` transaction to the SurfaceControl and dropping all refs.

### Removed
- `g_Auth`, `g_Token`, `g_KeyType`, `g_KeyExpiry` globals — moved to locals inside `ValidateKey` or deleted where dead.
- Legacy `system()` calls for directory creation.
- Unused `JsonGetInt64` call for the `expiry` field (nothing reads it since the Key Status panel was removed).

### Compatibility
- Magisk v24+ (Zygisk required).
- arm64-v8a only.
- CODM build target (`com.garena.game.codm`).

### Known limitations
- No armv7 / x86 support yet.
- Hide Stream relies on `ActivityThread.mActivities` reflection — on ROMs that block it, `ZEL_Render` falls back to the normal surface and the overlay stays visible to capture, with no error surfaced to the UI.
- Client-side `rng` timestamp anti-replay check removed — server must enforce response freshness.
- `isToggled` is a plain `bool` shared across threads (input thread writes, GL thread reads). Works on ARM64 aligned stores; theoretically UB under the C++ memory model.

---

## [1.0.0] — 2026-11-16

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
