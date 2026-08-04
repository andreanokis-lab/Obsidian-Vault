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
| row floated in dead space, closer to the reviews block than to the cards it belongs to | **1px `#E5E7EB` rule at full 921 width above it** — makes it the pricing block's footer, not an orphan |
| lone 17px `#6B7280` person glyph sat at the same value as the text — read as noise, and "person" ≠ "specialist" | **Removed the icon entirely** |
| B had silently **dropped the phone number** that the original `Contact Info` carried | **Restored** as the fallback action |
| one flat 13px run, no hierarchy | Three tiers: muted question `#6B7280` → accent button `#C81E1E` → dark number `#111827` |

### ⚠️ What this section is actually for — price-objection recovery

**Corrected by the owner 2026-08-04, and it changes the whole brief.** Every earlier draft read this
as a *choice* problem ("Not sure which option fits?" — help the user pick between three tiers). It
isn't. The real job is **catching the customer whose reaction to the number is to close the tab**:

- the price came back higher than they hoped, **or**
- the auto-quote generated wrong from the details they entered, **or**
- they just don't like the price.

**Desired outcome: they pick up the phone instead of bouncing.** Not "they understand the tiers."

Confusion copy and price-shock copy are opposites — "let me help you choose" vs "this number isn't
final and asking costs you nothing." Three conditions or they still leave:

1. **Name the objection in their own words.** They're already thinking "that's too much." Saying it
   out loud is what interrupts the exit; an unspoken objection just becomes a bounce.
2. **Give a legitimate reason the number could be wrong.** The quote is auto-generated from
   user-entered details, and the rail's own disclaimer already says final cost depends on vehicle
   condition, modifications, and handling. So "estimate" is *honest and already on the page* — it
   doesn't undercut the three prices above.
3. **Make calling feel free.** Anyone spooked by a price will not click something that smells like a
   salesperson. "free", "no obligation" is load-bearing, not filler.

**Final copy:**
> **Price not working for you?** (14 SemiBold `#111827`)
> Quotes are estimates — we can review yours, free. (13 Regular `#6B7280`)
> → button: **Call (360) 539 8600**

"Price not working for you?" was chosen over the sharper "Price higher than you expected?" because it
covers all three cases (too high · generated wrong · just doesn't suit) without presuming which,
and "not working" implies it can be worked on.

**The phone number moved *into* the button.** Since the goal is a call, the accented control and the
number are now the same object — nothing to hunt for, and it becomes a `tel:` link on mobile. The
separate "or call …" text was deleted as redundant. Avoid a second competing action here; two CTAs
dilute the one behaviour this section exists to produce.

### The button stays — it wasn't the control that was wrong

First pass replaced the outlined button with a red text link, on the theory that a 37px control
inside a 20px row was the mismatch. **Owner overruled: keep the button.** Correct call — the
mismatch was the *missing structure*, not the control. Once the full-width rule anchors the row and
the text has hierarchy, a 37px button reads as a deliberate footer action rather than a chip
floating in whitespace. The link version was solving the wrong problem.

**Final action:** `Button — Call` **437:12904** — `Color=Red · Size=l · Outline=True · State=Default`
(variant **2:1146**), **245×45**, radius 4, padding V 12/12, label "Call (360) 539 8600" **14
SemiBold** `#C81E1E`, 1px `#C81E1E` border, both icon booleans off. *(No phone icon exists in the
file — the whole icon library is `plus`, `forward`, `arrow-up`, `chevron-down`. A phone glyph before
the number would strengthen it but needs a new asset.)*

#### Why these exact numbers — "make it more consistent"

Owner rejected the first button as inconsistent. Measuring against the page's *only* other button
(the card CTA 434:7797) showed three real outliers, not a taste problem:

| | Card CTA (434:7797) | first attempt | now |
|---|---|---|---|
| size | 245×45 | 229×**37** | **245×45** ✓ |
| padding V | 12/12 | **8/8** | 12/12 ✓ |
| label weight | **SemiBold** | **Medium** | SemiBold ✓ |
| label size | 14 | 14 | 14 ✓ |
| radius | 4 | 4 | 4 ✓ |

`Size=sm` (37px) is a height that appears **nowhere else on the page** — that alone made it read as
foreign. The fix is geometric parity with the card CTAs: identical width, height, padding, radius and
type, differing *only* in fill weight (outline vs filled). Same button, quieter voice.

**⚠️ DS defect found:** the `Button` set's **`Outline=True` variants use Poppins Medium while the
filled variants use SemiBold**. The first button inherited Medium silently. Any outline instance needs
its label weight overridden to SemiBold until the set is fixed — see follow-ups.

Note `Size=l Outline=True` (2:1146) natively renders 182×48, radius 8, label **16 Medium** — so this
instance overrides height 48 → 45, radius 8 → 4, label 16 → 14 and Medium → SemiBold. The card CTAs
do the same 48 → 45 and 16 → 14 overrides, so heavy overriding is this page's existing convention,
not a shortcut.

**Structure** — `Price Objection — B` (436:12872) at x=315 y=858, w=921, h=64,
VERTICAL auto-layout, gap 20, counter-axis CENTER. Children:
1. full-width 1px `#E5E7EB` rule (`layoutAlign: STRETCH`)
2. `Line` — HORIZONTAL, gap 20, counter-axis CENTER — two siblings only:
   `Copy` (VERTICAL, gap 2: headline + subline) · `Button — Call`

Wrapper frames `Ask` and `Link` and the 1×14 vertical hairline were all deleted along the way —
the tree is intentionally flat for handoff.

**Rhythm:** 24.5 above / 26 below. Reviews block stays at y=950 — the 66px block still fits the
116.5px gap without moving anything.

**Accent:** `#C81E1E` border + label on white = 5.74:1 ✓ AA. Still the only red *outline* on the
page, so it carries accent without joining the three filled `#FB3D37` "Choose …" CTAs.

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
- [x] ~~Decide the band~~ → **B, refined** (see above).
- [ ] **Fix the `Button` set: `Outline=True` variants use Poppins Medium, filled use SemiBold.** Every
      outline instance silently inherits the wrong weight. Pick one weight for the whole set.
- [ ] Apply `Price Objection — B` (436:12872) to the real frame 434:7727 and delete the three option clones + section 435:12841.
- [ ] Add a **phone glyph** component — none exists, so the call CTA is text-only.
- [ ] Fix the filled-red AA failure → `#E02424`.
- [ ] Third tier card is 317 vs 297 — confirm intentional.
- [ ] Reconcile `#FB3D37` against the Flowbite red ramp, or document it as a brand override.

Back to [[Hub]].
