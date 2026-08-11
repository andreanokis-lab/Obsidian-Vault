---
status: in-review
type: screen-spec
figma_node: TBD
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Order Search Screen

Filter/search form for the Orders list. Pushed iOS screen — nav bar with back + `Reset`, six criteria fields, two single-select [[Segment Control]] filters, bottom-anchored `Apply`.

First reviewed 2026-08-11 from a screenshot; **Figma node not yet recorded** — link it on the next pass.

## Structure

| Region | Component | Notes |
|---|---|---|
| Nav bar | [[Navigation Bar]] `Type=Default` | Back chevron leading · title "Order Search" · **text `Reset`** trailing — see gap below |
| Order | [[Input]] | placeholder `e.g. 53232.1` |
| Vehicle | [[Input]] | placeholder `e.g. 2019 Honda Civic` |
| Ref# | [[Input]] | placeholder `e.g. 8975632` |
| VIN | [[Input]] | placeholder `Full or last 6 digits` |
| Order hierarchy | [[Segment Control]] `Segments=4` | `Parent / Sub. 1 / Sub. 2 / All` — **unlabelled** |
| Status | [[Segment Control]] `Segments=4` | `Pickup / Delivery / Completed / All` — **unlabelled** |
| Pickup Address | [[Input]] | placeholder `City, State or ZIP` |
| Delivery Address | [[Input]] | placeholder `City, State or ZIP` |
| Apply | [[Button]] `Size=L, Type=Primary, Role=Inverse` | Full-width, bottom-anchored — correct per [[Form Pattern]] |

## What this screen got right

- The trailing `✕` inside the Segment Control is **gone** — `All` is a real segment ([[Rules#C5]]).
- One segment is always selected; the control always shows current state.
- The reset action is a **word in the nav bar**, not a glyph in the track — placement #3 of the ranked table in [[Filter Search Results Pattern]].
- `Reset` is spatially separated from `Apply`, satisfying the [[Form Pattern]] don't-put-Clear-near-Submit rule.
- `Apply` is full-width and bottom-anchored per [[Form Pattern]].

## States

Two designed: **Order Search Filled** and **Order Search empty**. Both reviewed 2026-08-11 (rev 2).

| State | Fields | Segments | `Reset` |
|---|---|---|---|
| Filled | 6 populated (`53232.1`, `2019 Honda Civic`, `8975632`, `3456H3`, `Massachusetts`, `Seattle`) | `Parent` · `Delivery` | Enabled |
| Empty (pristine) | all placeholders | `All` · `All` | **Disabled / dimmed** ✅ |

## HIG verdict — Segment Controls pass (rev 2)

No actions inside the control · closely related choices affecting a view state · consistent segment size · all-text content · 4 segments (≤5 on iPhone) · a segment is always selected. Compliant with HIG § Segmented controls and with [[Rules#C5]].

## Findings

| # | Finding | Status (rev 2) | Strength |
|---|---|---|---|
| 1 | `All` was the **last** segment in both controls | ✅ **Fixed** — now leading in both, consistent with [[Orders List]] | Convention + internal consistency |
| 2 | `Reset` used a red / destructive treatment | ⚠️ **Partial** — red removed, but it now matches the title's white and reads as a label, not a button. Apply `Text/Link` (`#3395FF`); keep the dimmed treatment for disabled. | Vault rule ([[Colors - Semantic]]: `Text/Link` = tappable text actions) |
| 3 | Both Segment Controls are **unlabelled** while all 6 Inputs have labels | ❌ **Open** — add `Order type` and `Status` in the field-label style, `Space/S` gap. [[Form Pattern]]: *always show the Label on every field*. Also leaves VoiceOver with no context for the group. | Vault rule + a11y |
| 4 | `Reset` enabled in the pristine state | ✅ **Fixed** — dimmed in the empty state | Usability |
| 5 | 4 segments across 361pt ≈ 76pt each after padding | ⚠️ **Verify** — in the filled state "Completed" nearly touches the container edge. Check at 375pt ([[Rules]] L3) and Dynamic Type XXL. If it truncates: `Scrollable=Yes` (exists only at `Segments=4`) or shorten to "Done". | Check |
| 6 | Back chevron + bottom `Apply` — unapplied-filter behaviour undefined | ❌ **Open** — annotate: does back discard? If presented modally, iOS convention is `Cancel` leading, not a chevron. | Flow question |

## Intentional deviations

- **`Apply` stays enabled in the pristine state** while `Reset` is disabled. [[Form Pattern]] says to disable submit until minimum required fields are filled, but an empty search legitimately means "show everything". Recorded so the next reviewer doesn't re-flag it.

## DS gap filed

**[[Navigation Bar]] has no text trailing action.** All six `Type` variants specify the trailing slot as an 88pt container holding a 44pt circular *icon* button. A text `Reset` / `Clear` / `Done` is therefore an off-system override ([[Rules]] C2). Needs a new variant or a text-trailing property — logged in [[Component Status]].

Back to [[Driver App]] · [[Design System]] · [[Filter Search Results Pattern]].
