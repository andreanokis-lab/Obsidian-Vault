# HaulEx UIKit — Design System

The canonical token & component reference for the HaulEx UIKit Figma library.

- **File:** [HaulEx UIKit](https://www.figma.com/design/3qOFF7kHsaZPfdftDb1CVz/HaulEx-UIKit)
- **File Key:** `3qOFF7kHsaZPfdftDb1CVz`
- **Owner:** Andrew Nabok
- **Last synced:** 2026-05-26

---

## Core principle

**Primitive → Semantic.** Designs reference *semantic* tokens only. Primitives feed semantics.

| Layer | Has modes? |
|---|---|
| Spacing | Single mode |
| Border | Single mode |
| Colors / Primitive | Single mode |
| Colors / Semantic | **Light + Dark** |
| Typography / Primitive | Single mode |
| Typography / Semantic | **iOS** mode only |

Read [[Architecture]] for the full philosophy and [[Rules]] for what's enforced.

---

## Foundations

The token layer — values everything else composes from.

| Note | Purpose |
|---|---|
| [[Foundations/Spacing\|Spacing]] | 18 tokens, 0–112pt |
| [[Foundations/Border\|Border]] | Radius (XS–Pill, Circle) + width (XS–XL) |
| [[Foundations/Colors - Primitives\|Colors – Primitives]] | Raw scales — Red / Green / Blue / Yellow / Neutral (58 tokens). Do not use directly. |
| [[Foundations/Colors - Semantic\|Colors – Semantic]] | Light + Dark role tokens (Text, Background, Border, Icon) |
| [[Foundations/Camera Tokens\|Camera Tokens]] | 5 always-dark tokens for camera UI |
| [[Foundations/Typography - Primitives\|Typography – Primitives]] | SF Pro size & line-height ramp. Do not use directly. |
| [[Foundations/Typography - Semantic\|Typography – Semantic]] | iOS roles (Screen, Section, List, Form, Meta…) |
| [[Foundations/Text Styles\|Text Styles]] | Published Figma text styles + node IDs |

---

## Components

Built components in the UIKit library. Status overview: [[Component Status]].

| Component | Note |
|---|---|
| [[Components/Avatar\|Avatar]] | Circular avatar, rank ring + badge |
| [[Components/Badge\|Badge]] | 47 variants (Type × Role × Accent) |
| [[Components/Vertical Badge\|Vertical Badge]] | Pickup / delivery stop markers |
| [[Components/Button\|Button]] | 143 variants (Size × Type × State × Icon × Role) |
| [[Components/Input\|Input]] | 7 state variants |
| [[Components/Text Area\|Text Area]] | 5 state variants |
| [[Components/Draw Area\|Draw Area]] | Signature / freehand capture, S + M |
| [[Components/Divider\|Divider]] | Horizontal + vertical hairline |
| [[Components/Tooltip\|Tooltip]] | 4 directional + info popover |
| [[Components/Navigation Bar\|Navigation Bar]] | 6 Type variants — Default, Search, Order Label, Settings, Stack, Horizontal |
| [[Components/Tab Bar\|Tab Bar]] | iOS bottom tab bar, 3 Selected variants |
| [[Components/Sidebar\|Sidebar]] | Right-edge slide-in drawer with scrim |
| [[Components/Toast\|Toast]] | 4 Message variants — Success, Error, Warning, Info |
| [[Components/Components - In Progress\|In Progress]] | Camera component build plan |

---

## Patterns

Compositional guidance — how components combine into common UI. Full index: [[Patterns/Patterns|Patterns]].

**Generic:**
- [[Patterns/Form Pattern|Form Pattern]] — multi-field data entry
- [[Patterns/List with Actions Pattern|List with Actions Pattern]] — rows with trailing controls
- [[Patterns/Empty State Pattern|Empty State Pattern]] — no data / no results
- [[Patterns/Error State Pattern|Error State Pattern]] — inline / modal / full-screen by recovery path
- [[Patterns/Loading Skeleton Pattern|Loading Skeleton Pattern]] — native spinner + Titles `Place=Skeleton`
- [[Patterns/Section Header Pattern|Section Header Pattern]] — plain / + action / Action Section

**HaulEx-specific:**
- [[Patterns/Camera Capture Flow|Camera Capture Flow]] — end-to-end photo capture
- [[Patterns/Take Photo Screen Pattern|Take Photo Screen Pattern]] — static camera layout
- [[Patterns/Photo Viewer Pattern|Photo Viewer Pattern]] — native iOS 18 viewer for attached/captured photos (portrait + landscape)
- [[Patterns/Leaderboard Pattern|Leaderboard Pattern]] — Olympic podium + rank list
- [[Patterns/Sheet Pattern|Sheet Pattern]] — Half / Full / Stack Button / Action Sheet
- [[Patterns/Filter Search Results Pattern|Filter Search Results Pattern]] — search bar + chips with empty state
- [[Patterns/Navigation Patterns|Navigation Patterns]] — Navigation Stack vs Tab Bar (legacy combined note)

Pattern → real screen mapping: [[Patterns/_Pattern Evidence Map|Pattern Evidence Map]].

---

## Rules & reference

- [[Rules]] — non-negotiable visual rules. Read before building.
- [[Content Style Guide]] — voice, tone, labels, errors, copy formats, HaulEx glossary.
- [[Architecture]] — token philosophy, naming, mode rules.
- [[Component Status]] — full inventory: built / in progress / planned.
- [[Getting Started]] — onboarding for new designers.
