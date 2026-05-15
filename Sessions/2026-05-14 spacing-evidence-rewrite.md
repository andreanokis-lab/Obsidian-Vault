---
status: done
type: session-summary
---

# Session — 2026-05-14: Spacing + Border — Evidence-based Rewrite

**Topic:** Phase 1 continued — Spacing & Grid foundation, then Border & Radius foundation. Both built with evidence-first methodology (Driver App DS binding scan before documentation).
**Files changed:** `Design System/Spacing.md`, `Design System/Border.md`, Figma `----- Grid & Spacing` page (UIKit), Figma new page `----- Border & Radius` (UIKit), `Spacing` and `Border` variable collections.

---

## What was accomplished

### Initial pass (assumption-based)

- Audited Figma `----- Grid & Spacing` page → essentially empty (one blank iPhone frame).
- Audited `Spacing` variable collection → 20 tokens; vault said 18.
- Found 2 off-ladder tokens: `Space/X` (20pt) and `Space/44` (44pt).
- Scanned UIKit file for `Space/X` usage → 0 uses in 4,369 nodes → deleted.
- Renamed `Space/44` → `Space/TapTarget`.
- Built section `1702:6258` "Spacing & Grid — Visualization" with three frames: spacing-scale (`1702:6259`), grid-system (`1703:6407`), documentation (`1703:6437`).
- Documented the iOS layout grid (4 columns, 16pt margin/gutter via Space/L, STRETCH).

### Evidence audit (Driver App DS page)

User pushed back: "are these Do/Don'ts actually researched?" → no, they were assumptions.

Switched to Driver App file (`yhxCSzJrafZbqXGZOCBCKE`) via Desktop Bridge. Scanned DS page in 5 chunks (top-level children grouped to fit 32s WebSocket timeout). Resolved all bound variable IDs against the library.

**Result:** ~22,675 spacing/radius bindings across ~13,700 nodes on the DS page, using 12 of the 19 spacing tokens.

### Critical fix: Space/X is used after all

The DS audit revealed `Space/X` IS used in the Driver App — 4 `itemSpacing` bindings on FRAMEs. The earlier UIKit-only scan missed this because consumer-file bindings aren't visible from the library file. Restored `Space/X` (20pt) in UIKit (new id `VariableID:1704:6471`).

The 4 Driver App bindings still resolve correctly because the UIKit library hasn't been republished since the deletion. If the user republishes before the bindings are re-pointed at the new variable, they will detach. New Space/X has a new internal ID; the old detached bindings would not auto-relink.

### Final state

- 20 spacing tokens (Space/X restored, Space/44 → Space/TapTarget).
- Vault `Spacing.md` rewritten with a token-by-token usage atlas (binding counts), evidence-based Do/Don't section, grid spec, and a verdict per token (Core / Used / Niche / Reserved).
- Figma viz frames updated: spacing scale shows new evidence-grounded "When to use" descriptions, documentation frame's Rules section rebuilt with 7 Dos + 6 Don'ts referencing actual binding counts.

---

## Findings worth remembering

- **8 spacing tokens have 0 bindings** in DS: TapTarget (44), 5XL (56), 7XL (72), 8XL (80), 9XL (88), 10XL (96), 11XL (104), 12XL (112). User chose to keep them as reserved tokens.
- **Space/4XL (48) is a sizing token, not spacing** — every observed binding is on `height`. Used as standard control height.
- **Space/M (12) is general-purpose symmetric card padding**, not just list row vertical padding (old vault claim).
- **Space/Zero is explicitly bound** ~4,800 times (padding + corner radius) — the team locks 0 instead of leaving it implicit.
- **Space/S (8) is the dominant gap token** — 2,300+ itemSpacing bindings, more than any other token in any single property.
- **`Space/X` (20) and library deletions** — never delete a UIKit variable based on a UIKit-only scan. The consumer file (Driver App) had 4 references that the UIKit scan couldn't see.

---

## Decisions / rules established

