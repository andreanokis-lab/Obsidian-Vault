# Titles

Leaderboard / podium name block — driver name + stats (Vehicles, Trips). Three variants for first place, 2nd–3rd places, and a loading skeleton.

Used inside [[Places Segments]] and the leaderboard podium composition.

- **Component set node:** `1282:4616`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1282-4616)
- **Figma section:** `----- Image Content` → "Titles"
- **Figma documentation:** Section `1751:8341` "Titles — Documentation" on the same page

---

## Composition

`Place=1st Place` — vertical stack: full name + stats row.

| Layer | Bindings |
|---|---|
| Container (FRAME) | gap `Space/XS` |
| Full Name (TEXT) | `Section/Title/*` (20pt, SF Pro Display) · `Text/Primary` |
| Underline (FRAME) | gap `Space/XS` |
| Vehicles (TEXT) | `Text/Tertiary` |
| Trips (TEXT) | `Text/Tertiary` |

The Skeleton variant replaces the text rows with placeholder shapes for loading states.

---

## Variants — `Place`

| Place | Use for |
|---|---|
| `1st Place` | Top podium spot — largest treatment |
| `2nd - 3nd Places` | Second / third podium spots |
| `Skeleton` | Loading state — placeholder shapes before data loads |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Full Name` | TEXT | "John K." | Driver display name |
| `Vehicles` | TEXT | "Vehicles: 12" | Vehicles stat |
| `Trips` | TEXT | "Trips: 4" | Trips stat |

---

## Do

- ✅ Use `1st Place` for the leaderboard winner — pair with the largest [[Avatar]] (Rank=First).
- ✅ Use `2nd - 3nd Places` for podium positions 2 and 3.
- ✅ Use `Skeleton` while leaderboard data is loading — restore content once available.
- ✅ Keep names abbreviated when long (use initials or "John K." style) so they fit the title slot.

## Don't

- ❌ Don't use Titles for ranks 4 and below — use [[Leaderboard Row]] for compact list rows.
- ❌ Don't use Titles outside the leaderboard context — the typography is sized for podium display.
- ❌ Don't leave Vehicles / Trips empty in non-Skeleton variants — they're the stat the row exists to show.

---

Back to [[Design System]] · [[Component Status]].
