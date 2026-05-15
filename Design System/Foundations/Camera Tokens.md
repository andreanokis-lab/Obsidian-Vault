# Camera Tokens

5 semantic color tokens in the `Colors: Semantic` collection, prefixed `Camera/`. All tokens are **static across both Light and Dark modes** — the camera UI is always-dark regardless of system appearance.

- **Figma file:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **Collection:** `Colors: Semantic`
- **Modes:** Light + Dark (values identical)
- **Total tokens:** 5
- **Where used:** Camera screens and components — section `1182:544` "----- Camera" in UIKit.

These tokens live in `Colors: Semantic` rather than a separate Camera collection because they're consumed by [[Colors - Semantic|Colors: Semantic]] consumers (Background, Icon, etc.) — keeping them in the same collection simplifies binding.

---

## Token spec

| Token | Hex | Alpha | Primitive ref |
|---|---|---|---|
| `Camera/Overlay` | `#000000` | 0.5 | [[Colors - Primitives#neutral|neutral/black-50]] |
| `Camera/Controls Background` | `#0D0D0D` | 1.0 | neutral/950 |
| `Camera/Surface` | `#1A1A1A` | 1.0 | neutral/900 |
| `Camera/Icon Primary` | `#FFFFFF` | 1.0 | neutral/0 |
| `Camera/Icon Secondary` | `#808080` | 1.0 | neutral/500 |

---

## When to use

| Token | Use for |
|---|---|
| `Camera/Overlay` | Dim layer behind camera UI controls — 50% black scrim over the camera viewfinder to lift contrast on overlay icons |
| `Camera/Controls Background` | Background fill for camera control containers — bottom bar, top bar, capture area surround |
| `Camera/Surface` | Card / panel surface inside camera UI — capture mode pill, settings sheet on camera, photo preview thumbnail background |
| `Camera/Icon Primary` | All primary camera icons — shutter, flash, switch camera, close. Always white because the surface is always dark |
| `Camera/Icon Secondary` | De-emphasised camera icons — disabled controls, secondary actions inside camera surfaces, decorative glyphs |

---

## Don't

- ❌ Do not use `Camera/*` tokens outside the camera screens — they bypass Dark/Light mode and will look wrong on normal app surfaces. Use `Background/Inverse Static` and `Icon/Inverse Static` elsewhere if you need always-dark behaviour.
- ❌ Do not bind a `Camera/*` token to a mode-aware surface — that defeats their purpose. Camera UI is intentionally locked to dark.
- ❌ Do not use `Camera/Icon Primary` (white) on a non-camera dark surface — use `Icon/Inverse Static` instead so the rest of the system stays consistent.
- ❌ Do not introduce new `Camera/*` tokens for one-off camera variants. Compose with existing tokens or extend the primitive layer first.

---

## Why these are static

Camera UI on iOS is universally dark regardless of system appearance — Apple's own Camera, FaceTime, and most third-party camera apps lock to dark. Reasons:

1. **Contrast over viewfinder.** Light camera UI loses against a bright outdoor scene.
2. **Glare avoidance.** A bright UI in low-light shooting creates lens flare and dilates the pupil.
3. **Battery / OLED.** Dark camera UI on OLED displays reduces draw.

The 5 `Camera/*` tokens encode that "always-dark" decision once. Components binding to them inherit the behaviour without needing per-screen mode overrides.

---

Back to [[Design System]] · [[Colors - Semantic]] · [[Components - In Progress]].
