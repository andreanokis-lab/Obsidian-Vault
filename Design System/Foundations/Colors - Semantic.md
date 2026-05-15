# Colors — Semantic

Semantic color tokens with **Light** and **Dark** modes. Always use semantic tokens in designs — never reference [[Colors - Primitives|primitives]] directly. The semantic layer is what lets the system re-theme without touching individual screens.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Page:** `0:1` — `----- Colors`
- **Modes:** Light, Dark
- **Total tokens:** 56 semantic tokens across 4 groups
- **Visualization:** Section `1696:1621` "Semantic Colors — Visualization" on `----- Colors` page — documentation layout with 4 group sections (Text, Background, Border, Icon). Each token card shows Light + Dark swatch pair (live-bound to the variable via `setBoundVariableForPaint` + per-swatch mode override), hex values, "Use for" description, and per-group "Don't" rules. Re-run the build script to refresh after any token change.

---

## How modes work

| Collection | Modes |
|---|---|
| Colors / Semantic | **Light + Dark** |
| Colors / Primitive | Single mode — feeds semantics only |

Apply the correct mode to every frame. Screens inherit the mode of their nearest parent frame. Never override a token's value directly — swap the mode instead.

---

## Group 1 — Text

Used for all typographic content: headings, body, labels, placeholders, links, status messages.

| Token | Light | Dark | Primitive ref |
|---|---|---|---|
| `Text/Primary` | `#0D0D0D` | `#F2F2F2` | neutral/950 → neutral/50 |
| `Text/Secondary` | `#262626` | `#E5E5E5` | neutral/850 → neutral/100 |
| `Text/Tertiary` | `#4C4C4C` | `#CCCCCC` | neutral/700 → neutral/200 |
| `Text/Disabled` | `#A6A6A6` | `#4C4C4C` | neutral/350 → neutral/700 |
| `Text/Primary Inverse` | `#F2F2F2` | `#0D0D0D` | neutral/50 → neutral/950 |
| `Text/Secondary Inverse` | `#E5E5E5` | `#262626` | neutral/100 → neutral/850 |
| `Text/Tertiary Inverse` | `#D9D9D9` | `#595959` | neutral/150 → neutral/650 |
| `Text/Primary Inverse Static` | `#F2F2F2` | `#F2F2F2` | neutral/50 (both) |
| `Text/Link` | `#007AFF` | `#3395FF` | blue/500 → blue/400 |
| `Text/Link Pressed` | `#004999` | `#66AFFF` | blue/700 → blue/300 |
| `Text/Negative` | `#FF3B30` | `#FF3B30` | red/500 (both) |
| `Text/Negative Pressed` | `#99231D` | `#FF8983` | red/700 → red/300 |
| `Text/Positive` | `#2CA44A` | `#2CA44A` | green/500 (both) |
| `Text/Warning` | `#96790D` | `#FACA15` | yellow/700 → yellow/500 |
| `Text/Status Red` | `#FF3B30` | `#FF3B30` | red/500 (both) |
| `Text/Status Green` | `#56B66E` | `#56B66E` | green/400 (both) |
| `Text/Status Yellow` | `#FBD544` | `#FBD544` | yellow/400 (both) |
| `Text/Status Blue` | `#007AFF` | `#007AFF` | blue/500 (both) |

### When to use — Text

| Token                               | Use for                                                                                                                         |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `Text/Primary`                      | All main body copy, headings, list primary labels, form field values                                                            |
| `Text/Secondary`                    | Supporting text, subtitles, metadata below a primary label                                                                      |
| `Text/Tertiary`                     | Placeholders inside inputs, hints, timestamps, fine print                                                                       |
| `Text/Disabled`                     | Labels, input values, or any text on a disabled control                                                                         |
| `Text/Primary Inverse`              | Text that sits on `Background/Inverse` (dark surface in light mode)                                                             |
| `Text/Primary Inverse Static`       | Text on always-dark surfaces regardless of mode — e.g. dark overlays, black Badge type, camera UI                               |
| `Text/Link`                         | Tappable text links, "View all", "Learn more" actions                                                                           |
| `Text/Negative`                     | Inline validation errors, destructive action labels                                                                             |
| `Text/Positive`                     | Confirmation messages, success labels                                                                                           |
| `Text/Warning`                      | Caution labels — use sparingly; warn does not mean error. Light mode uses yellow/700 (`#96790D`) for legibility on light surfaces; dark mode uses yellow/500 (`#FACA15`) |
| `Text/Status Red/Green/Yellow/Blue` | Static status text in badges, list rows, and indicators — these never flip in dark mode so they stay readable on any background |

