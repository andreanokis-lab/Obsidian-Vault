# Spacing & Grid

20 FLOAT tokens, single mode. Use for padding, gaps, margins, and (where noted) corner radius and element height. **Never type pt values manually — always bind to a `Space/*` variable.**

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Collection:** `Spacing`
- **Mode:** single
- **Total tokens:** 20
- **Visualization:** Section `1702:6258` "Spacing & Grid — Visualization" on `----- Grid & Spacing` page.
- **Usage evidence:** All rules below are grounded in a binding scan of the **DS page** in the HaulEx Driver App file — ~22,675 spacing/radius bindings across ~13,700 nodes.

---

## Token spec

| Token | px | Real usage in DS page | Verdict |
|---|---|---|---|
| `Space/Zero` | 0 | ~4,800 bindings — used to explicitly lock padding and corner radius to 0 | ✅ Core |
| `Space/2XS` | 2 | ~120 bindings — tight icon-internal padding and stacks | ✅ Core |
| `Space/XS` | 4 | ~3,500 bindings — dominant vertical inner padding (≈930 paddingT, ≈930 paddingB) and dense itemSpacing | ✅ Core |
| `Space/S` | 8 | ~5,500 bindings — **most-used gap token** (≈2,300 itemSpacing) | ✅ Core |
| `Space/M` | 12 | ~1,100 bindings — symmetric card padding (≈200 each side) + itemSpacing | ✅ Core |
| `Space/L` | 16 | ~1,700 bindings — paddingLeft (≈680) + paddingRight (≈770) = **screen margins**; itemSpacing (≈280); also grid gutter | ✅ Core |
| `Space/X` | 20 | 4 bindings — `itemSpacing` only, on 4 FRAMEs. Off-ladder. | ⚠️ Niche |
| `Space/XL` | 24 | ~190 bindings — mostly itemSpacing for wider gaps | ✅ Used |
| `Space/2XL` | 32 | ~30 bindings — itemSpacing only | ⚠️ Rare |
| `Space/3XL` | 40 | ~17 bindings — paddingT/B/L/R on instances | ⚠️ Rare |
| `Space/TapTarget` | 44 | 0 bindings (rule, not yet observed) | ❌ Reserved |
| `Space/4XL` | 48 | ~125 bindings — **used as `height` (~120)**, not as spacing | ✅ Used (as size) |
| `Space/5XL` | 56 | 0 bindings | ❌ Reserved |
| `Space/6XL` | 64 | 1 binding | ❌ Reserved |
| `Space/7XL` | 72 | 0 bindings | ❌ Reserved |
| `Space/8XL` | 80 | 0 bindings | ❌ Reserved |
| `Space/9XL` | 88 | 0 bindings | ❌ Reserved |
| `Space/10XL` | 96 | 0 bindings | ❌ Reserved |
| `Space/11XL` | 104 | 0 bindings | ❌ Reserved |
| `Space/12XL` | 112 | 0 bindings | ❌ Reserved |

Verdicts:
- **✅ Core** — load-bearing, used hundreds+ of times. Touch only with caution.
- **✅ Used** — present in production with a clear role.
- **⚠️ Niche / Rare** — fewer than ~30 bindings. Keep, but justify additions.
- **❌ Reserved** — zero (or one stray) bindings. Kept by decision, not by demand.

Reserved tokens (TapTarget, 5XL–12XL plus 6XL with one stray) live in the collection but have no production footprint as of this audit. Apple HIG's 44pt tap-target rule is the reason `Space/TapTarget` stays even though no node currently binds it.

`Space/4XL` (48pt) is in practice a **sizing token, not a spacing token** — every observed binding is on the `height` property. Treat 48 as the standard control height, not as a gap.

---

## Grid

Every iOS frame uses a layout grid:

| Property | Value |
|---|---|
| Pattern | `COLUMNS` |
| Count | 4 |
| Margin (offset) | 16pt — `Space/L` |
| Gutter | 16pt — `Space/L` |
| Alignment | `STRETCH` |
| Reference frame | iPhone 14 & 15 Pro · 393×852pt |

Both margin and gutter alias to `Space/L`, so column metrics shift in lockstep with the screen-margin token. Use the grid for horizontal placement decisions. Vertical rhythm is governed by the `Space/*` tokens.

---

## Do — evidence-based

- ✅ `Space/L` (16pt) is the **universal horizontal screen margin** — confirmed by ~1,450 paddingLeft/Right bindings on screen-level frames.
- ✅ `Space/S` (8pt) is the **default item gap** — ~2,300 itemSpacing bindings make it the dominant gap token.
- ✅ `Space/XS` (4pt) is the **default tight vertical padding** for dense stacks — ~1,860 paddingTop+paddingBottom bindings.
- ✅ `Space/M` (12pt) is the **symmetric card padding** — used on all four sides equally (~200 each), not just vertical.
- ✅ `Space/Zero` (0pt) is the **explicit "no spacing / square corners" binding** — don't leave 0 as an inferred default; bind it.
- ✅ `Space/4XL` (48pt) is the **standard control height** — bind to `height` for buttons, rows, inputs. Not for gaps.
- ✅ `Space/TapTarget` (44pt) is the **minimum tap target size** (Apple HIG). Bind to `minHeight`/`minWidth` on interactive elements even when content is smaller.

## Don't — evidence-based

- ❌ Don't type pt values manually. Bind to `Space/*` variables only.
- ❌ Don't use `Space/4XL` (48pt) as a gap or padding — every observed binding is `height`. Mixing roles will break the implicit "this token = control height" convention.
- ❌ Don't reach for tokens above `Space/4XL` — `Space/5XL`–`Space/12XL` have **zero** production bindings. If you need >48pt of space, justify it before binding.
- ❌ Don't add new "in-between" tokens. `Space/X` (20pt) is already an off-ladder oddity used only 4 times; the system doesn't need more of those.
- ❌ Don't assume `Space/M` is only for list rows (old guidance) — in practice it's general-purpose symmetric padding.
- ❌ Don't delete `Space/X` (20pt) without first scanning the consumer file. It's used in 4 Driver App bindings.

---

## Removed / renamed

| Old        | New               | Reason                                                                                        |
| ---------- | ----------------- | --------------------------------------------------------------------------------------------- |
| `Space/44` | `Space/TapTarget` | Numeric name didn't convey semantic intent. Token is currently a reserved rule, not used yet. |

Back to [[Design System]] · [[Rules]].
