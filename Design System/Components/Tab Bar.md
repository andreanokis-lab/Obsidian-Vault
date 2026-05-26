---
status: built
figma_node: 317:3058
file_key: 3qOFF7kHsaZPfdftDb1CVz
---

# Tab Bar

iOS bottom tab bar — primary navigation between top-level destinations. 3-tab layout, one tab active at a time. The active tab shows a blue icon + label; inactive tabs are tertiary text. Sits above the home indicator with a translucent chrome material.

**Figma:** [HaulEx UIKit · Tab Bar](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=317-2557)
**Component set:** `317:3058`
**Library key:** `170058e75c2c6e5ee54217439ed499f70b2000ba`

---

## Variants — `Selected`

| Selected | Node | Active tab |
|---|---|---|
| 1 | `317:3055` | Left tab |
| 2 | `317:3056` | Middle tab |
| 3 | `317:3057` | Right tab |

Width 393pt, height 83pt.

---

## Anatomy

```
┌───────────────────────────────────────────┐   ← Chrome material: backdrop-blur 25, top border 0.333pt Border/Subtle
│                                           │     top border = Border/Subtle
│   🏠         🔔         👤               │   ← Icon row (18pt SF Symbols, 510 weight)
│  Tab Name   Tab Name   Tab Name          │   ← Caption labels (12 / 16)
│                                           │
└───────────────────────────────────────────┘
```

- **Outer frame:** 393×83pt, `background/primary` (`#0d0d0d`)
- **Chrome material:** absolute fill, `backdrop-blur 25px`, top border `0.333pt` solid `Border/Subtle`
- **Tab Bar Buttons row:** anchored 7pt from top, 3 equal-width children (`flex-1`), space-between
- **Each tab cell:** height 40pt
  - **Icon:** absolute, top ~2.5%, 18pt SF Pro Medium (510 weight), font feature `ss16` (SF Symbols)
  - **Label:** absolute below icon, `Meta/Caption` (12 / 16), slightly overflowing left/right (-1.04% inset) for centering
- **Active/inactive state** is driven only by color — icon and label both flip together

---

## Tokens

**Colors**
- Frame: `Background/Primary` (`#0d0d0d`)
- Top border: `Border/Subtle` (`#262626`), width `0.333pt`
- Active tab icon + label: `Text/Status Blue` (`#007aff`)
- Inactive tab icon + label: `Text/Tertiary` (`#ccc`)

**Type**
- Label: `Meta/Caption` (12 / 16, regular)
- Icon: SF Pro Medium 18pt (SF Symbols, not a text style — driven by symbol property)

**Effects**
- Chrome material: `backdrop-filter: blur(25px)` over the underlying screen content

---

## Composition notes

- The component is NOT composed of [[Components/Tab Item|Tab Item]] instances — it's a flat inline implementation. `Tab Item` is a separate atom used in other contexts (e.g. order status tabs).
- Tabs are equal-width via `flex-[1_0_0]` with `space-between` distribution.

---

## Usage rules

- Use only at the bottom of a screen, never elsewhere.
- Always 3 tabs in the current build. If the app needs 4 or 5 tabs, file a new variant (see [[Component Status]] before drawing ad-hoc).
- Active tab is mandatory — exactly one tab must be active at any time.
- Color alone conveys active state — pair with the icon symbol change so colorblind users can still tell ([[Rules]] A1).
- Each tab cell is full-width / full-height (≥44pt tap target met by the 83pt bar height) ([[Rules]] L1).
- Place above the bottom safe-area inset (34pt for Dynamic Island / notch devices) ([[Rules]] L4).
- See [[Navigation Patterns]] for tab vs nav stack decisions.

---

## Component properties

- `selected` — `1 \| 2 \| 3`
- `tabName1`, `tabName2`, `tabName3` — label string per tab
- `symbol1`, `symbol2`, `symbol3` — SF Symbols glyph per tab (Private Use Area code point)

---

## Related

- Strategy / when to use: [[Navigation Patterns]]
- Atom alternative for non-tab-bar tab contexts: [[Components/Tab Item|Tab Item]]

Back to [[Design System]] · [[Component Status]].
