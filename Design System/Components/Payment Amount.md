# Payment Amount

Boxed payment breakdown — title ("Payment Amount:") with itemised method/amount pairs (USHIP $5.00 / Venmo $75.00 / …). Used in invoices, deposit slips, and payment confirmations to show how a total breaks down across payment methods.

- **Component node:** `389:862`
- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit?node-id=389-862)
- **Figma section:** `----- Card` → "Payment Amount"
- **Figma documentation:** Section `1742:7264` "Payment Amount — Documentation" on the same page

---

## Composition

Vertical stack: title row + divider + breakdown rows.

| Layer | Bindings |
|---|---|
| Container (FRAME) | fill `Background/Tretiary` (legacy — see note) · stroke `Border/Primary` |
| Title (TEXT, "Payment Amount:") | `Text/Body/*` (17pt) · `Text/Primary` |
| Divider (Line) | `Width/XS` · `Border/Primary` |
| Method label (TEXT, "USHIP", "Venmo") | `Form/Label/*` (15pt) · `Text/Secondary` |
| Method amount (TEXT, "$5.00", "$75.00") | `Form/Input/*` (17pt) · `Text/Primary` |

329 × 201 default dimensions.

**Note:** Container fill is still bound to the legacy `Background/Tretiary` semantic token (a known typo / deprecated token in `Colors: Semantic`). Kept by decision — fix-out is tracked as a follow-up at the system level.

---

## Variants
main
None — single component.

---

## Instance properties

None — content is overridden directly on the inner text layers.

---

## Do

- ✅ Use Payment Amount when an invoice / deposit needs to show a per-method breakdown.
- ✅ Edit the method labels (USHIP, Venmo, etc.) to match the actual payment methods used.
- ✅ Place inside a [[Card]] or details panel — Payment Amount has its own bordered surface and doesn't need to nest inside [[Card Base]].

## Don't

- ❌ Don't use Payment Amount for a single total — use [[View]] instead.
- ❌ Don't override the divider styling — the `Width/XS` × `Border/Primary` line is system-standard.
- ❌ Don't fill in method labels that aren't real payment methods in this app's payment flow.

---

Back to [[Design System]] · [[Component Status]].
