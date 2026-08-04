---
type: screen
status: in-review
figma: CHECKOUT/QUOTE FORM — `ABPgXbgmJ7MfISH38GmnBQ` · frame "Service Options" 434:7727 (1920×1376)
---

# Checkout / Quote — Service Options (step 1)

First page after the lead form redirect. Client picks one of three service tiers; the right rail
carries the locked quote context. Brand shown is a **white-label** skin (Diesel Auto Express),
not HaulEx — HaulEx appears only as a trust logo in the reviews strip.

Steps: **Plan** (this page) → Pickup → Delivery → Pay.

## Layout grid (exact, read from the file 2026-08-04)

| Region | node | x | y | w | h |
|---|---|---|---|---|---|
| Page frame | 434:7727 | — | — | 1920 | 1376 |
| Price-type toggle (Regular/Cash) | 434:8187 | 315 | 218 | 240 | 42 |
| Pricing Options (3 cards) | 434:7731 | 315 | 279.5 | 921 | 554 |
| Contact Info (weak text block) | 434:7728 | 315 | 854 | 352 | 61 |
| Reviews / trust block | 434:8106 | 315 | 950 | 921 | 397 |
| Shipping Details rail | 434:7954 | 1266 | 230 | 344 | 1117 |

- Content margin **315** both sides; main column **921**; rail **344**; gutter **30**.
- Cards: 297 / 297 / **317** wide — the third is 20px wider than its siblings. Likely unintentional.
- Cards bottom = 833.5, reviews top = 950 → only **116.5px** of vertical space between them.

## Colors (sampled, not guessed)

The palette is **Flowbite** (gray-50 `#F9FAFB`, gray-100 `#F3F4F6`, gray-200 `#E5E7EB`,
gray-500 `#6B7280`, blue-600 `#1C64F2`) with **one off-palette custom red**.

| Role | Value | Where |
|---|---|---|
| Commit / CTA red | **`#FB3D37`** (custom — not a Flowbite stop) | the three "Choose …" button fills |
| Outline red | **`#C81E1E`** (Flowbite red-700) | Button `Outline=True` border + label |
| Selection blue | **`#1C64F2`** | Prime card's 2px border · phone link |
| Card surface | `#F9FAFB` + 1px `#E5E7EB`, radius 4 | all three tier cards |
| Reviews surface | `#F3F4F6` + 1px `#E5E7EB`, radius 4 | trust block |

**Two accents carry two different meanings** — red = commit, blue = selected/link. Anything new on
this page has to pick one deliberately. A blue element reads as "selectable option"; a red one reads
as "commit now".

**Surface ladder:** page `#FFFFFF` → cards `#F9FAFB` → reviews `#F3F4F6`. Plain white is *unused as
a container*, which makes it available for a new object class that must not read as a card.

## ⚠️ `#FB3D37` fails WCAG AA

White 14px SemiBold on `#FB3D37` = **3.61:1**. AA needs 4.5:1 for text this size. This affects all
three existing "Choose …" buttons — pre-existing, not introduced by any new work.

Fixes that keep the hue: **`#E02424`** (Flowbite red-600) = 4.72:1 ✓ · `#C81E1E` (red-700) = 5.74:1 ✓.
The component set's own `Outline=True` red is already `#C81E1E`, so the outline variants pass by
construction — only the filled ones are short.

## Local `Button` component set

A real variant set in this file, richer than the page currently uses:

| Axis | Options |
|---|---|
| **Color** | Green · Red · White · Primary · Alternative · Alternative Dark · Dark · Gray |
| **Size** | xs (34) · sm (37) · base (41) · l (48) · xl (52) |
| **State** | Default · Hover · Focus |
| **Outline** | False · True |
| **Icon only** | False · True |

Plus text/icon props (`Button text`, `Show left/right icon`, `Left/Right icon style`).

- **`Outline=True` already exists** — border + label `#C81E1E`, no fill, radius **8**, gap 8.
  A lower-emphasis red CTA needs no new component, just a property flip.
- Radius mismatch: outline variants are **radius 8**, but the card instances are overridden to
  **radius 4** to match the cards. Override to 4 for anything on this page.
- Card buttons are `Color=Red, Size=l, Outline=False` at 245×**45** — note `Size=l` is 48 in the set,
  so the instances are also height-overridden.

## Open item — CTA under the prices

`Contact Info` (434:7728) is currently 12px gray body copy + a blue phone number, 352px wide in a
921px column. It has no visual weight and the blue number is the page's only stray link.

**Three variants built 2026-08-04** in section `CTA options under prices — A / B / C` (435:12841),
at canvas x=-14280 y=965 — full clones of the page, one per option, for in-context comparison:

