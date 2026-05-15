---
status: done
type: session-summary
---

# Session — 2026-05-13: Typography Semantic — Figma Build + HIG Review

**Topic:** Phase 1 continued — Typography Semantic documentation + Figma frames + HIG compliance audit
**Files changed:** `Design System/Typography - Semantic.md`, Figma `----- Typography` page

---

## What was accomplished

### Background/Secondary Figma variable fixes (carried from previous session)

Renamed 4 variables in `Colors: Semantic` collection and fixed light-mode alias values:
- `Background/Secondary Blue` → `Background/Subtle Blue` (alias already correct: blue/100)
- `Background/Secondary Green` → `Background/Subtle Green` + light alias green/400 → green/100 (`VariableID:63:88`)
- `Background/Secondary Red` → `Background/Subtle Red` + light alias red/200 → red/100 (`VariableID:63:79`)
- `Background/Secondary Yellow` → `Background/Subtle Yellow` + light alias yellow/400 → yellow/100 (`VariableID:63:106`)

---

### Typography Semantic — vault rewrite

`Typography - Semantic.md` fully rewritten from a basic 3-column table to a comprehensive spec:
- Added iOS primitive mapping column
- Added letter-spacing for all 10 roles
- Corrected 3 size values: Text/Secondary, List/Subtitle, Form/Label all 16pt → 15pt
- Added Text/Secondary mixed-primitive footnote (*)
- Added Text/Footnote 1:1 LH footnote (†)
- Added When to use (expanded), Don't section (7 rules), Quick lookup table
- Added visualization frame reference: node `1698:3169`

---

### Figma visualization frame — node `1698:3169`

Created on `----- Typography` page, section "Semantic Typography — Visualization":
- x=1500, y=−500; section 1120×1476, inner `doc` frame 960×1396
- 10-row reference table; columns: meta (220px) | live-styled sample (460px) | spec (220px)
- 6 group separators: SCREEN, SECTION, TEXT, LIST, FORM, META
- Live text styles applied via `setTextStyleIdAsync`
- HaulEx-specific sample strings (real content, not lorem ipsum)

---

### Figma documentation frame — node `1698:3320`

Created adjacent to visualization (x=1175, y=0, 1040×2671):
- Header block
- How to apply section
- 10 role cards (name + spec + When/Don't)
- 9 system rules (✅/⛔)
- 12-row quick lookup table

---

### HIG compliance audit

See findings below.

---

## HIG compliance findings

| Token | HaulEx | HIG standard | Verdict |
|---|---|---|---|
| `Screen/Title` | 17pt Semibold, LH 22, LS −0.43 | Headline: 17pt Semibold, LH 22, LS −0.43 | ✅ Match (family label imprecise) |
| `Section/Title` | 20pt Regular, LH 25, LS +0.38 | Title 3: 20pt Regular, LH 25, LS +0.38 | ✅ Match |
| `Text/Body` | 17pt Regular, LH 22, LS −0.408 | Body: LS −0.43 | ⚠️ LS rounding (~0.02pt) |
| `Text/Secondary` | **15pt** Regular, LH 21, LS −0.32 | Callout: **16pt** Regular, LH 21, LS −0.32 | ❌ Hybrid: Subheadline size + Callout metrics |
| `Text/Footnote` | 13pt Regular, LH **13** | Footnote: 13pt Regular, LH **18** | ❌ Intentional 1:1 LH — WCAG 1.4.12 risk |
| `List/Title` | 17pt Regular, LH 22, LS −0.408 | Body: LS −0.43 | ⚠️ Same rounding as Text/Body |
| `List/Subtitle` | 15pt Regular, LH 20, LS **−0.24** | Subheadline: LS **−0.45** | ⚠️ Notable LS deviation |
| `Form/Label` | 15pt Regular, LH 20, LS **−0.24** | Subheadline: LS **−0.45** | ⚠️ Same as List/Subtitle |
| `Form/Input` | 17pt Regular, LH 22, LS −0.408 | Body: LS −0.43 | ⚠️ Same rounding |
| `Meta/Caption` | 12pt Regular, LH 16, LS 0 | Caption 1: 12pt Regular, LH 16, LS 0 | ✅ Exact match |

**Critical:** `Text/Secondary` is not a valid HIG text style. It borrows Callout's LH and LS but uses Subheadline's size. The vault footnote (*) documents this but doesn't flag it as a decision to revisit.

**Intentional:** `Text/Footnote` 1:1 LH is documented as intentional for single-line hint/legal text only. WCAG 1.4.12 applies to body text; restricted use case may be defensible.

**Decisions / fixes applied:**
1. ✅ **`Text/Secondary` fixed** — rebound to clean Subheadline primitive: 15pt / LH 20 / LS −0.24. No size shift (kept 15pt), eliminated the Callout/Subheadline hybrid. Changes:
   - Figma var `Text/Secondary/Height` (`159:375`): alias Height/Callout → Height/Subheadline (`142:321`)
   - Figma var `Text/Secondary/Letter Spacing` (`159:376`): alias Letter Spacing/Callout → Letter Spacing/Subheadline (`142:332`)
   - Viz frame spec text + doc frame role card updated to match
   - Vault token spec row + footnote updated
2. ✅ **Subheadline primitive LS aligned to HIG** — `Letter Spacing/Subheadline` (`VariableID:142:332`) changed −0.24 → −0.45. Propagates automatically to `Text/Secondary`, `List/Subtitle`, `Form/Label`. Viz frame spec text updated. Also fixed `Typography - Primitives.md` Subheadline row: size 16 → 15 (vault doc bug — Figma always had 15) and LS to −0.450.
3. **Accepted as rounding noise:** LS −0.408 vs HIG −0.43 on Body-based tokens — 0.022pt diff, no action.
4. **Accepted as intentional:** `Text/Footnote` 1:1 LH — restricted to single-line hint/legal copy per existing Don't rule.

---

## Pending

- Camera token group: 5 undocumented tokens in Colors: Semantic — Controls Background, Icon Primary, Icon Secondary, Overlay, Surface
- Phase 1 remaining: Spacing, Border, Typography Primitives updates
- Phase 2–6 as previously listed

Back to [[Design System]] · [[Sessions]].