### Don't — Text

- ❌ Do not use `Text/Primary Inverse Static` for regular inverted text — it is for always-dark surfaces only. Use `Text/Primary Inverse` for mode-aware inverse text.
- ❌ Do not use `Text/Tertiary` for a label above a required form field — it reads as disabled. Use `Text/Secondary`.
- ❌ Do not use `Text/Status *` tokens for general body text — they are semantically tied to status indicators and will confuse intent.
- ❌ Do not use `Text/Warning` on a light background expecting bright yellow — the light-mode value is `#96790D` (yellow/700), not `#FACA15`. The bright yellow only appears in dark mode.

---

## Group 2 — Background

Used for screen surfaces, cards, input fills, overlays, and colored action backgrounds.

| Token | Light | Dark | Primitive ref |
|---|---|---|---|
| `Background/Primary` | `#F2F2F2` | `#0D0D0D` | neutral/50 → neutral/950 |
| `Background/Subtle` | `#E5E5E5` | `#262626` | neutral/100 → neutral/850 |
| `Background/Subtle Pressed` | `#D9D9D9` | `#404040` | neutral/150 → neutral/750 |
| `Background/Inverse` | `#0D0D0D` | `#F2F2F2` | neutral/950 → neutral/50 |
| `Background/Inverse Static` | `#0D0D0D` | `#0D0D0D` | neutral/950 (both) |
| `Background/Disabled` | `#D9D9D9` | `#1A1A1A` | neutral/150 → neutral/900 |
| `Background/Mono` | `#1A1A1A` | `#F2F2F2` | neutral/900 → neutral/50 |
| `Background/Mono Pressed` | `#404040` | `#BFBFBF` | neutral/750 → neutral/250 |
| `Background/Primary Blue` | `#007AFF` | `#007AFF` | blue/500 (both) |
| `Background/Primary Blue Pressed` | `#004999` | `#66AFFF` | blue/700 → blue/300 |
| `Background/Subtle Blue` | `#CCE4FF` | `#003166` | blue/100 → blue/800 |
| `Background/Primary Green` | `#2CA44A` | `#2CA44A` | green/500 (both) |
| `Background/Primary Green Pressed` | `#1A622C` | `#80C892` | green/700 → green/300 |
| `Background/Subtle Green` | `#D5EDDB` | `#12421E` | green/100 → green/800 |
| `Background/Primary Red` | `#CC2F26` | `#CC2F26` | red/600 (both) |
| `Background/Primary Red Pressed` | `#99231D` | `#FF8983` | red/700 → red/300 |
| `Background/Subtle Red` | `#FFD8D6` | `#661813` | red/100 → red/800 |
| `Background/Primary Yellow` | `#FACA15` | `#FACA15` | yellow/500 (both) |
| `Background/Primary Yellow Pressed` | `#96790D` | `#FCDF73` | yellow/700 → yellow/300 |
| `Background/Subtle Yellow` | `#FEF4D0` | `#645108` | yellow/100 → yellow/800 |

### When to use — Background

| Token | Use for |
|---|---|
| `Background/Primary` | Top-level screen background, root-level surfaces |
| `Background/Subtle` | Cards, list rows, input field fills, sheet content areas, secondary surfaces layered on Primary |
| `Background/Subtle Pressed` | Pressed/highlighted state of any subtle-background element (list row tap, card tap) |
| `Background/Inverse` | Dark surfaces overlaid on a light screen — mode-aware (becomes light in dark mode) |
| `Background/Inverse Static` | Always-dark surface regardless of mode — camera UI overlays, black Badge type, dark bottom bars |
| `Background/Disabled` | Fill of disabled buttons, disabled input fields |
| `Background/Mono` | The primary dark CTA button fill (the "default" action button — monochrome across modes) |
| `Background/Mono Pressed` | Pressed state of the Mono button |
| `Background/Primary Blue` | Blue CTA button (confirm, submit, default blue action) |
| `Background/Primary Green` | Green CTA button (approve, complete, success action) |
| `Background/Primary Red` | Red CTA button (delete, reject, destructive action) |
| `Background/Primary Yellow` | Yellow CTA (caution/warning action — use sparingly) |
| `Background/Subtle {Color}` | Tinted background for status badges, callout cards, info banners — never for full screens |

