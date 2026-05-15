# Architecture

## Token philosophy
- **Primitive → Semantic.** Primitives are raw values (scales). Semantics are role-based aliases that point at primitives.
- Designs and code reference **semantic** tokens only. This lets us re-theme by remapping the semantic layer without touching screens.

## Modes
| Collection | Modes |
|---|---|
| [[Spacing]] | single |
| [[Border]] | single |
| [[Colors - Primitives]] | single |
| [[Colors - Semantic]] | Light, Dark |
| [[Typography - Primitives]] | single |
| [[Typography - Semantic]] | iOS |

## Naming
- Slash-separated namespaces: `Group/Subgroup/Variant` (e.g. `Background/Subtle Blue`, `Text/Link Pressed`).
- T-shirt sizing for scales (`XS S M L XL 2XL …`); numeric for color shades (`100 … 950`).
- Inverse, Pressed, Disabled, Subtle/Primary are recurring suffix concepts — keep them consistent across new tokens.

## Font stack
- `SF Pro` (Display) for large headings (Title, Large Title).
- `SF Pro Text` for body and UI copy.

## Recent renames / removals
- `Background/Secondary {Blue|Green|Red|Yellow}` → `Background/Subtle …`
- Removed: `Background/Tretiary`, `Background/Inverse Pressed`, `Background/Error`, `Icon/Inverse Static 2`, `Text/Primary Inverse Static 2`.

## Counts (last sync)
- 234 variables across all collections
- 11 published styles (10 text + 1 grid)
- 58 primitive colors
- 18 spacing, 11 border tokens

Back to [[Design System]].
