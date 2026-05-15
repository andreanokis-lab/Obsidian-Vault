# Badge

Compact pill or pip used to label status, count, or category. Appears inline next to content (status badge), atop another component (count badge on avatars/icons), or standalone (damages indicator on vehicle outlines).

- **Component set node:** `283:90`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=283-90)
- **Figma section:** `----- Badges` → "Badge"
- **Figma documentation:** Section `1718:4768` "Badge — Documentation" on the same page

---

## Composition

`Type=Default, Role=Status, Accent=Primary` (`283:61`) — horizontal stack of label + optional icons.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Subtle` (per Type) · radius `Radius/Pill` (999) · padding `Space/S` all sides · gap `Space/XS` |
| Leading icon (16×16, optional) | `Icon/Primary` (per Type) |
| Label (TEXT) | `Text/Secondary/*` (Subheadline 15pt, SF Pro Text) · fill `Text/Primary` (per Type) |
| Trailing icon (16×16, optional) | `Icon/Primary` (per Type) |

Other Type and Accent combinations swap the container fill, label color, and icon color. Roles control which content slots are visible — Count shows a number, Icon shows just an icon, Label shows text, Status shows text + optional dot, Damages is a special vehicle-outline indicator.

---

## Variant axes

3 axes — combine to pick the right badge.

| Axis | Values | Notes |
|---|---|---|
| `Type` | `Default` · `Yellow` · `Green` · `Blue` · `Red` · `Disabled` · `Black` | Drives color treatment (fill, text, icon) |
| `Role` | `Status` · `Label` · `Count Badge` · `Icon Badge` · `Damages` | Determines content slots and shape |
| `Accent` | `Primary` · `Secondary` | `Primary` = solid filled; `Secondary` = subtle tinted background |

Total combinations: 7 × 5 × 2 = 70. Built: 47 (not every Type+Role+Accent makes sense — e.g., `Disabled` only ships as Primary).

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Badge` | TEXT | "Badge" | Label string (Status / Label roles) |
| `Count` | TEXT | "0" | Count number (Count Badge role) |
| `Letter` | TEXT | "S" | Single-letter glyph (compact badges) |
| `Text` | TEXT | "ABBR" | Short abbreviation text |
| `Icon` | INSTANCE_SWAP | default circle | Icon (Icon Badge role) |
| `Leading Icon` | INSTANCE_SWAP | default circle | Leading icon for status badges |
| `Trailing Icon` | INSTANCE_SWAP | default circle | Trailing icon for status badges |
| `Show Leading Icon` | BOOLEAN | true | Toggles the leading icon |
| `Show Trailing Icon` | BOOLEAN | true | Toggles the trailing icon |

---

## When to use

| Use case | Pick |
|---|---|
| Inline status next to a label ("Active", "Pending") | `Role=Status, Type=Default/Yellow/Green/Red, Accent=Primary` |
| Category label on a card or row | `Role=Label, Type=Default, Accent=Primary` |
| Count pip on icons / avatars (e.g., "3 unread") | `Role=Count Badge, Type=Red, Accent=Primary` |
| Standalone icon indicator | `Role=Icon Badge, Type=Red/Green, Accent=Primary` |
| Damage marker on vehicle outline | `Role=Damages, Type=Yellow/Blue/Red, Accent=Primary` |
| Muted tinted background for low-emphasis status | Same Role + `Accent=Secondary` (tinted, not solid) |

---

## Do

- ✅ Use `Type=Red` only for negative / urgent status (errors, overdue, missing).
- ✅ Use `Type=Yellow` for caution / in-progress / partial status.
- ✅ Use `Type=Green` for positive / completed / approved status.
- ✅ Use `Type=Blue` for informational / neutral status (not destructive, not success).
- ✅ Use `Accent=Secondary` (tinted background) when multiple badges sit in the same row and you want them visually quieter.
- ✅ Use `Role=Count Badge` for numeric overlays — pairs with [[Avatar]] rank badge slot and notification dots on toolbar icons.

## Don't

- ✅ Don't use `Type=Red` for non-urgent items just because red is eye-catching — users pattern-match red to errors.
- ❌ Don't pile up multiple `Accent=Primary` badges in one row — they all compete for attention. Promote one to Primary, demote the rest to Secondary.
- ❌ Don't use `Role=Damages` outside vehicle-outline contexts — it carries domain-specific semantics.
- ❌ Don't override the label text with a paragraph — badges are 1–2 word affordances. Use a Card or Toast for longer copy.
- ❌ Don't use `Type=Disabled` for "inactive but tappable" controls — it implies non-interactive. For "not selected" use `Accent=Secondary` instead.

---

Back to [[Design System]] · [[Component Status]].
