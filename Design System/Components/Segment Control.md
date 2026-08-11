# Segment Control

iOS-style segmented control — a row of 2–4 [[Tab Item]] pills inside a `Background/Subtle` container, with one item selected at a time. Scrollable variant available when segments overflow the screen width.

For a single pill (not part of a segment group) use [[Tab Item]] alone.
For drop-down value picking use [[Select]] + [[Menu]].

- **Component set node:** `321:1008`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=321-1008)
- **Figma section:** `----- Segment Control` → "Segment Control"
- **Figma documentation:** Section `1748:7889` "Segment Control — Documentation" on the same page

---

## Composition

`Selected=1, Segments=3, Scrollable=No` — horizontal pill containing 3 Tab Items.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` · radius `Radius/Pill` · padding `Space/XS` all sides · gap `Space/XS` |
| Selected Tab Item | fill `Background/Inverse` · `Radius/Pill` · padding `Space/Zero` × `Space/S` |
| ↳ Label | `Text/Secondary/*` (15pt, SF Pro Text) · `Text/Primary Inverse` |
| Unselected Tab Items | no fill (transparent) · same padding |
| ↳ Label | `Text/Secondary/*` · `Text/Primary` |
| Trailing `Controls` slot | [[Controls]] `xMark` · 44×44 · `Icon/Primary` · **hidden by default in every variant** |

Every variant carries a hidden trailing [[Controls]] `xMark` layer at x=313 inside the container. Auto-layout redistributes the Tab Items when it is switched on (2 segments: 174.5 → 150.5pt each; 3 segments: 99pt each). It is toggled by **raw layer visibility**, not a boolean component property — see the ⚠️ below.

---

## Variants

13 combinations across 3 axes.

| Axis | Values | Notes |
|---|---|---|
| `Segments` | `2` · `3` · `4` | How many segments are shown |
| `Selected` | `1` · `2` · `3` · `4` | Which segment is currently active |
| `Scrollable` | `No` · `Yes` | Yes when segments overflow horizontally — only at `Segments=4` |

Not every combination exists — `Scrollable=Yes` only appears with `Segments=4`.

---

## Instance properties

None at the top level — the Tab Item labels inside each segment are overridden via the inner instance. The trailing `xMark` has no boolean property either; it is switched on by unhiding the layer.

---

## ⚠️ The trailing `xMark` — reviewed 2026-08-11, verdict: don't ship it

Two Driver App instances (`930:30872` 2-segment "Sub. 1 / Sub. 2", `930:30878` 3-segment "Order / Picked Up / Delivered", both inside frame `1925:26706`) have the trailing `xMark` unhidden to act as a "clear the selection" affordance. This is wrong for four reasons:

| # | Problem |
|---|---|
| 1 | **Mixes an action into a selection group.** HIG treats a segmented control as a set of mutually exclusive options that express the *current state of the view*. Segments select; they don't act. An action glyph sharing the container reads as a fifth segment. |
| 2 | **"Nothing selected" isn't a state the control can express.** With the selection cleared, the control shows no state at all and the user can't tell what the list below is filtered to. `UISegmentedControl` technically allows `noSegment`, but no first-party iOS UI ships it and HIG gives no deselect affordance. |
| 3 | **`✕` already means something else on iOS.** Close / dismiss / clear-text-field. Users will read it as "close this screen", not "reset this filter" — an icon-only control with no label and a mismatched convention. |
| 4 | **VoiceOver can't distinguish it.** It sits inside the group with the segments and no accessibility label of its own, so the destructive control is announced like any other option. |

### What to do instead

| Situation | Fix |
|---|---|
| The "no filter" case is real (most common) | Add an explicit **`All`** segment. This is already the convention on [[Orders List]] (`All / Active / Completed`) — keeps mutual exclusivity, always shows current state, zero new affordances. |
| The whole filter row is dismissible | Put a text **Clear** / **Reset** [[Button]] (`Type=Ghost`) **outside** the container, or in the [[Navigation Bar]] trailing slot. Never inside the track. |
| Filters are multi-select or individually removable | Use [[Chip]] rows, not a Segment Control. A removable `✕` is legitimate on a chip. |
| 5+ options | [[Select]] + [[Menu]]. |

Until this is resolved: **leave the `Controls` layer hidden** and don't add a boolean prop for it (adding the prop legitimises the pattern). If it survives PM review, it must at minimum move outside the container, gain a text label, and get its own accessibility label.

Space cost is also real: at `Segments=4` + `xMark`, segments fall to ~73pt and long labels truncate.

---

## Do

- ✅ Use Segment Control to pick between 2–4 mutually exclusive views or filters.
- ✅ Match `Selected` to the currently active segment in your design.
- ✅ Use `Scrollable=Yes` for 4-segment groups where labels are long and would overflow the row.
- ✅ Keep segment labels short (1–2 words) — Apple HIG: segments are scannable at a glance.

## Don't

- ❌ Don't use Segment Control for more than 4 segments — readability collapses. Use [[Select]] + [[Menu]] for 5+ options.
- ❌ Don't use Segment Control for binary on/off — use [[Toggle]].
- ❌ Don't mix Tab Item Role colors (Pickup, Deliver, Complete) with generic segments — pick one taxonomy.
- ❌ Don't unhide the trailing [[Controls]] `xMark` to mean "clear selection" — use an `All` segment or an external `Clear` button (see the ⚠️ section above).
- ❌ Don't leave the control with no segment selected — it always shows the current state of the view below.

---

Back to [[Design System]] · [[Component Status]].
