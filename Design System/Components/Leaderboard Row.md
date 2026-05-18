# Leaderboard Row

Driver-leaderboard row showing rank, avatar/initials, name, and stats (vehicles, trips). Used in the leaderboard list — typically composed below the podium ([[Avatar]] First/Second/Third) showing positions 4+.

- **Component node:** `1297:250`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1297-250)
- **Figma section:** `----- Content Row` → "Leaderboard Row"

---

## Composition

Horizontal row: rank number + avatar circle + name + stats.

| Layer | Bindings |
|---|---|
| Row Content (FRAME) | padding `Space/XL` × `Space/L` · gap `Space/L` |
| Rank (FRAME) | padding `Space/S` × `Space/M` |
| ↳ Rank number (TEXT) | `Text/Primary` |
| Avatar (FRAME) | fill `Background/Subtle` · circular |
| ↳ Initials (TEXT) | `Text/Primary` |
| Info (FRAME, name + stats) | gap `Space/XS` |
| ↳ Name (TEXT) | `Text/Primary` |
| ↳ Stats (FRAME) | gap `Space/XL` |
| ↳↳ Vehicles / Trips (FRAME each) | gap `Space/XS` |
| Divider | `Border/Primary` (toggleable) |

---

## Variants

None — single component.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Rank` | TEXT | "4" | Position number (4+ for non-podium) |
| `Name` | TEXT | "Seoul Steelton" | Driver name string |
| `Initials` | TEXT | "SS" | Avatar initials fallback (used when no photo) |
| `Vehicles` | TEXT | "24" | Vehicles stat value |
| `Trips` | TEXT | "4" | Trips stat value |
| `Show divider` | BOOLEAN | true | Toggle the bottom divider |

---

## Do

- ✅ Use Leaderboard Row for ranks 4 and below — positions 1–3 use the [[Avatar]] First/Second/Third podium.
- ✅ Show initials when no photo is available — driver leaderboards default to initials.
- ✅ Keep the stats short (1–3 digits). The layout assumes compact numerics.
- ✅ Hide `Show divider` on the last row before a section break.

## Don't

- ❌ Don't use Leaderboard Row for the top 3 — they get the bigger [[Avatar]] podium treatment.
- ❌ Don't put a third stat — the row layout is sized for Vehicles + Trips only.
- ❌ Don't use Leaderboard Row outside of leaderboard contexts. For generic driver list rows, use [[List]] or [[Content Row]].

---

Back to [[Design System]] · [[Component Status]].
