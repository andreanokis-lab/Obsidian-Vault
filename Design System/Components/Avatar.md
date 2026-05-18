# Avatar

Circular profile image with optional colored ring + rank badge. Built for leaderboard / podium contexts (1st, 2nd, 3rd place) but reusable as a generic profile avatar by hiding the badge.

- **Component set node:** `1281:4432`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=1281-4432)
- **Figma section:** `----- Image Content` → "Avatar"
- **Figma documentation:** Section `1728:5720` "Avatar — Documentation" on the same page

---

## Composition

`Rank=First` — image + ring + rank badge stacked vertically.

| Layer | Bindings |
|---|---|
| Image (FRAME, 112×112 for First; 88×88 for Second/Third) | fill `Background/Subtle` · clipped to circle |
| Ring (ELLIPSE stroke, INSIDE) | strokeWeight `Width/M` (3pt, HIG-aligned) · stroke color per Rank |
| Rank Badge (FRAME, overlaps bottom-center) | fill per Rank · radius `Radius/Pill` · padding `Space/S` × `Space/XS` |
| ↳ Badge label (TEXT, "1"/"2"/"3") | font `Meta/Caption/*` (12pt) · fill per Rank |

The Rank Badge is anchored to the bottom-center of the image and visually overhangs the image edge by half its height.

---

## Variants — `Rank`

| Rank | Image size | Ring stroke | Badge fill | Badge text fill |
|---|---|---|---|---|
| `First` | 112×112 | `Border/Yellow` | `Background/Primary Yellow` | `Text/Primary Inverse Static 2` (dark on yellow) |
| `Second` | 88×88 | `Border/Primary` | `Background/Subtle` | `Text/Primary` |
| `Third` | 88×88 | `Border/Primary` | `Background/Subtle` | `Text/Primary` |

The size hierarchy reinforces rank — First is largest, Second and Third are smaller. Ring color singles out First (yellow medal) while Second/Third share a neutral ring.

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Rank` | VARIANT | `First` | Pick the podium position (First / Second / Third) |

The nested Image and Rank Badge are instances themselves — swap the photo or override `Count` on the badge via the instance properties of those nested components.

---

## Do

- ✅ Use `Rank=First` for the leader / 1st place — yellow ring + yellow badge cue the win.
- ✅ Use `Rank=Second` / `Rank=Third` for podium positions 2 and 3.
- ✅ Swap the nested Image instance to set the actual photo. Default placeholder shows a person icon.
- ✅ Use Avatar inside list rows, leaderboards, and profile contexts where rank matters.

## Don't

- ❌ Don't use Avatar for profile photos that don't represent ranked positions — use the [[Image]] atom with `Format=Circle` for plain avatars.
- ❌ Don't increase the ring weight manually — `Width/M` (3pt) is the HIG-aligned standard.
- ❌ Don't swap the yellow ring colour for First — it's a fixed convention across leaderboard contexts.
- ❌ Don't stack a `Rank Badge` from [[Badge]] manually on top of an Avatar — the rank badge slot is already built in.

---

Back to [[Design System]] · [[Component Status]].