### Don't — Background

- ❌ Do not use `Background/Subtle` for top-level screen backgrounds — use `Background/Primary`. Subtle is one level up.
- ❌ Do not use `Background/Inverse Static` where `Background/Inverse` would work — Static bypasses dark mode and is only for surfaces that must stay dark in both modes (camera, overlays with fixed contrast requirements).
- ❌ Do not put colored text on `Background/Subtle {Color}` without verifying contrast — e.g. `Text/Status Yellow` on `Background/Subtle Yellow` (light mode) fails 4.5:1.
- ❌ Do not use `Background/Primary Yellow` for a primary CTA unless it is specifically a warning/caution action — users read yellow as "proceed with care", not "go".
- ❌ Do not mix `Background/Mono` and `Background/Primary Blue` in the same button row — they look similar in dark mode and create visual ambiguity. Pick one.


---

## Group 3 — Border

Used for input outlines, dividers, card strokes, and focus rings.

| Token | Light | Dark | Primitive ref |
|---|---|---|---|
| `Border/Primary` | `#BFBFBF` | `#4C4C4C` | neutral/250 → neutral/700 |
| `Border/Subtle` | `#E5E5E5` | `#262626` | neutral/100 → neutral/850 |
| `Border/Inverse` | `#F2F2F2` | `#1A1A1A` | neutral/50 → neutral/900 |
| `Border/Inverse Static` | `#F2F2F2` | `#F2F2F2` | neutral/50 (both) |
| `Border/Disabled` | `#CCCCCC` | `#333333` | neutral/200 → neutral/800 |
| `Border/Blue` | `#007AFF` | `#3395FF` | blue/500 → blue/400 |
| `Border/Positive` | `#2CA44A` | `#2CA44A` | green/500 (both) |
| `Border/Negative` | `#FF3B30` | `#FF3B30` | red/500 (both) |
| `Border/Yellow` | `#FACA15` | `#FBD544` | yellow/500 → yellow/400 |

### When to use — Border

| Token | Use for |
|---|---|
| `Border/Primary` | Default visible border on input fields, cards with explicit stroke, dividers between sections |
| `Border/Subtle` | Low-contrast separators — list row dividers, hairline borders between content areas |
| `Border/Inverse Static` | Borders on always-dark surfaces — e.g. outlines on camera overlays, white ring on Avatar |
| `Border/Disabled` | Border of disabled input fields and disabled buttons with outline style |
| `Border/Blue` | Focused state of input fields |
| `Border/Positive` | Input in valid/positive state |
| `Border/Negative` | Input in error state, destructive action outlines |
| `Border/Yellow` | Input in warning state |

### Don't — Border

- ❌ Do not use `Border/Primary` as a list row divider — it is too heavy. Use `Border/Subtle` for separators.
- ❌ Do not use `Border/Subtle` as a card stroke on `Background/Subtle` — insufficient contrast. Use `Border/Primary` when the card background matches the surface.
- ❌ Do not use `Border/Negative` for anything other than validation error states — it carries inherent "error" semantics and will mislead users.
- ❌ Do not apply `Border/Inverse Static` in normal light/dark UI — it only exists for surfaces that stay permanently dark (camera, sheet overlays).

---

## Group 4 — Icon

Used for all iconography: navigation icons, list row leading icons, action buttons, status indicators.

