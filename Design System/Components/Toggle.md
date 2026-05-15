# Toggle

iOS-style switch for an instant on/off setting. Tap flips the state immediately — no Save button needed. Used for preferences, feature flags, mode switches.

- **Component set node:** `268:1861`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=268-1861)
- **Figma section:** `----- Forms`
- **Figma documentation:** Section `1720:5154` "Toggle — Documentation" on the same page

---

## Composition

| Layer | Bindings |
|---|---|
| Track (variant root) | fill `Background/Subtle` (Off) / `Background/Primary Green` (On) — 51 × 31, capsule |
| Knob | fill `Text/Primary Inverse Static` (near-white) |

The Toggle has no internal label or text. Pair it with a label / [[Content Row]] in the surrounding layout.

---

## Variants — `State`

| State | Track fill | Use for |
|---|---|---|
| `Off` | `Background/Subtle` | Setting is disabled |
| `On` | `Background/Primary Green` | Setting is enabled |

---

## Instance properties

None. The Toggle has no instance properties — its only state is the variant.

---

## Do

- ✅ Use Toggle for instant, reversible on/off settings — the change applies immediately.
- ✅ Place Toggle on the trailing edge of a list row, paired with a leading label.
- ✅ Use the colour change (gray → green) as the only on/off affordance — no extra "On" / "Off" text needed.

## Don't

- ❌ Don't use Toggle for settings that need confirmation or save — use [[Checkbox]] inside a form with a Save button instead.
- ❌ Don't add text labels "On" / "Off" inside the toggle area — iOS convention is colour-only.
- ❌ Don't use Toggle for picking between two equal options (A vs B) — that's segmented control territory.
- ❌ Don't disable the Toggle to indicate a setting is unavailable without context — pair with a helper line explaining why.

---

Back to [[Design System]] · [[Component Status]].
