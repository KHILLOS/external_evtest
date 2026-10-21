# Modification Map: external/evtest

## Source: BlissOS android-x86 reference (external/evtest)
- BlissOS commit: e445e61 (hmtheboy154, 'Adding Android.mk to build on Android')
- UPSTREAM commit: bd4c587 (KhillOS port)
- Upstream base: freedesktop libevdev/evtest@evtest-1.36 (tag 96e6cb5)

## Modifications Applied to UPSTREAM/external_evtest (khillos-17 branch)

### 1. Android.bp Build System (NEW - replaces Android.mk)
**File:** `Android.bp` (entire file)
- Migrated from BlissOS Android.mk (make-based) to Soong Android.bp
- `cc_binary` for evtest with same cflags
- Package-level license configuration (GPL-2.0-or-later)
- **FIXED:** Removed `vendor_available: true` (evtest is a diagnostic tool, not vendor partition)

### 2. AOSP 17 Compliance Metadata Files (NEW)
**Files:** `METADATA`, `NOTICE`, `MODULE_LICENSE_GPL2`, `OWNERS`
- METADATA: Package metadata per AOSP external_updater format
- NOTICE: Short license notice
- MODULE_LICENSE_GPL2: SPDX identifier for Soong license module
- OWNERS: Standard AOSP OWNERS file

### 3. SPDX Header to Source File
**File:** `evtest.c`
- Added `/* SPDX-License-Identifier: GPL-2.0-or-later */` after first comment block

## Summary
- **Total files modified:** 6 (4 new metadata + 1 Android.bp + 1 SPDX header)
- **Source files unchanged:** Yes (only SPDX header added)
- **Logic/behavior changes:** None
- **Build system changes:** Android.mk → Android.bp migration (functional equivalent)
- **FIX:** Removed incorrect `vendor_available: true` from Android.bp