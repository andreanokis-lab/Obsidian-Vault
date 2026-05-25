---
status: in-progress
type: screen-spec
figma_node: "777:20871"
figma_file: yhxCSzJrafZbqXGZOCBCKE
---

# Orders List

Vertical list of Order cards inside Section 1 on Page 5 of the Driver App file. Built 2026-05-25 as a demo / sandbox for the Orders list pattern.

**Figma:** https://www.figma.com/design/yhxCSzJrafZbqXGZOCBCKE/HaulEx-Driver-App?node-id=762-20797

## Composition

| Layer | Component / Token |
|---|---|
| List container | Vertical auto-layout frame, 361 wide, FIXED width, AUTO height |
| Item spacing | `Space/L` (16) — bound via `setBoundVariable("itemSpacing", …)` |
| Padding | 16 top, 16 bottom, 0 horizontal |
| Card row | Detached clones of [[Card]] component set `Role=Orders` variant |
| Card key | `5777f6f74ed505ce262f7030dda861e3c8edb2a8` |

## Cards rendered

| # | Vehicle | Trip # | Badges |
|---|---|---|---|
| 1 | 2015 Porsche Cayenne | #10421 | ENCL |
| 2 | 2022 Tesla Model Y | #10422 | EXP |
| 3 | 2019 BMW X5 | #10423 | ENCL · EXP |
| 4 | 2024 Ford F-150 | #10424 | ENCL |
| 5 | 2020 Audi Q7 | #10425 | EXP |

Slots 2/3 (route Origin → Destination, pickup/delivery dates, $ amount) inherit defaults from the Card variant — they were not customized per row in this sandbox build.

## Known gap — SF Pro Text not available locally

The DS Card uses **SF Pro Text Regular** in several text nodes. That family is not installed on the build host (only `SF Pro` is). As a result, fresh `createInstance()` + `appendChild` failed with `unloaded font "SF Pro Text Regular"`.

Workaround used:

1. `clone()` an existing reference Order Item on the DS page (cloning doesn't validate fonts).
2. `detachInstance()` the clone to release it from the component property system.
3. `setRangeFontName(0, len, { family: "SF Pro", style: "Regular" })` on every TEXT node — this requires the *new* font loaded, not the old.
4. `appendChild` into the target list — now passes font validation.

**Consequence:** the resulting cards are detached frames, not live Card instances. They will not pick up updates when the [[Card]] component changes. If we need live instances, the host system must install SF Pro Text, or the Card text styles must be rebound to a family that ships locally (SF Pro).

## Follow-ups

- Decide whether to keep this as a sandbox or promote to a real Orders screen variant under the `ORDERS` section.
- File a font issue: either install SF Pro Text on the build environment, or migrate the Card's bound text styles from `SF Pro Text` to `SF Pro` so future use_figma sessions can use live instances.
- If kept, customize Slot/Slot 2/Slot 3 per row (route addresses, dates, payment amount) so the cards aren't identical except for vehicle + trip#.

Back to [[Driver App]] · [[Design System]].
