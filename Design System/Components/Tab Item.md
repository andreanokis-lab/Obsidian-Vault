# Tab Item

Individual pill-shaped tab inside a tab strip or Segment Control. Six Role variants color-encode trip-stop status (Pickup, Deliver, Complete) and segment state (Normal, Idle, Disabled).

Used inside a higher-level Segment Control molecule — rarely placed alone.

- **Component set node:** `320:3407`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=320-3407)
- **Figma section:** `----- Segment Control`
- **Figma documentation:** Section `1724:5387` "Tab Item — Documentation" on the same page

---

## Composition

`Role=Pickup` — capsule pill with a centered label.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Primary Yellow` (per Role) · radius `Radius/Pill` · padding `Space/S` × `Space/Zero` |
| Label (TEXT) | font `Text/Secondary/*` (Subheadline 15pt, SF Pro Text) · fill `Text/Primary Inverse Static` |

Other Role values swap container fill and label color.

---

## Variants — `Role`

| Role | Container fill | Use for |
|---|---|---|
| `Pickup` | `Background/Primary Yellow` | Pickup stop indicator |
| `Deliver` | `Background/Primary Red` | Delivery stop indicator |
| `Complete` | `Background/Primary Green` | Completed stop |
| `Normal` | Default neutral fill | Active / current tab in a generic Segment Control |
| `Idle` | Subtle / neutral fill | Inactive tab |
| `Disabled` | `Background/Disabled` | Tab not selectable in current context |

---

## Instance properties

| Property | Type | Default | Purpose |
|---|---|---|---|
| `Label` | TEXT | "Label" | Visible tab label string |

---

## Do

- ✅ Use Role to color-encode meaning: Yellow = pickup, Red = deliver, Green = complete.
- ✅ Use `Normal` / `Idle` for plain segment-control tabs that aren't trip-stop coded.
- ✅ Use `Disabled` when the tab represents an action / step that's not yet available.
- ✅ Always set the `Label` — bare tabs have no meaning.

## Don't

- ❌ Don't use Tab Item alone — it's designed for use inside a Segment Control or tab strip group.
- ❌ Don't swap Pickup/Deliver colors — the Yellow/Red convention is fixed across the Driver App.
- ❌ Don't put a Tab Item inside a Tab Bar (the bottom-of-screen navigation) — those use a different component.

---

Back to [[Design System]] · [[Component Status]].
