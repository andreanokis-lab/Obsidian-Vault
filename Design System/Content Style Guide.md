# Content Style Guide

How HaulEx writes — for every label, button, error, empty state, toast, and confirmation across the Driver App. The visual system tells the user *what* they're looking at; the words tell them *what to do*. Both must be consistent.

This guide is the single source of truth. When a pattern doc and this guide disagree, fix the pattern doc.

For visual rules see [[Rules]]. For composition rules see [[Patterns]].

---

## 1 — Voice & tone

**Audience.** Working drivers. Time-pressured, often outdoors, sometimes one-handed, occasionally on a poor connection. Not browsing. Not entertaining themselves.

**Voice.** Calm, direct, useful. Three checks:
- ✅ Would a dispatcher say this to a driver on the radio? Then ship it.
- ❌ Is it chatty, clever, or apologetic? Cut it.
- ❌ Is it "delightful"? Drivers don't want delight — they want done.

**Tone by context.**

| Context | Tone | Example |
|---|---|---|
| Routine confirmation | Matter-of-fact | "Receipt saved." |
| Error | Honest + actionable | "Couldn't load trips. Check your connection." |
| Destructive confirm | Consequence-first | "This can't be undone." |
| Empty state — no data | Patient + informative | "Your trips will appear here." |
| Empty state — no results | Direct + recoverable | "No companies found. Try clearing your filters." |
| Loading | Specific or silent | "Uploading 1 of 3 photos…" or nothing at all |

---

## 2 — Grammar & mechanics

| Rule | Do | Don't |
|---|---|---|
| Case | Sentence case for labels, buttons, headings | `Save Receipt` (title case) · `SAVE RECEIPT` (all caps) |
| Exclamation marks | Never | "Saved!" · "Oops!" · "Uh oh!" |
| Voice | Active | "Tap Retry" not "Retry can be tapped" |
| Person | Second person or imperative | "Your trips" · "Add a photo" — never "We will…" |
| Numbers | Digits | "1 photo" not "one photo" |
| Acronyms | Always uppercase | VIN, BOL, COP, COD, ETA, GPS |
| Truncation | Ellipsis character `…` | three dots `...` |
| Contractions | OK in body, avoid in errors | "We're loading" · in errors: "We are unable to" feels off — rewrite the sentence to avoid the contraction/expansion choice |
| Oxford comma | Use it | "Pickup, delivery, and notes" not "Pickup, delivery and notes" |

**Sentence fragments** are fine for labels, buttons, captions. **Full sentences with periods** for messages and helpers. **No periods on single-line labels.**

---

## 3 — Button labels

| Rule | Detail |
|---|---|
| Length | 1–3 words. Prefer 1–2. |
| Form | Verb (action) — "Save", "Add", "Continue", "Delete" |
| Sentence case | "Save changes" not "Save Changes" |
| Destructive | Use the destructive verb itself — "Delete", "Sign out", "Remove". Never "Confirm" (see [[Sheet Pattern]] · Stack Button Sheet) |
| Multi-step "next" | "Continue" until the final step; the final step is the actual action |
| Cancel vs Close vs Done | Cancel = abandons unsaved changes · Close = dismisses without state · Done = commits the change |
| Disabled state | Same label — disable visually, don't rename to "Please fill the form" |

**Final-step naming.** In a multi-step flow, only the last screen's button is the actual action. Everything before says "Continue".

| Step | Button |
|---|---|
| Vehicle Details (1 of 4) | Continue |
| Pickup & Delivery (2 of 4) | Continue |
| Service & Notes (3 of 4) | Continue |
| Review & Confirm (4 of 4) | **Confirm order** |

**Cancel placement.** In destructive confirmations, Cancel is **below** the destructive button — secondary position. This is the standard, not a preference.

---

## 4 — Form labels, placeholders, helpers

