---
type: session
date: 2026-08-11
project: HaulEx Driver App
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Session — Segment Control trailing `✕` review

Owner asked whether the `✕` inside two segmented controls (meant as "unselect the choice") is correct, and what HIG says.

## What was reviewed

Frame `1925:26706` in the Driver App file — two [[Segment Control]] instances with the trailing `xMark` unhidden:

| Node | Segments | Widths |
|---|---|---|
| `930:30872` | `Sub. 1` (selected) / `Sub. 2` | 150.5pt each + 44pt `✕` |
| `930:30878` | `Order` (selected) / `Picked Up` / `Delivered` | 99pt each + 44pt `✕` |

## Findings

1. **The `xMark` is part of the master component**, not a local addition. Every variant of `321:1008` in the UIKit contains a trailing [[Controls]] layer (e.g. `2149:4528` in `324:339`) that is **hidden by default**. The Driver App instances just unhide it.
2. **[[Controls]] gained a third variant** — `+ / - / x = xMark`, node `2149:4518` — after the vault note was written. The note said Plus/Minus only. Now corrected.
3. **No boolean property** governs the slot; it is toggled by raw layer visibility, so the pattern is undiscoverable and untrackable in handoff.

## Decisions ratified by the owner

| Decision | Outcome |
|---|---|
| **How "no filter" is expressed** | Explicit **`All`** segment. Matches the [[Orders List]] precedent. `Order / Picked Up / Delivered` needs no clear affordance — `Order` is already the default. |
| **Hidden `xMark` slot in the master** | **Delete from all 13 variants** of `321:1008` + republish. Explicitly *not* promoted to a boolean property — that would legitimise the pattern. |
| **Generalised as a rule** | New [[Rules#C5]]: a mutually exclusive selection control never carries an action. Covers [[Segment Control]], [[Tab Bar]], [[Page Control]]. |

**Execution pending** — no Figma edits applied yet. Two workstreams: (a) UIKit master cleanup + library republish + updates-accepted in the Driver App, (b) the two Driver App instances `930:30872` / `930:30878` switched to `Segments=3` with an `All` label (or the `✕` simply removed).

The HIG citation that decided it: § Segmented controls, Best practices — the bullet forbidding segmented controls from offering actions, whose examples include *removing* content. Recorded verbatim in [[Rules#C5]].

## Verdict — don't ship it

Reasoning recorded in full in [[Segment Control]]. Summary: it mixes an action into a mutually exclusive selection group; "nothing selected" is not a state a segmented control can express (HIG has no deselect affordance, and no first-party iOS UI ships `noSegment`); `✕` already means close/dismiss on iOS; and VoiceOver can't distinguish it from a segment.

Recommended fixes, in order of preference: explicit **`All`** segment (already the convention on [[Orders List]] — `All / Active / Completed`) → external ghost **Clear** button or [[Navigation Bar]] trailing action → [[Chip]] row if filters are really multi-select/removable → [[Select]] + [[Menu]] at 5+ options.

Also flagged: at `Segments=4` + `xMark`, segments drop to ~73pt and long labels truncate.

## Files written

- [[Segment Control]] — trailing slot documented + ⚠️ review verdict section + 2 new Don'ts
- [[Controls]] — `xMark` variant added, scope limited to dismiss/close
- [[Component Status]] — both rows updated

## Open

- PM decision on the canonical filter set for the `Order / Picked Up / Delivered` control (same open question as [[Orders List]] § Follow-ups).
- If PM insists on a clear affordance, it must move outside the container, gain a text label, and get its own accessibility label.

Back to [[Design System]] · [[Driver App]].