| Token | Light | Dark | Primitive ref |
|---|---|---|---|
| `Icon/Primary` | `#1A1A1A` | `#F2F2F2` | neutral/900 → neutral/50 |
| `Icon/Subtle` | `#666666` | `#666666` | neutral/600 (both) |
| `Icon/Inverse` | `#F2F2F2` | `#1A1A1A` | neutral/50 → neutral/900 |
| `Icon/Inverse Static` | `#F2F2F2` | `#F2F2F2` | neutral/50 (both) |
| `Icon/Disabled` | `#A6A6A6` | `#4C4C4C` | neutral/350 → neutral/700 |
| `Icon/Blue` | `#007AFF` | `#007AFF` | blue/500 (both) |
| `Icon/Positive` | `#2CA44A` | `#2CA44A` | green/500 (both) |
| `Icon/Negative` | `#FF3B30` | `#FF3B30` | red/500 (both) |
| `Icon/Yellow` | `#FACA15` | `#FACA15` | yellow/500 (both) |

### When to use — Icon

| Token | Use for |
|---|---|
| `Icon/Primary` | Default icons — navigation bar icons, list row leading icons, button icons |
| `Icon/Subtle` | Disclosure chevrons, decorative icons, secondary / non-interactive icons |
| `Icon/Inverse` | Icons on `Background/Inverse` surfaces — mode-aware |
| `Icon/Inverse Static` | Icons on always-dark surfaces — camera UI, black badge icons, overlays |
| `Icon/Disabled` | Icons inside disabled controls |
| `Icon/Blue` | Active tab bar icon, tinted action icon |
| `Icon/Positive` | Success status icon (checkmark, green indicator) |
| `Icon/Negative` | Error / destructive icon (X, warning on destructive action) |
| `Icon/Yellow` | Warning icon |

### Don't — Icon

- ❌ Do not use `Icon/Primary` on a colored (`Background/Primary Blue` etc.) surface — it has no contrast. Use `Icon/Inverse Static` or `Icon/Inverse` instead.
- ❌ Do not use `Icon/Subtle` for interactive icons — it implies non-interactivity. Reserve it for disclosure arrows and decorative glyphs.
- ❌ Do not use `Icon/Blue` for a disabled state — use `Icon/Disabled`. Blue implies interactive/active.
- ❌ Do not use status icon tokens (`Icon/Positive`, `Icon/Negative`, `Icon/Yellow`) for non-status purposes — they carry semantic weight that contradicts general-purpose icon use.

---

## Removed / renamed tokens

These tokens existed in earlier versions. Do not use them in new designs.

| Old token | Replaced by |
|---|---|
| `Background/Secondary Blue` | `Background/Subtle Blue` |
| `Background/Secondary Green` | `Background/Subtle Green` |
| `Background/Secondary Red` | `Background/Subtle Red` |
| `Background/Secondary Yellow` | `Background/Subtle Yellow` |
| `Background/Tretiary` | removed — use `Background/Subtle` |
| `Background/Inverse Pressed` | removed |
| `Background/Error` | `Background/Subtle Red` |
| `Icon/Inverse Static 2` | removed |
| `Text/Primary Inverse Static 2` | removed |

---

## The rule in one sentence

> Use the most specific token that fits the context. `Text/Status Green` beats `Text/Positive` in a status badge. `Background/Primary Blue` beats `Background/Mono` for a blue CTA.

---

## Contrast quick-reference (WCAG AA)

All foreground/background pairings must reach **4.5:1** for normal text, **3:1** for large text (18pt+) and UI components.

| Pairing | Ratio | Pass |
|---|---|---|
| `Text/Primary` on `Background/Primary` (Light) | ~17:1 | ✅ AAA |
| `Text/Secondary` on `Background/Primary` (Light) | ~9:1 | ✅ AAA |
| `Text/Tertiary` on `Background/Primary` (Light) | ~4.6:1 | ✅ AA |
| `Text/Disabled` on `Background/Primary` (Light) | ~2.3:1 | ❌ decorative only |
| `Text/Primary Inverse Static` on `Background/Inverse Static` | ~17:1 | ✅ AAA |
| `Text/Link` on `Background/Primary` (Light) | ~4.5:1 | ✅ AA (borderline) |
| `Text/Negative` on `Background/Primary` (Light) | ~4.8:1 | ✅ AA |
| `Icon/Primary Inverse Static` on colored CTA backgrounds | verify per color | check individually |

> Disabled states are intentionally below AA — they communicate inactivity. Do not "fix" disabled contrast by making tokens darker; that breaks the intentional dimmed affordance.

---

Back to [[Design System]] · [[Architecture]] · [[Rules]].