| Opt | Frame | Band | Treatment |
|---|---|---|---|
| **A** assist band | 435:11265 | 435:11775 | 921×84 @ y=858 · white · 1px `#E5E7EB` · radius 4 · 4px `#FB3D37` left edge · `Color=Red Size=base Outline=True` button · reviews → y=974 |
| **B** inline one-liner ✅ **chosen** | 435:11793 | ~~435:12303~~ → **436:12872** | see *Refined B* below |
| **C** inverted dark | 435:12314 | 435:12824 | 921×84 @ y=858 · `#111827` fill · `Color=White Outline=False` button · reviews → y=974 |

Shared: 40px icon badge (`#FEF2F2` / `#374151`) reusing the *24/7 Customer Support* person glyph
cloned from 434:8088 — the icon library has no headset or phone component (only `plus`, `forward`,
`arrow-up`, `chevron-down`). Copy: "Not sure which option fits?" + "Talk to a transport specialist —
free, no obligation." Phone set as one text node with a range override (13 Regular `#6B7280` label,
15 SemiBold number).

### Two build gotchas worth remembering
1. **The `Button` set defaults `Show left icon` / `Show right icon` to ON**, with a flame glyph — a
   fresh `createInstance()` renders 🔥 either side of the label. Must explicitly set both false.
2. **Recoloring a cloned icon instance:** setting `fills` on the instance node paints its *frame
   background* → a solid square. Set `fills = []` on the instance and recolor only its `VECTOR`
   descendants.

Also: instance `cornerRadius` must be overridden 8 → 4 per this page's convention.

### Refined B — the chosen direction (`Pricing Help — B` 436:12872)

Owner picked B, then flagged it as reading "like beta". Diagnosis and fixes:

| Read as unfinished because | Fix |
|---|---|
| 37px outlined button inside a 20px whisper row — the control outweighed everything around it | **Replaced with a text link**: "Talk to a specialist" 13 SemiBold `#C81E1E` + 11px right chevron |
| lone 17px `#6B7280` person glyph sat at the same value as the text — read as noise, and "person" ≠ "specialist" | **Removed the icon entirely** |
| row floated in dead space, closer to the reviews block than to the cards it belongs to | **1px `#E5E7EB` rule at full 921 width above it** — makes it the pricing block's footer, not an orphan |
| B had silently **dropped the phone number** that the original `Contact Info` carried | **Restored**, separated by a 1×14 `#E5E7EB` vertical rule |
| one flat 13px run, no hierarchy | Three tiers: muted question `#6B7280` → accent action `#C81E1E` → dark number `#111827` |

**Structure:** `Pricing Help — B` at x=315 y=864, w=921, VERTICAL auto-layout, gap 20,
counter-axis CENTER, height 41 (hugs). Children: full-width rule (`layoutAlign: STRETCH`), then
`Line` — HORIZONTAL gap 16 — holding `Ask` (nested HORIZONTAL gap 6: question + `Link` gap 5) ·
vertical rule · phone text.

**Rhythm:** 30.5 above / 45 below. Deliberately not centered in the 116.5px gap — weighting it
toward the cards signals it belongs to the pricing decision; the larger gap below separates it from
the reviews section.

**Accent now comes from the red link text, not a box.** `#C81E1E` on white = 5.74:1 ✓ AA, and it's
the only red text in the main column, so it draws the eye with no container at all.

**Icon note:** no right-arrow component exists. `forward` (31:13889) is a *curved reply* arrow —
wrong semantics. Used `chevron-down` (31:13903) with `rotation = 90` to point right. Square icons
rotate safely inside auto-layout (bounding box unchanged).

The constraint driving every choice: it must **not** read as a fourth service tier. Four axes of
separation — horizontal not vertical · outline not filled · white not gray · no price, no star, no
checkmark list (the three signatures of a tier card here).

Rejected: red-tinted fill (`#FEF2F2` bands read as error states, and the rail's disclaimer is
already red text) · gray fill (would bond visually with the reviews block below) · filled red button
(creates a fourth equal CTA and flattens the three-way comparison).

## Follow-ups
- [ ] Decide the band (A assist band / B inline one-liner / C inverted dark).
- [ ] Copy: "Contact sales" is B2B register for a consumer car-shipping funnel — "Talk to a specialist" fits better.
- [ ] Fix the filled-red AA failure → `#E02424`.
- [ ] Third tier card is 317 vs 297 — confirm intentional.
- [ ] Reconcile `#FB3D37` against the Flowbite red ramp, or document it as a brand override.

Back to [[Hub]].