| Element | Rule | Example |
|---|---|---|
| Label | Descriptive noun phrase, sentence case | "Vehicle make" · "Contact phone" |
| Required | Trailing ` *` in the label | "Email *" |
| Optional | Trailing ` (optional)` in the label | "Notes (optional)" |
| Placeholder | An **example**, not an instruction | "e.g., Porsche" · "17-character VIN" — not "Enter make" |
| Helper (default) | What's expected or what happens | "We'll send a code to this number." |
| Helper (error) | What went wrong + how to fix | "Enter a 17-character VIN." |

**Never** rely on placeholder for the field's meaning — placeholders disappear on typing. Always show the label.

**Required vs optional** must always be unambiguous. If most fields are optional, mark required; if most are required, mark optional. Don't leave it implicit.

Cross-reference: [[Form Pattern]] for the composition rules.

---

## 5 — Error messages

Every error needs **what went wrong** + **what to do**.

| Type | Length | Example |
|---|---|---|
| Inline field error (Input Helper) | ≤ 60 chars, one sentence | "Enter a valid email." |
| Inline section error | Headline ≤ 40 chars + body ≤ 140 chars | "Couldn't save receipt." + "Check your connection and try again." |
| Full-screen error | Same as inline section, centred | "Couldn't load trips." + "Check your connection and try again." |
| Toast (non-blocking) | ≤ 60 chars | "Photo upload failed. Tap to retry." |

**Phrasing rules.**

- ✅ "Enter a 17-character VIN." (active, imperative)
- ❌ "VIN format invalid." (passive, jargon)
- ❌ "You entered an invalid VIN." (blames the user)

**Banned phrases.**

- "Something went wrong" without context
- "Oops"
- "Sorry"
- Any sentence ending in `!`

When the cause is unknown, still be specific about the surface — "Couldn't load trips" not "Something went wrong".

Cross-reference: [[Error State Pattern]].

---

## 6 — Empty state copy

Three flavours, three patterns. Don't mix them up.

| Flavour | Headline formula | Body formula | CTA |
|---|---|---|---|
| **No data yet** | "No [things] yet" | What will appear here or what the user can do | Optional ("Create", "Add", "Invite") |
| **No results — search** | "No [things] found" | "Try adjusting your search or clearing your filters." | "Clear search" |
| **No results — filters** | "No [things] found" | "Try adjusting your filters." | "Clear filters" |

**Examples — from the Driver App.**

| Screen | Type | Copy |
|---|---|---|
| Notifications Placeholder | No data yet | "No notifications yet" · "We'll let you know when something changes." |
| Notes Placeholder | No data yet | "No notes yet" · "Tap + to add a note about a Trip or Vehicle." |
| Leaderboard Placeholder | No data yet | "No standings yet" · "Standings appear after your first completed Trip." |
| No Contact Found | No results — search | "No companies found" · "Try adjusting your search or clearing your filters." · **Clear filters** |

**Never** use "no data yet" copy for "no results" — they're different situations.

Cross-reference: [[Empty State Pattern]] · [[Filter Search Results Pattern]].

---

## 7 — Notification & toast copy

| Situation | Tense | Example |
|---|---|---|
| Confirmation (action completed) | Past | "Receipt saved" · "Photo uploaded" · "Trip completed" |
| In progress | Present continuous | "Uploading photo…" · "Loading trips…" |
| Specific progress | Counted | "Uploading 1 of 3 photos…" |
| Failure with recovery | Past + action | "Photo upload failed. Tap to retry." |

**Length.** Toast text ≤ 60 chars, fits one line at 375pt.

**Timing.**

| Toast type | Auto-dismiss |
|---|---|
| Confirmation (success) | 3s |
| Confirmation with action ("Undo") | 5s |
| Error without action | 4s |
| Error **with** action (Retry) | **Never auto-dismiss** — user must read it |

**Specific beats generic.** "Photo uploaded" not "Success". "Couldn't save receipt" not "Error".

---

## 8 — Destructive confirmations

Use the Stack Button Sheet for any irreversible action (see [[Sheet Pattern]]).

