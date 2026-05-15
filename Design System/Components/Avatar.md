# Avatar

Reusable circular avatar with optional colored ring + rank badge. Built for leaderboard / podium contexts but works as a generic profile avatar via `Rank=None`.

- **Component set node:** `1281:4432` (page `----- Image Content` → section `Avatar`)
- **Source reference:** [Leaderboard avatar section](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1280-552) (`1280:552`)

## Composition

| Layer | Component / Token |
|---|---|
| Image | `Image` set (`449:2627`) — `Format=Circle`, `Size=L` (112) for Rank 1 / None, `Size=M` (88) for Rank 2 / 3 |
| Ring | Ellipse stroke, `strokeAlign=INSIDE`, `strokeWeight` → `Border / Width / M` (3 px — HIG aligned) |
| Ring color | `yellow/500` for Rank 1; `neutral/500` for Rank 2 / 3 / None |
| Rank Badge | `Badge` set (`283:90`) — `Role=Count Badge`, `Type=Yellow` for Rank 1, `Type=Default` for Rank 2 / 3, hidden for Rank=None. `Count` text = rank number. |

Badge is positioned bottom-center, vertically translated by half its height so it overhangs the image edge.

## Variants

| Rank | Image size | Ring color | Badge |
|---|---|---|---|
| `1` | L (112) | `yellow/500` | Yellow Count Badge "1" |
| `2` | M (88) | `neutral/500` | Default Count Badge "2" |
| `3` | M (88) | `neutral/500` | Default Count Badge "3" |
| `None` | L (112) | `neutral/500` | hidden |

## Known gaps vs reference design

- Reference uses 3 px ring on Rank 1 and 2 px on Rank 2 / 3. Tokens offer XS=1, **M=3** (HIG aligned), L=4, XL=8. Component now uses **M = 3 everywhere** — matches the Rank 1 reference; Rank 2/3 are 1px thicker than reference but the rank hierarchy is carried by image size, not stroke. Width/S (1.5) was deleted as non-standard.
- Reference badge for Rank 2 / 3 uses raw `#717171` with white text — there is no Badge variant matching this. Component uses the system's `Default Count Badge` (light gray fill, dark text). To replicate the reference exactly, add a `Type=Neutral Strong` (or similar) badge variant with `neutral/500` fill + inverse text.
- Reference badge sizes are 29 / 32 px; system Count Badge is 24 px. Component uses the system size.

## Properties exposed on instances

- `Rank` = `1 | 2 | 3 | None` (variant)
- Nested `Image` instance — swap photo or change `Size`/`Format` per usage
- Nested `Rank Badge` instance — override `Count` text, `Type` accent color

## Follow-ups

- Compose `LeaderboardCard` molecule on top of this: Avatar + name (`Semantic/IOS/List/Title`) + stats row (`Vehicles`, `Trips`).
- Consider adding `Size` as an independent property if non-podium uses need M-size avatars without rank.
- ~~File a token request for a true 3 px width token~~ — resolved 2026-05-14, `Width/M` corrected from 2pt to 3pt. Still need a `neutral` Badge variant to close the remaining design parity gap.

Back to [[Design System]] · [[Components - In Progress]].
