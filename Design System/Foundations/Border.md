# Border & Radius

10 FLOAT tokens, single mode, in the `Border` collection. **Never type radius or stroke values manually — always bind to a `Radius/*` or `Width/*` variable.**

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Collection:** `Border`
- **Mode:** single
- **Total tokens:** 10 (6 Radius + 4 Width)
- **Visualization:** Section `1706:6519` "Border & Radius — Visualization" on the new `----- Border & Radius` page (`1706:6518`).
- **Usage evidence:** Driver App DS page binding scan — ~22,675 spacing/radius bindings (Radius/* portion ~7,400) + ~2,870 stroke-weight bindings.

Border *color* tokens (`Border/Subtle`, `Border/Strong`, etc.) live in the [[Colors - Semantic|Colors: Semantic]] collection — separate from this collection.

---

## Radius spec

| Token | Value | DS bindings | Real usage | Verdict |
|---|---|---|---|---|
| `Radius/XS` | 4pt | 4 | Almost nothing | ❌ Reserved |
| `Radius/S` | 8pt | 744 | Small badges, chips, compact buttons | ✅ Heavy use |
| `Radius/M` | 12pt | 137 | Inputs, text areas, modals | ✅ Modest |
| `Radius/L` | 16pt | 734 | Cards, sheets, bottom bars | ✅ Heavy use |
| `Radius/Pill` | 999pt | ~5,632 | Buttons, chips, tabs — **dominant radius token** | ✅ Core |
| `Radius/Circle` | 999pt | 4 | Avatars, circular icon containers | ❌ Reserved |

**Fix applied this audit:** `Radius/Circle` was `50` — that value does not produce a circle on any real element. Corrected to `999`, matching `Radius/Pill`'s "max radius" behavior. The two tokens are now functionally identical but kept separate for semantic clarity (Pill = capsule-shape on a non-square element; Circle = round-shape on a square element).

**Legacy token retired:** A non-collection variable `rounded-full` (9999) was found bound to 12 corner bindings across 3 "Icon Shapes" frames in the Driver App. All 12 bindings rebound to `Radius/Pill`. The source variable still exists outside the Border collection but has no consumers.

---

## Width spec

| Token | Value | DS bindings | Real usage | Verdict |
|---|---|---|---|---|
| `Width/XS` | 1pt | ~1,860 | Dividers, default borders, all FRAME/INSTANCE/LINE strokes — **dominant stroke token** | ✅ Core |
| `Width/M` | 3pt | 6 | Avatar rings (ELLIPSE strokes) — corrected from 2pt to match HIG | ✅ Used (HIG) |
| `Width/L` | 4pt | 0 | — | ❌ Reserved |
| `Width/XL` | 8pt | 0 | — | ❌ Reserved |

Width/XS is so dominant (~1,860 bindings vs 6 for the next-most-used) that the system effectively has **two** stroke widths in production: 1pt for everything, 3pt for avatar rings. The 4pt / 8pt tokens have never been used in the DS-page consumer.

---

## Do — evidence-based

- ✅ `Radius/Pill` (999) is the standard for **buttons, chips, tabs** — confirmed by ~5,632 bindings, the dominant radius token.
- ✅ `Radius/L` (16) is the standard for **cards, sheets, bottom bars** — confirmed by 734 bindings.
- ✅ `Radius/S` (8) is the standard for **small badges and compact buttons** — confirmed by 744 bindings.
- ✅ `Radius/M` (12) is reserved for **inputs, text areas, modals** — 137 bindings confirm the role.
- ✅ `Width/XS` (1) is the **universal divider and default border** — confirmed by ~1,860 bindings.
- ✅ `Width/M` (3) is for **avatar rings (ELLIPSE strokes)** — confirmed by 6 bindings, exclusively on circular elements. Value corrected from 2pt to 3pt to match Apple HIG.

## Don't — evidence-based

- ❌ Don't type radius or stroke values manually. Bind to `Radius/*` or `Width/*` variables only.
- ❌ Don't use `Radius/Pill` and `Radius/Circle` interchangeably. `Pill` is for capsule-shape on non-square elements (buttons, chips); `Circle` is for round shape on square elements (avatars, icon containers).
- ❌ Don't reach for `Radius/XS` (4) — only 4 production bindings exist. Use `Radius/S` (8) for small containers.
- ❌ Don't use `Width/L` (4) or `Width/XL` (8) — both reserved, zero production bindings. Justify before binding.
- ❌ Don't use the legacy `rounded-full` (9999) variable — retired. The 3 Driver App nodes that referenced it were rebound to `Radius/Pill`.

---

## Fixes applied this audit

| Issue | Fix |
|---|---|
| `Radius/Circle` value was `50` — never produced a circle | Set to `999` (matches `Radius/Pill` behaviour) |
| Legacy `rounded-full` variable (9999) bound on 3 Empty-State "Icon Shapes" frames | All 12 corner bindings rebound to `Radius/Pill` in Driver App |
| `Width/S` (1.5pt) — non-standard iOS value, 0 production bindings | Deleted from collection |
| `Width/M` was 2pt — Apple HIG avatar ring is 3pt | Value corrected: 2 → 3. 6 existing avatar ring bindings auto-update to 3pt |

Back to [[Design System]] · [[Rules]].