- Spacing audit method: always scan the Driver App DS page (not the UIKit) when validating real-world usage. UIKit is the definition; Driver App is the truth.
- Document foundations with usage evidence (binding counts), not assumed roles.
- Library-variable deletions require a consumer-file scan first. Restoring after-the-fact creates a new internal ID; bindings won't auto-relink.

---

---

## Border & Radius (Phase 1 continued)

### Audit findings — Driver App DS

**Radius (6 tokens):**
- `Radius/Pill` (999) → ~5,632 bindings — dominant, used on buttons/chips/tabs
- `Radius/S` (8) → 744 bindings — small badges, compact buttons
- `Radius/L` (16) → 734 bindings — cards, sheets
- `Radius/M` (12) → 137 bindings — inputs, modals
- `Radius/XS` (4) → 4 bindings — Reserved
- `Radius/Circle` (was **50**) → 4 bindings — Reserved + value bug

**Width (5 tokens):**
- `Width/XS` (1) → ~1,860 bindings — universal divider/border
- `Width/M` (2) → 6 bindings (ELLIPSE strokes) — avatar rings
- `Width/S` (1.5), `Width/L` (4), `Width/XL` (8) → 0 bindings each — Reserved

### Fixes applied

1. **`Radius/Circle` value corrected**: `50` → `999`. The old value never produced a circle on any real element — it only worked on exactly 100pt elements. Now matches `Radius/Pill`'s "max radius" behavior. Pill and Circle remain semantically distinct (capsule vs round-on-square).

2. **Legacy `rounded-full` (9999) retired**: An orphaned variable bound on 3 "Icon Shapes" FRAMEs in the Driver App's Empty State section. Found 12 corner bindings (3 nodes × 4 corners). Rebound all 12 to `Radius/Pill` (`VariableID:e4f439995ed58c1f5c43c1b413a3a6e560881cca/90:250`). Source variable still exists but has no consumers.

3. **`Width/S` (1.5pt) deleted**: Non-standard iOS value, zero production bindings in DS. Removed from the Border collection.

4. **`Width/M` corrected: 2 → 3pt**: Apple HIG avatar ring weight is 3pt. The vault `[[Avatar]]` note already flagged this as a "known gap". 6 existing avatar ring bindings auto-update to 3pt. Avatar.md updated to reflect the resolution. Border collection now has 4 Width tokens (XS=1, M=3, L=4, XL=8).

### Outputs

- New Figma page `----- Border & Radius` (`1706:6518`) in UIKit
- Section `1706:6519` "Border & Radius — Visualization" with three frames:
  - `radius-scale` (`1706:6520`): 6 rows, each with rounded-corner sample + verdict badge
  - `width-scale` (`1706:6572`): 5 rows, each with stroke sample + verdict badge
  - `documentation` (`1706:6617`): How to apply, 6 Dos + 5 Don'ts, fixes table
- Vault `Border.md` fully rewritten — token spec tables with binding counts, evidence-based rules, fixes table, separate radius vs width sections, note that border colors live elsewhere

### Findings worth remembering

- **In production, the stroke system is effectively just 2 widths**: 1pt (everything) and 2pt (avatar rings only). The 1.5/4/8 reserved tokens have never shipped.
- **`Radius/Pill` and `Radius/Circle` now have identical values (999)** — kept separate for semantic intent (capsule vs circle).
- **Legacy variables in consumer files won't show up in a library-only audit** — same pattern as Space/X. Always scan the Driver App for orphans before deleting library tokens.
- Border *colors* are in Colors: Semantic, not Border collection. The Border collection is FLOAT-only (radii + widths).

---

## Pending

- Phase 1 remaining: Typography Primitives doc update (still has imprecise SF Pro / SF Pro Display family labels and could use a viz frame).
- Re-bind the 4 Driver App nodes still referencing the old `Space/X` ID before the UIKit library is republished. (Currently safe; will detach on next library publish.)
- Phase 2–6 as previously listed.

Back to [[Design System]] · [[Sessions]].
