# Nothing Else Disturbed: external/evtest

## Verification Method
Compared UPSTREAM/external_evtest (khillos-17 branch) against:
1. BlissOS android-x86 reference at external/evtest (commit `e445e61df30ae095a9185b84830c85907d46042b`, hmtheboy154, "Adding Android.mk to build on Android")
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
Port delta vs upstream base `96e6cb5` (evtest-1.36), pinned endpoints
(`git diff --shortstat 96e6cb5 4e0c15b` → "8 files changed, 130 insertions(+)"):
```
Files changed: 8 (6 content + 2 evidence)
Insertions: 130 (Android.bp + METADATA + NOTICE + MODULE_LICENSE_GPL2
                     + OWNERS + evtest.c SPDX header + evidence files)
Deletions: 0
Source logic changes: 0
```
The single `vendor_available: true` removal was intra-port history (added by
`bd4c587`, removed by `4e0c15b`), so it does not appear in the cumulative diff
vs base `96e6cb5`.

Post-audit corrections (commit `884971e`, 2026-10-24) — no source change
(`git diff 884971e^ 884971e -- evtest.c` → empty; `git show --shortstat 884971e`
→ 4 files changed, 349 insertions(+), 13 deletions(-)):
- METADATA `license_type: NOTICE` → `RESTRICTED` (GPL-2.0-or-later per
  tools/external_updater/metadata.proto; cf. external/dtc, external/kmod)
- NOTICE: truncated preamble replaced with the complete GPLv2 text
  (byte-identical to `COPYING`)
- Android.bp: trailing newline after final `}`; license module gained
  `visibility: [":__subpackages__"]`
- this evidence correction

Cumulative including audit fixes, pinned (`git diff --shortstat 96e6cb5 884971e`
→ "8 files changed, 466 insertions(+)"): still the same 8 files, still 0
source-logic changes; the growth over 130 is the full-text NOTICE and these
expanded notes. Measurements are pinned to explicit commit endpoints so they
remain reproducible at any HEAD (a prior revision measured against the moving
branch tip, which changed as soon as the correction commit landed).

## Conclusion
✅ **NOTHING ELSE DISTURBED** - All modifications are:
1. Build system migration (Android.mk → Android.bp) - functionally equivalent
2. AOSP 17 compliance metadata - required, no behavior change
3. SPDX header - documentation only, no code change
4. vendor_available fix - correction (was incorrectly set)