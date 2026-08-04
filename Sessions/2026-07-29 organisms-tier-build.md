---
type: session
date: 2026-07-29
project: HaulEx Web design system
vault: D:\Info-storage\HaulEx-Web\HaulEx-Web\
---

# Session — Organisms tier build (HaulEx **Web**, not Driver App)

> Note: this session was entirely about the **HaulEx Web** design system (`D:\CRM_V2` → Figma `Exr6OibRbgO7X9YeBka2EW`), whose vault is `D:\Info-storage\HaulEx-Web\HaulEx-Web\`. Logged here only because the session-log hook points at this folder.

## Topics
1. Reviewed the claimed atom status (13 done / 2 left) — found **Icon Button missing from Figma** despite `status: built`; rebuilt 120 variants.
2. Built the remaining atoms: Tooltip, Rating, Skeleton.
3. Built the **whole Molecules tier** — 15 sets, 114 variants, 4 sections.
4. Audited **all 12 Organism candidates** before building: **6 build · 4 drop · 2 defer**.
5. Built the **whole Organisms tier** — D0–D6, **9 sets / 26 variants**: Data Table · Modal · Confirm Dialog · Filter Bar · Search Results Panel · Dropzone · File List · Nav Rail · Utility Drawer.
6. Reorganised the Figma file from 22 → 13 pages; nested 12 spec boards with their sets.
7. Swept the library for missing text properties after the same defect appeared three times → **19 of 37 sets** affected.

## Decisions
- **Prod is the source of truth (ratified).** The Component Unification Map and the plan's phase lists are *candidate* lists, not commitments. A deviation needs one of: owner design intent · prod defect not worth replicating · a locked DS convention. Every deviation documented with counts.
- **"A wrapper that only holds instances is not a component."** The owner challenged `Filter Status Row` (0 props, 0 fills, only 5 Tabs instances). It was deleted and kept as a usage-example frame. Rule now in `Master Plan.md` and applied consistently with the earlier Stat-row call.
- **Modal sizes: md + sm only.** Prod = md 31 · sm 5 · lg 1 · xl 0, plus a `size:'large'` typo bug and 21 `windowClass` bypasses.
- **Data Table scoped to the ngx-datatable cluster** (25 uses, 18 identical configs); the 69 plain `<table>` tags are a separate migration.
- **Calendar panel dropped** — flatpickr renders its own DOM; nothing to spec.
- **Accordion dropped** — 0 real uses (the one `ngbAccordion` file is an orphaned template; `NgbAccordionModule` imported nowhere).
- **Top bar dropped** — 0 selectors, 0 CSS; navigation is sidebar-only.
- **Colors: single light mode** (ratified earlier).

## Audit rules that emerged (all learned the hard way)
1. Parse actual tags across `.html` **and** `.ts`, multi-line safe.
2. Count **rendered shapes**, not option flags (Select has ~40 flags → 20 variants).
3. **Count the mode, not the tag.**
4. **Read the CSS** — don't infer visuals from roadmap prose. (Cost a Tabs + Segmented Control rebuild.)
5. **Check for rival idioms** — Tabs had six competing ones.
6. **A wrapper that only holds instances is not a component.**
7. A per-component audit can miss a pattern living **next door** — Tabs' count badge evidence was in `app-filters` all along.

## Bugs caught by verification
- **All Select fills rendered black** — I'd stripped the `VariableID:` prefix, so every token lookup silently failed.
- **Tooltip arrows invisible** — Figma `rotation` doesn't pivot around visual centre; replaced with explicit `vectorPaths`.
- **Modal `Size=sm` overflowed 47px** — body hugging at 299px inside a 300px panel; fixed with `layoutSizingHorizontal='FILL'`.
- **Tabs had no `Text` property at all** — labels could not be set since the original build.
- Form Field's `Show help` defaulted ON while only ~4 of 406 prod inputs have help text.
- Select + MultiSelect were missing `read-only` despite 44 prod uses (170 `readView` total).

## Files touched
**Vault — new:** `Molecules/` ×14 notes · `Atoms/Tooltip.md` `Atoms/Rating.md` `Atoms/Skeleton.md` · `Molecules Checklist.md` · `Content & Layout Audit.md` · `Organisms Audit.md` · `Organisms/Data Table.md` `Organisms/Modal.md` `Organisms/Filter Bar.md` `Organisms/Search Results Panel.md`
**Vault — edited:** `Master Plan.md` (tier table, phase lists, page structure, the ratified prod-grounding rule) · `Foundations/Color.md` (`surface/field`, `surface/inverse`) · `Components/Tooltip & Popover.md` · `Components/Rating.md` · `Component Inventory.md` · `HaulEx-Web.md`
**Figma `Exr6OibRbgO7X9YeBka2EW`:** Atoms (16 sets, 5 sections) · Molecules (15 sets, 114 variants, 4 sections) · Organisms (5 sets so far, 4 sections)

## D5 + D6 outcomes (later in the session)
- **D5** — `app-files` **rejected** as a container (dropzone + list in a `display:flex` div). Shipped `Dropzone` (3) + `File List` (6). The Organisms Audit had said "the organism is `app-files` (15), not `app-file-list` (1)" — backwards: the `1` was a raw *tag* count and that tag renders 15× inside `app-files`. Counts also killed 3 modes with 1 use each (avatar / inspection / onlyFile), and two states the plan wanted don't exist in prod (`dragover` has no CSS; upload errors are Toasts).
- **D6** — shipped `Nav Rail` (3: collapsed 54 / expanded 212 / mobile full-width) + `Utility Drawer` (2). Owner chose prod over the design-only Sidebar file, which is 5 nav items behind and has no mobile state. Its 3px green active accent, `INSTANCE_SWAP` icon property and 6px radius were raised as candidate improvements, not adopted.
- **Four atom defects found by composition, three fixed:** Tabs `Text` ✅ · Button `Label` (150 variants) ✅ · Badge count clipped at 2 digits (45 variants) ✅ · Menu item API ⬜.
- **Two owner decisions raised:** add `surface/nav` = gray-800 (the DS has no dark-surface family, flagged independently by both the build and the design file's own note); and the nav active state is ≈**1.05:1** against the rail and is the *only* active indicator — a genuine a11y failure faithfully reproduced.

## Follow-ups
- **Next up:** the Text Property Audit pass — 14 sets, ~86 variants (owner-approved for after D6, before Phase 6).
- Then **Phase 4 · Templates**.
- **Screenshots are broken** — `figma_capture_screenshot` times out, `figma_take_screenshot` falls back to REST → 403. `exportAsync` works in-plugin (11,484 bytes), so it's MCP plumbing, likely aggravated by 4 plugin instances (ports 9223–9226). Numeric geometry verification substituted, and it has caught real bugs.
- Pending eye-checks: Data Table header `#cfd8dc` → `surface/sunken`; Modal title 18 SemiBold vs prod 19/400; Search panel's very heavy `rgba(0,0,0,0.67)` shadow.
- Publish atoms + Form Field to the empty Component Library page (`89:136`).
- **13px off-scale type now hits three components** (Segmented Control, Pagination, Search rows) — decide whether to add a token or snap all three to 14.

## Links
- Figma component library: `Exr6OibRbgO7X9YeBka2EW`
- Prod source: `D:\CRM_V2` (Angular 21, Tailwind 3.3 + Flowbite, ngx-datatable, flatpickr, slim-select, ngx-popperjs, NgRx)
- Design-only sidebar file: `ZaNTxYs4fbG9tu5d60pzxG`
