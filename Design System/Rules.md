# Rules — What Every Designer Must Know

These rules apply to every screen, every component, every state. They are not suggestions.

---

## T — Token Rules

**T1. Use semantic tokens only — never primitives.**
`Text/Primary` ✅ · `neutral/950` ❌
Primitives are the raw scale. Semantics are the interface. Using a primitive breaks Dark mode and makes future re-theming impossible.

**T2. Apply typography via Figma text styles — never set size/weight manually.**
Open the text style panel → `Semantic/IOS/…`. If the style you need doesn't exist, flag it — don't invent a custom size.

**T3. Use spacing tokens for all padding, gaps, and margins.**
No arbitrary px values. Every padding and gap must map to a `Space/` token. See [[Spacing]] for the full scale and what each value is for.

**T4. Use border tokens for radius and stroke width.**
`Radius/L` for cards and sheets. `Radius/M` for inputs. `Radius/Pill` for pill buttons. `Width/XS` for dividers. See [[Border]].

**T5. Never hardcode a hex value.**
If a semantic token doesn't exist for your use case, open a token request — document it in [[Component Status]] or the relevant component note.

---

## M — Mode Rules

**M1. Design every screen in both Light and Dark mode.**
Use Figma variable modes. Both variants must be complete before the screen is considered done.

**M2. When placing a semantic color, confirm you're in the right mode.**
Assigning `Background/Primary` in a Dark-mode frame should resolve to `neutral/950`. Verify in the variable inspector.

**M3. Use `Inverse Static` and `Primary Inverse Static` tokens only for elements that are intentionally always on a dark surface.**
Example: a white label on a colored button that doesn't flip in Dark mode. If you're unsure, use the regular `Inverse` variant (which flips) instead.

---

## L — Layout Rules

**L1. Minimum touch target is 44×44pt for every interactive element.**
Visual size can be smaller (a 24pt icon is fine) but the hit area must be padded to 44pt. No exceptions. This is a HIG requirement that affects ~25% of tap accuracy.

**L2. Screen horizontal margin is always `Space/L` (16pt).**
Content hugging the screen edge is a P0 bug. The one exception is full-bleed images and video.

**L3. Design for 375pt width minimum.**
iPhone SE / mini. Test your layout by resizing the frame to 375. If it breaks, fix it before moving on.

**L4. Respect safe areas.**
- Top: 59pt (Dynamic Island devices), 47pt (notch), 20pt (SE)
- Bottom: 34pt (home indicator), 0pt (SE)
Never place interactive elements behind the Dynamic Island or home indicator.

**L5. Primary actions belong in the lower third of the screen.**
One-handed reachability. Put your most important CTA where a thumb can reach it without repositioning the phone.

---

## C — Component Rules

**C1. Use library components — don't recreate from scratch.**
Check [[Component Status]] before drawing anything. If the component exists in Figma, use it. Override properties via the instance panel, not by detaching.

**C2. Do not detach component instances to make small visual tweaks.**
If you need a variant that doesn't exist, either add it to the component set or document the gap. Detached instances drift and cause inconsistencies.

**C3. When a needed component doesn't exist, file it.**
Add a row to [[Component Status]] with status `Planned` and describe what you need. Don't build ad-hoc — schedule it.

**C4. Camera components are in progress — use the specs in [[Components - In Progress]].**
Do not reassemble camera screens until the component build plan (ShutterButton → CameraBottomBar pipeline) is complete.

---

## A — Accessibility Rules

**A1. Never use color as the only conveyor of meaning.**
Error state? Use `Text/Negative` color AND an error icon AND a label. A colorblind user must understand the state without seeing color.

**A2. Minimum contrast ratios.**
- Normal text (< 18pt or < 14pt Bold): **4.5:1**
- Large text (≥ 18pt or ≥ 14pt Bold): **3:1**
Use a contrast checker on any custom color combination before shipping.

**A3. Use SF Symbols for all icons.**
SF Symbols scale with Dynamic Type automatically. Custom SVG icons do not. If a custom icon is required, provide `@1x @2x @3x` assets.

**A4. All text must support Dynamic Type.**
Apply semantic text styles (they scale). Never pin a fixed pt size. Test at XS, Default (L), XXL, and AX1 sizes.

**A5. Every interactive element needs a VoiceOver label.**
In your design annotation, specify `accessibilityLabel` text for any element that doesn't have visible text (icon buttons, image thumbnails, status indicators).

---

## QA Checklist (before handing off any screen)

- [ ] All tokens are semantic (no raw hex, no primitive color, no arbitrary px spacing)
- [ ] Light mode reviewed ✓
- [ ] Dark mode reviewed ✓
- [ ] Layout tested at 375pt width ✓
- [ ] All interactive elements ≥ 44×44pt ✓
- [ ] Safe areas respected ✓
- [ ] Typography uses Semantic/IOS styles only ✓
- [ ] Color contrast ≥ 4.5:1 for normal text ✓
- [ ] Dynamic Type tested (XS → AX1) ✓
- [ ] VoiceOver labels annotated ✓
- [ ] No detached component instances ✓

---

Back to [[Design System]] · [[Getting Started]].
