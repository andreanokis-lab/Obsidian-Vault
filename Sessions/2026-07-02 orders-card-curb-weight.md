---
date: 2026-07-02
type: session
area: Design System / Card
---

# Orders card — curb weight

Added **curb weight** to the `Card` component, `Role=Orders` variant, in the HaulEx UIKit (`3qOFF7kHsaZPfdftDb1CVz`).

## What changed
- **Placement:** centered between the pickup (P) and delivery (D) clusters in the P/D row (`362:1054`, `SPACE_BETWEEN`). Reads *pickup date · curb weight · delivery date*.
- **Build:** cloned the pickup cluster (`362:1044`) to inherit exact typography/color variable bindings → new group `2001:3637`; swapped `Icons/p-square` → `Icons/scalemass` (Size=sm, `199:609`); set value `4,398 lb`.
- **Properties added on the set (`389:2319`):**
  - `Curb Weight` TEXT (default "4,398 lb") → bound to the value text `characters`.
  - `Show Weight` BOOLEAN (default true) → bound to the weight group `visible`.

## Why centered-in-P/D-row
Roomiest spot on the card (the P/D row is two clusters with a wide empty middle); keeps the vehicle title and the order#/amount row clean. Semantically weight is a vehicle attribute, not a stop — the `scalemass` icon disambiguates. (User picked this over the bottom-row/`#00000` option.)

## Propagation — OPEN
Driver App (`yhxCSzJrafZbqXGZOCBCKE`) Order cards are **remote library instances** (`remote: true`) of this component, spread across screens (e.g. "Trips" `1:28891`) — there is **no separate detached "Orders List" screen** to hand-edit (the old `782:20481` node no longer resolves). They will only receive curb weight after the **UIKit library is republished and the Driver App accepts the update** — not yet done (publish is a shared action, awaiting user go-ahead). Each card then supplies its own weight via the `Curb Weight` prop, or hides it via `Show Weight`.

Related: [[Card]] · [[Orders List]]
