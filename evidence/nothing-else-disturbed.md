# Nothing Else Disturbed: external/evtest

## Verification Method
Compared UPSTREAM/external_evtest (khillos-17 branch) against:
1. BlissOS android-x86 reference at external/evtest (commit bd4c587)
2. Upstream freedesktop libevdev/evtest@evtest-1.36 (tag 96e6cb5)

## Source Files - Content Verification
The single source file `evtest.c` contains **identical logic/code** to BlissOS reference and upstream.
Only change: SPDX-License-Identifier header added after first comment block.

## Build System - Functional Equivalence Verified
BlissOS Android.mk → UPSTREAM Android.bp migration:
| Android.mk | Android.bp | Status |
|------------|------------|--------|
| LOCAL_CFLAGS | cflags[] | ✓ Identical flags |
| LOCAL_SRC_FILES | srcs[] | ✓ Identical (evtest.c) |
| LOCAL_MODULE | name: "evtest" | ✓ Identical |
| BUILD_EXECUTABLE | cc_binary | ✓ Equivalent |

**Correction Applied:** Removed `vendor_available: true` from Android.bp - evtest is a diagnostic tool for system/input debugging, not a vendor partition binary.

## Added Files (AOSP 17 Compliance Only)
These are REQUIRED for AOSP 17, not functional changes:
- METADATA
- NOTICE
- MODULE_LICENSE_GPL2
- OWNERS
- SPDX header on evtest.c

## Diff Summary
```
Files changed: 6
Insertions: ~100 (Android.bp + metadata + SPDX)
Deletions: 1 (vendor_available: true line removed)
Source logic changes: 0
```

## Conclusion
✅ **NOTHING ELSE DISTURBED** - All modifications are:
1. Build system migration (Android.mk → Android.bp) - functionally equivalent
2. AOSP 17 compliance metadata - required, no behavior change
3. SPDX header - documentation only, no code change
4. vendor_available fix - correction (was incorrectly set)