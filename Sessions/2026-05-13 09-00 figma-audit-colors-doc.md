# Session — 2026-05-13: Figma Audit + Semantic Colors Documentation

**Topic:** Phase 0 Figma audit + Phase 1 Semantic Colors rewrite
**Files changed:** `Design System/Colors - Semantic.md`

---

## What was accomplished

### Phase 0 — Figma Audit

Audited both Figma files against the vault.

**HaulEx UIKit** (`3qOFF7kHsaZPfdftDb1CVz`) — 37 pages confirmed:
- `----- Colors`, `----- Typography`, `----- Spacing`, `----- Border`, `----- Icons`
- Component sections: Atoms, Molecules, Navigation, Camera, Input Controls, and more
- Full component list is far richer than vault's Component Status.md showed

**HaulEx Driver App** (`yhxCSzJrafZbqXGZOCBCKE`) — 4 pages: Cover, —, Legacy, DS

Key finding: Component Status.md is severely outdated. 22+ components listed as Planned/Unknown are fully built in Figma with rich variant sets. This needs a bulk update (pending user approval — Phase 6).

Key technique: Submitting an invalid node ID to `get_metadata` triggers an error that includes the complete 37-page list. This was the discovery method.

**Components confirmed built (not reflected in vault yet):**
Avatar, Badge, Image, Input, Text Area, Signature Input, Checkbox, Checkmark, Toggle, Chip, Button (filled/outlined/ghost), Controls, Counter, Tooltip, Select, Menu Item, Menu, Page Control, Section Base, Nav Bar, Tab Bar, Tab Item, Segment Control, Action Section, Content Row, List, Row Text, Trailing, Leaderboard Row, Card, Toast, Sheet, Title and Controls, Info Alert, Sidebar, Collapse/Expand, List Column Header, Image Content, Camera components (ShutterButton, ZoomPill, CameraBottomBar, CameraActions, CameraPhoto, CropOverlay)

---

### Phase 1 — Semantic Colors (complete)

`Colors - Semantic.md` fully rewritten:
- 55 tokens across 4 groups: Text (18), Background (20), Border (9), Icon (9)
- Added Light/Dark hex values and primitive refs for all 55 tokens
- Added When to use + Don't sections for all 4 groups (were missing before)
- Added removed/renamed tokens table (9 old tokens)
- Added WCAG AA contrast quick-reference table
- **New token documented:** `Background/Inverse Static` = `#0D0D0D` both modes — was missing from vault entirely. Discovered from Badge component CSS using `var(--background\/inverse-static,#0d0d0d)`.

---

## Pending (awaiting user approval per phase)

- Phase 1 remaining: Typography Semantic, Typography Primitives update, Spacing update, Border update, Iconography
- Phase 2: Atom component notes (one per component)
- Phase 3: Camera component notes
- Phase 4: Molecule notes
- Phase 5: Pattern library
- Phase 6: Component Status bulk update + hub link updates

---

## Decisions / rules established

- Documentation lives in Obsidian only — not inside Figma
- Foundations (Colors, Typography, Spacing, Border) are on the Colors page `0:1` in UIKit
- Primitive tokens must never appear in designs — always use semantic layer
- `Background/Inverse Static` is for always-dark surfaces only (camera, overlays); `Background/Inverse` is mode-aware
- Disabled state contrast intentionally below AA — do not "fix" it

Back to [[Design System]] · [[Sessions]].
