# Places Segments

Leaderboard podium block — [[Avatar]] image + rank badge + [[Titles]] (name + stats). Two variants for first place vs 2nd / 3rd places. Composes into the leaderboard podium.

- **Component set node:** `1282:4757`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1282-4757)
- **Figma section:** `----- Image Content` → "Places Segments"
- **Figma documentation:** Section `1751:8407` "Places Segments — Documentation" on the same page

---

## Composition

`Place=First place` — vertical stack: avatar with ring + rank badge + titles block.

| Layer | Bindings |
|---|---|
| Container (FRAME) | gap `Space/S` |
| Image (FRAME) | fill `Background/Subtle` · `Radius/Pill` (circular) |
| Ring (ELLIPSE) | stroke `Width/M` (3pt, HIG aligned) · stroke color `Border/Yellow` |
| Rank Badge (FRAME) | fill `Background/Primary Yellow` · `Radius/Pill` · padding `Space/S` × `Space/XS` |
| Rank number (TEXT, "0") | `Meta/Caption/*` (12pt) · `Text/Primary Inverse Static 2` (dark on yellow) |
| Titles (instance) | nested [[Titles]] block — name + stats |

The `2-3 Places` variant uses a different ring colour and the smaller avatar size for 2nd/3rd podium spots.

---

## Variants — `Place`

| Place | Use for |
|---|---|
| `First place` | Top podium spot — yellow ring + larger avatar |
| `2-3 Places` | Podium 2nd and 3rd spots |

---

## Instance properties

None at the top level — the inner [[Titles]] instance exposes name and stats overrides.

---

## Do

- ✅ Use `First place` for the rank-1 podium spot — the larger size and yellow ring are the rank signal.
- ✅ Use `2-3 Places` for podium positions 2 and 3.
- ✅ Override the nested [[Titles]] instance to set the driver name and stats per spot.
- ✅ Compose three Places Segments side-by-side for the full podium layout.

## Don't

- ❌ Don't use Places Segments for ranks 4+ — those use [[Leaderboard Row]] (compact list row format).
- ❌ Don't override the ring colour manually — `Border/Yellow` for 1st is part of the design language.
- ❌ Don't swap the Avatar Image size — variant size is determined by `Place`.

---

Back to [[Design System]] · [[Component Status]].