| Slot | Rule | Example |
|---|---|---|
| Title | What's about to happen, as a question | "Delete this receipt?" · "Sign out of HaulEx?" · "Cancel this trip?" |
| Body | The consequence | "This can't be undone." · "You'll need to sign in again to access your trips." |
| Primary button | The destructive verb itself | "Delete" · "Sign out" · "Cancel trip" |
| Secondary button | "Cancel" — always present, below the destructive button | "Cancel" |

**Never:**

- Use "Confirm" as the destructive button — it's vague and disables muscle memory
- Stack two destructive actions in one sheet — pick one
- Show a destructive confirmation for reversible, low-stakes actions — just do it

---

## 9 — Loading & progress copy

| Wait time | What to show |
|---|---|
| < 250ms | Nothing (the flicker is worse than the wait — iOS HIG) |
| < 1s | Spinner only |
| 1–3s | Spinner + "Loading…" caption |
| > 3s, known total | Specific progress — "Uploading 1 of 3 photos…" |
| > 3s, unknown total | Spinner + specific surface — "Loading trips…" |

**Don't add anxiety.** Never:

- "Don't close this app"
- "Please wait"
- "This may take a while"
- "Almost there!"

The spinner is the signal that work is happening. Words should help locate the user, not warn them.

Cross-reference: [[Loading Skeleton Pattern]].

---

## 10 — Dates, times, units, formats

| Element | Format | Example |
|---|---|---|
| Date — long form | Month abbrev. + day + year | "May 22, 2026" |
| Date — relative (within ±1 day) | Word | "Today" · "Yesterday" · "Tomorrow" |
| Date — within current week | Day of week | "Monday" · "Friday" |
| Time | 12-hour, lowercase am/pm, no period | "2:30 pm" · "8:00 am" |
| Time range | En dash with spaces | "10:00 am – 12:00 pm" |
| Distance | Miles, full word in body | "12 miles" · `mi` only in tight columns |
| Weight | Pounds | "3,500 lbs" |
| Currency | `$` prefix, two decimals always | "$1,250.00" · "$12.50" |
| Phone | US parens + dashes | "(555) 123-4567" |
| Plurals | Zero is plural | "0 photos" · "1 photo" · "2 photos" |

**Currency rule.** Always two decimals on receipt and invoice amounts — even whole dollars ("$50.00" not "$50"). This avoids "is that the total?" ambiguity.

**Relative dates.** Use within ±1 day only. After that, full date — drivers run multi-day trips and "3 days ago" is harder to verify than "May 19".

---

## 11 — Glossary (HaulEx domain terminology)

Canonical terms. If a screen uses a different word for the same thing, fix the screen.

### Acronyms — always uppercase

| Term | Meaning |
|---|---|
| **BOL** | Bill of Lading. The document inspected at pickup and delivery. |
| **VIN** | Vehicle Identification Number. 17 characters. |
| **COP** | Cash on Pickup. Receipt type. |
| **COD** | Cash on Delivery. Receipt type. |
| **ETA** | Estimated Time of Arrival. |
| **GPS** | Global Positioning System. |
| **INOP** | Inoperable. Vehicle condition flag. |

### One-word vs two-word — easy to get wrong

| Term | Use as |
|---|---|
| **Pickup** (noun) | "Pickup at 2:30 pm" |
| **Pick up** (verb) | "Pick up the vehicle at the lot" |
| **Drop-off** (noun, hyphenated) | "Drop-off complete" |
| **Drop off** (verb) | "Drop off at the customer's home" |
| **Sign-out** (noun) | "Sign-out time: 6:00 pm" |
| **Sign out** (verb) | "Sign out of HaulEx" — never "Log out" |
| **Sign-in** (noun) / **Sign in** (verb) | Same rule as sign-out |

### Domain nouns

