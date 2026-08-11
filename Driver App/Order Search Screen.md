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

## Open findings — 2026-08-11

| # | Finding | Fix | Strength |
|---|---|---|---|
| 1 | `All` is the **last** segment in both controls | Move to **first**. Widest scope leads, it is the default state, and [[Orders List]] already uses `All / Active / Completed` — the two screens currently disagree. | Convention + internal consistency (not a HIG bullet) |
| 2 | `Reset` uses a red / destructive treatment | Use `Text/Link` (`#3395FF` dark). Per [[Colors - Semantic]], `Text/Negative` is for validation errors and destructive labels only — resetting a search form destroys nothing. | Vault rule |
| 3 | Both Segment Controls are **unlabelled** while every Input above has a label | Add field labels (`Order type`, `Status`) in the field-label style, `Space/S` gap. [[Form Pattern]]: *always show the Label on every field*. | Vault rule |
| 4 | `Reset` is enabled in the pristine state (`All`/`All`, all fields empty) | Disable or hide until ≥1 criterion is set. | Usability |
| 5 | 4 segments across 361pt ≈ 85pt each; ~80pt at 375pt ([[Rules]] L3) | "Completed" is already tight and breaks at larger Dynamic Type. Use `Scrollable=Yes` (exists only at `Segments=4`) or shorten to "Done". | Check |
| 6 | Back chevron + bottom `Apply` — unapplied-filter behaviour undefined | Annotate: does back discard? If presented modally, iOS convention is `Cancel` leading, not a chevron. | Flow question |

## DS gap filed

**[[Navigation Bar]] has no text trailing action.** All six `Type` variants specify the trailing slot as an 88pt container holding a 44pt circular *icon* button. A text `Reset` / `Clear` / `Done` is therefore an off-system override ([[Rules]] C2). Needs a new variant or a text-trailing property — logged in [[Component Status]].

Back to [[Driver App]] · [[Design System]] · [[Filter Search Results Pattern]].