| Term | Definition | Capitalize? |
|---|---|---|
| **Trip** | A complete assignment from origin to destination, potentially multi-stop | Capitalize when referring to a specific Trip entity ("Your Trip is ready"); lowercase as a generic noun ("3 trips left this week") |
| **Stop** | An individual pickup or delivery location within a Trip | Same rule as Trip |
| **Route** | An ordered sequence of Stops forming a Trip | Same rule |
| **Order** | A customer's request that becomes a Trip | Same rule |
| **Adjustment** | A correction to a receipt or BOL | Lowercase as generic noun, capitalize as receipt type |

### Vehicle types — canonical list

Use these exact strings in pickers and labels:

- Sedan
- SUV
- Truck
- Motorcycle
- Van
- RV (always uppercase)

If a needed type isn't in this list, add it here first, then to the picker.

### Receipt types — canonical list

- COP
- COD
- Adjustment

### Brand

**HaulEx** — always one word, capital H and capital E. Never "Haulex", "HAULEX", "haul ex", "HaulEX".

---

## 12 — Accessibility copy

### VoiceOver labels for icon-only elements

Every icon button needs an `accessibilityLabel`. Format: **imperative verb + object**.

| Icon button | accessibilityLabel |
|---|---|
| Camera shutter | "Take photo" |
| Camera flash toggle | "Toggle flash" |
| Camera switch | "Switch camera" |
| Close (✕) | "Close" |
| Back chevron | "Back" |
| Delete (trash icon) | "Delete receipt" (specific to context) |
| Add (+ icon) | "Add photo" (specific to context) |

Generic labels like "Button" or "Icon" are wrong. Always specific to the context.

### Image alt text

Describe the content, never start with "Image of…" or "Picture of…".

- ✅ "Driver signature"
- ✅ "BOL page 1 of 3"
- ❌ "Image of driver signature"

### Hint vs label

- **Label** = what it is. "Add photo"
- **Hint** = what happens. "Opens the camera"

iOS reads the hint **after a delay**. Don't put critical info in the hint.

Cross-reference: [[Rules]] A1–A5.

---

## 13 — Permission prompts (iOS)

### Pre-prompt before the OS prompt

iOS shows the system permission alert exactly once per permission per install. Don't burn it.

**Always show your own copy first** explaining *why* you need the permission, then trigger the OS prompt only after the user consents to your screen.

| Permission | Pre-prompt copy |
|---|---|
| Camera | "HaulEx needs your camera to capture receipts and BOL inspections." |
| Photo library | "Choose existing photos for receipts or vehicle damage records." |
| Location | "We use your location to assign Trips near you and track Stops." |
| Notifications | "Get notified when a new Trip is assigned or a Stop is updated." |

### If denied

Don't trap the user. Show inline copy + a button that opens Settings, not a generic error toast.

- ✅ "Camera access is off. Turn it on in Settings to capture receipts." **[ Open Settings ]**
- ❌ "Permission denied."

### Never

- Beg ("We promise we won't…")
- Add anxiety ("Without this, the app won't work")
- Show the OS prompt on app launch — wait for the first feature attempt

---

## How to use this guide

- Writing new copy for a screen — read sections 1–9 before opening Figma.
- Adding a new domain noun — add it to the Glossary (section 11) **before** using it in a design.
- Reviewing a screen for handoff — run the QA checklist below.

### Content QA checklist

- [ ] Voice matches section 1 (calm, direct, useful — no chatty, no apologetic)
- [ ] All labels are sentence case
- [ ] No exclamation marks anywhere
- [ ] Every error has *what went wrong* + *what to do*
- [ ] Required fields marked `*`; optional marked `(optional)`
- [ ] Destructive button uses the destructive verb (never "Confirm")
- [ ] Empty state distinguishes "no data yet" from "no results"
- [ ] Toast copy ≤ 60 chars
- [ ] Dates / times / units follow section 10 formats
- [ ] Domain terms match the Glossary (section 11)
- [ ] Icon-only buttons have `accessibilityLabel` annotations

---

Back to [[Design System]] · [[Rules]] · [[Patterns]] · [[Hub]].
