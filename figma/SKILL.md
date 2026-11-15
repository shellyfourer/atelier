---
name: figma
description: >-
  Builds the complete Figma design file — variables, component library, and
  assembled pages at all three breakpoints — from a signed-off brand-tokens.json.
  This is GENERATE.md Step 5. Use after the brandbook skill has produced a signed-off
  brand-tokens.json. Never invoked before sign-off; refuses to build on a draft token file.
  Output: a Figma file with variable collections, a bound component library, and
  desktop / tablet / mobile frames for every page type in the brief.
---

# figma

Realizes the signed-off design system in Figma — **bottom-up, bound to tokens at every node,
never hardcoded values.** This skill is GENERATE.md Step 5. The brand book is the contract;
this skill is the execution. Everything it creates traces directly to `brand-tokens.json`.

## The dependency contract (enforced before build begins)

```
brand-tokens.json  → signedOff.status MUST be "signed-off"
      │
      ▼
  Figma variables     ← this skill mints these first
      │
      ▼
  Components          ← bind to semantic variables only
      │
      ▼
  Pages (all 3 BPs)   ← instantiate components; apply container contract
```

**Gate: if `signedOff.status` is not `"signed-off"`, halt immediately and return the user to
the brandbook skill.** A draft token file means the brand is not agreed — building on it means
reworking everything when the brand shifts. This is the same gate GENERATE.md enforces.

---

## The non-negotiable build order

```
0. CHECK SIGN-OFF  — refuse if brand-tokens.json is not signed-off
1. LOAD SKILLS     — mandatory figma-use pre-flight (see Step 1)
2. CREATE SESSION  — open or create the Figma file
3. VARIABLES FIRST — primitive collection → semantic collection (+ mode columns)
4. COMPONENTS      — atoms → molecules → organisms, all bound to semantic variables
5. PAGES           — desktop → tablet → mobile frames, section by section
6. VERIFY          — anti-slop checklist + traceability audit + bold-move naming
```

Steps 3 → 4 → 5 are strictly ordered. Never draw a page before its component exists; never
build a component before its semantic variable is published.

---

## Critical build rules (learned the hard way — read before any `use_figma` call)

These are not style preferences. Each one is a failure that shipped broken output on a real
first pass and had to be fully rebuilt. Violating any of them produces a design that looks like
collapsed, overlapping garbage or that cannot convert to code.

### R1 — EVERYTHING is auto-layout. Never absolute-position with guessed heights.

The single biggest failure mode. `textAutoResize = 'HEIGHT'` + `resize()` **does NOT recompute
the node's height inside the same `use_figma` call that created it** — the text node stays at
its placeholder ~10px, and everything you positioned below it (using that stale height) overlaps
into a pile. The first pass built heroes, cards, and headers with absolute `x/y` + hand-computed
`y += node.height` offsets; every text node read as 10px, so the whole page collapsed. Only the
Buttons survived — because they were the one thing built as pure auto-layout.

**The rule:** build every container with `figma.createAutoLayout()` (or `layoutMode` +
`primaryAxisSizingMode`). Append children, THEN set `layoutSizingHorizontal='FILL'` /
`layoutSizingVertical='HUG'`. Let Figma compute heights. **Never** read `.height` and restack
by hand. Absolute positioning is allowed ONLY for genuinely decorative overlapping art (e.g. a
concentric-ring motif) — never for layout, never for anything containing text.

This also makes the output convert cleanly to CSS flexbox. Absolute-positioned frames do not.

### R2 — HUG axis depends on layout direction. Don't cross the enums.

- `primaryAxisSizingMode` / `counterAxisSizingMode` take **`'FIXED' | 'AUTO'`** (set on the frame).
- `layoutSizingHorizontal` / `layoutSizingVertical` take **`'FIXED' | 'HUG' | 'FILL'`** (child-side).
- To hug height on a **VERTICAL** frame → `primaryAxisSizingMode = 'AUTO'`.
- To hug height on a **HORIZONTAL** frame → `counterAxisSizingMode = 'AUTO'` (height is the
  *counter* axis). Getting this backwards silently clamps the frame (e.g. a footer locked at
  96px while its content is 220px, clipping everything). This bit the tablet footer on pass two.
- After `combineAsVariants` or a `resize(w, 10)`, **re-assert the hug** (`primaryAxisSizingMode`),
  because those operations can reset it to FIXED and leave a 10px-tall component.

### R3 — Equal-height cards = FILL children on a FIXED-height row (CSS `align-items: stretch`).

`counterAxisAlignItems` has **no `'STRETCH'` value** in Figma (only MIN/MAX/CENTER/BASELINE).
To make a row of cards equal height: find the tallest card at natural HUG, set the row's
`counterAxisSizingMode='FIXED'` + `resize(row.width, tallest)`, then set every card's
`layoutSizingVertical='FILL'`. That is exactly `flex: 1; align-self: stretch` in code. The first
pass left cards at 463/431/431px because they only HUGged — a visible, flagged defect.

### R4 — Pages are Figma **Sections** wrapping a per-breakpoint page frame.

Each page = a `figma.createSection()` named for the page, containing `<Page> · Desktop`,
`<Page> · Tablet`, `<Page> · Mobile` frames side by side. The page frame is a VERTICAL
auto-layout of **component instances** (header, hero, …, footer) — never hand-drawn bands,
never inline-rebuilt chrome. The first pass built flat band frames directly on the canvas and
forgot the Footer as a component entirely.

### R5 — Chrome is components, placed as instances. Build the component, verify it in isolation, THEN assemble.

Header, Footer, Hero, Newsletter, Section-Header, Card are all components (one `Breakpoint`
variant set each). Pages place **instances** and `setProperties(...)` to fill text. **Read
`componentPropertyDefinitions` before building pages** so you use the real property IDs
(they are `Name#nn:n`, assigned by Figma — not guessable). Screenshot each component on its own
and confirm it renders before placing dozens of instances of a broken one.

### R6 — Real assets, no reconstruction, no emoji.

Upload the real logo via `upload_assets` (POST the bytes → get `imageHash` → use as an IMAGE
fill). Never rebuild a logo from text or shapes. The header logo lives on the **left**. Never
use emoji as iconography in UI. And never add a section the register doesn't want — a
trust/reviews strip on a personal blog is nonsense; cut it.

### R7 — Verify by screenshot, every page, before claiming done.

The first pass *claimed* the home page was clean while the section heading was clipped and the
cards were unequal — because it wasn't actually looked at. Screenshot every page (and the tricky
responsive frames) and read them. "I built it" is not "I verified it."

### R8 — IDs don't persist across calls; text styles need font loaded.

No JS reference survives between `use_figma` calls — pass node/variable IDs back as return
values and re-resolve them with `getNodeByIdAsync` / `getVariableByIdAsync`. Load every font
(`figma.loadFontAsync`) before writing text or applying a text style, and verify exact style
strings with `listAvailableFontsAsync` (`"SemiBold"` vs `"Semi Bold"` is a real footgun). If a
brand font isn't a Figma cloud font (e.g. Gambetta, a Fontshare face), pick the closest
available old-style serif as a documented stand-in and note it in the style description.

---

## Step 0 — Gate check

Before anything else, read `system/<project>/brand-tokens.json` and confirm:

```json
{ "signedOff": { "status": "signed-off" } }
```

If `status` is `"draft"` or `"in-review"`, **stop**. Tell the user the brand book has not been
signed off and return them to the brandbook skill. Do not proceed under any circumstance.

Also surface from the token file:
- `brand.register` — drives method choices throughout
- `colors.posture` — which color-system architecture to replicate in Figma variables
- `signatureMove.description` — the one bold move; must be nameable in the finished file

---

## Step 1 — Load skills (mandatory pre-flight)

**Load `figma-use` before any `use_figma` write call.** Skipping this causes silent failures.
When creating a new Figma file, load `figma-create-new-file` first. For assembled page pushes,
load `figma-generate-design` and `figma-generate-library`.

Call `create_session` with the target fileKey and a concise task description before any file
tool. If the fileKey is unknown or a placeholder (`undefined` / `null` / `{{…}}`), **halt and
ask the user for the correct key.** Never guess or reuse an unrelated key.

---

## Step 2 — Establish the Figma file

If no file exists for this project:
1. `create_new_file` — name it `<BrandName> Design System`
2. `create_session` with the returned fileKey

If a file already exists, `create_session` with the known key.

The Figma file will hold, in order:
- **Cover page** — project name, version, sign-off date from `brand-tokens.json`
- **Variables** — a documentation page; the actual collections live in Figma variables
- **Components** — pages grouped by function (Actions / Forms / Cards / Nav / Layout)
- **Pages** — one page per site page type (Home, PLP, PDP…)

---

## Step 3 — Variables first (the token spine in Figma)

**Open `method/01-color.md`, `method/02-typography.md`, `method/03-space-grid.md`.**

Figma variables mirror the `brand-tokens.json` two-tier spine exactly. Build in this order:

### 3a. Color — primitive collection

Name: `Primitives / Color`

Create one variable per entry in `brand-tokens.json → colors.roles`:
- Variable name: the color's `name` (e.g. `Ink`, `Cream`, `Forest`, `Gold`)
- Value: the hex from the token file
- Group by family if the posture is tonal-ramp (e.g. `Forest/100`, `Forest/200`…)

**Never expose primitives to UI directly.** Their only consumer is the semantic collection below.

### 3b. Color — semantic collection (UI binds here)

Name: `Semantic / Color`

One variable per entry in `colors.semanticRoles`:
- Variable name: the `token` (e.g. `text-primary`, `surface`, `accent`, `border`, `text-on-dark`)
- Value: alias to the matching primitive variable (never a raw hex)

**If the color posture is `thin-semantic` or `brand-dominant`** (`colors.posture`), add a mode
column per color mode (light / dark) in this collection. Semantic variables resolve to different
primitives per mode — never a `dark-` prefix on the name.

**Verify every semantic variable:** the contrast ratio from `semanticRoles[*].contrast` must be
documented in the variable description field (e.g. `"7.1:1 — AAA"`). A variable with no
contrast record is a documentation gap.

### 3c. Typography — composite token set

Name: `Semantic / Type`

For each role in `type.roles`, create a **text style** (Figma text style, not a variable):
- Style name: `<role>` (e.g. `Display`, `H1`, `Body`, `Caption`)
- Properties from the token file: face, weight, size, line-height, tracking
- Mobile variant: a second style `<role>/Mobile` using the `mobile` size/lineHeight from the token
- Description: the full composite spec (`Gambetta · 500 · 44/48 · −0.02em`)

Do not hardcode a single pixel. Every size/tracking value must come from `type.roles[*]`.

### 3d. Spacing / radius / elevation

Name: `Primitives / Space` and `Semantic / Space`

- **Spacing scale**: create a number variable per step from `space.scale` (e.g. `Space/4`, `Space/8`, `Space/16`…). Name by value at the primitive tier.
- **Radius**: one number variable per entry in `space.radius` (e.g. `Radius/sm`, `Radius/md`, `Radius/full`). The posture — size-keyed ramp vs single-knob — dictates how many steps exist.
- **Elevation**: one effect style per entry in `space.elevation` (e.g. `Elevation/0`, `Elevation/ambient`, `Elevation/contact`), using the shadow from the token file.

### 3e. Grid — per-breakpoint frame settings

Name: `Grid / Desktop`, `Grid / Tablet`, `Grid / Mobile`

For each entry in `grid.breakpoints`, record as a grid style:
- Columns: `breakpoint.columns`
- Gutter: `breakpoint.gutter`
- Margin: `breakpoint.margin`
- Container width: `breakpoint.container`

These become the layout grid applied to every page frame at the matching breakpoint.

**Checkpoint:** before proceeding to Step 4, every variable and style from the token file must be
published in the Figma file. No component is drawn before this is complete.

---

## Step 4 — Components (atoms → molecules → organisms)

**Open `method/04-components.md`.**

Build order: atoms → molecules → organisms. Never composite before its parts exist.

> **Every component is auto-layout (R1) and verified in isolation before use (R5, R7).** Create
> it, screenshot it on the Components page, confirm it renders correctly, record its
> `componentPropertyDefinitions`, and only then place instances. A broken component multiplied
> across five pages is five broken pages.

### 4a. Figma component invariants (from method/04-components.md)

- **States and kinds as variant axes** — Default / Hover / Active / Disabled / Error on one variant set, not forked copies.
- **One base atom; every higher structure instances it** — override a slot on the base; never paste duplicates.
- **Responsive components: one set, `Breakpoint` variant {Desktop, Tablet, Mobile}** — not three unrelated frames. Identity and tokens are shared; only layout changes.
- **Overlay/open states co-located** — author as a hidden child frame inside the same variant (drawer open, mega-menu expanded, bottom-sheet).
- **Function-grouped pages** — `Components / Actions`, `Components / Forms`, `Components / Cards`, `Components / Nav`, `Components / Layout`. Never flat or feature-grouped.
- **Path taxonomy**: `design_system/<BrandName>/components/<Name>` for every component.

### 4b. Required component inventory (minimum viable kit)

Built from `page-skeletons.md` section requirements. Each must be bound to semantic variables:

**Navigation**
- Header (Desktop / Tablet / Mobile), with utility cluster and mega-menu co-located as hidden states
- Footer (all 3 breakpoints), with newsletter band as an optional slot
- Breadcrumb atom

**Commerce atoms**
- Product card (image+badge / category eyebrow / title / price / swatch row)
- Price display (with sale/compare state as variant)
- Swatch chip (color variant axis)
- Rating atom (star row + count)
- Badge / pill (semantic status axis)

**Actions**
- Button family: Primary / Secondary / Ghost (size × state axes)
- Icon button (separate family — icon-only has no content-type axis)
- Link text (default / hover / visited)

**Forms**
- Field (label + input + helper/error slots; states = Default / Focus / Error / Disabled)
- Checkbox / Radio
- Select dropdown
- Quantity stepper

**Cards + content**
- Section-Header organism (eyebrow? / heading / supporting? / action? — slots via hidden layers)
- Trust/USP chip (icon + label)
- Review card (avatar + rating atom + body)

**Layout**
- Grid container frame (one per breakpoint, with correct margin/column/gutter from Step 3e)
- Divider (horizontal hairline, bound to `border` semantic token)

### 4c. Register-conditional components

Switch on `brand.register` from the token file:

- **storefront / taxonomy-commerce**: add filter sidebar, control toolbar (result count + sort), pagination, cross-sell rail, cart line item, checkout step indicator
- **rich-app / dashboard**: add nav rail (expanded / collapsed variants), stat card, table primitive, empty-state organism (four types: passive-data / actionable-first-run / empty-table / generic)
- **marketing / brand site**: add hero organism, conversion-ribbon, press-logo strip

### 4d. Signature move

The `signatureMove` from the token file must exist as a named component or component annotation.
It is not decoration — it is the brand's one authored moment, and it must appear in the library
as a reusable asset so it can be placed consistently across pages.

---

## Step 5 — Pages (desktop → tablet → mobile)

**Open `method/05-composition.md` and `method/page-skeletons.md`.**

Build the pages the brief (GENERATE.md Step 0 §8) calls for. The canonical section stack per
page type is in `page-skeletons.md`; the composition laws below apply to all of them.

### 5a. Composition invariants (enforced on every page)

- **Band chassis** — full-width horizontal sections, content sets height (no fixed slot heights)
- **One token ramp drives everything** — every gap, padding, width from the spacing/grid scale
- **Chrome / body split** — `GLOBAL CHROME + BODY STACK`; chrome (header+footer) is a single
  component instance per breakpoint, not redrawn per page
- **Density oscillation** — never two tall/heavy bands back-to-back; on high-chroma registers,
  oscillate surface weight (saturated ↔ neutral) as a second axis
- **Grid-break = narrowing** — the only intentional grid break is narrowing to a centered column;
  never widening text to full-bleed
- **Threaded proof** — ratings/badges/quotes at multiple depths, not clustered in one block
- **Section-opening grammar** — a reusable Section-Header organism opens each band

### 5b. Responsive authoring rule

Each page is a **Section** (R4) containing three sibling frames, built side by side:
- `<PageName> · Desktop` — 1440px wide, using Desktop grid style
- `<PageName> · Tablet` — 768px wide, using Tablet grid style
- `<PageName> · Mobile` — 390px wide, using Mobile grid style

Each frame is a VERTICAL auto-layout of component **instances** at the matching `Breakpoint`
variant, plus any inline bands (also auto-layout). Set the page frame to hug height
(`primaryAxisSizingMode='AUTO'`) and every child to `layoutSizingHorizontal='FILL'`.

**Section order is breakpoint-invariant.** Derive tablet/mobile ONLY by:
1. Collapsing column count (N → N/2 → 1) — on a card row, change how many instances per row;
   re-equalize heights per R3.
2. Switching a 2-column split (hero split, contact form + aside) from a HORIZONTAL to a
   **VERTICAL** auto-layout so it stacks — same children, same order, just the container direction.
3. Drawer-izing filters/sidebars behind a trigger + sticky "Show results" bar.
4. Nav collapse (hamburger replaces inline nav at Tablet; **bar height held constant**).
5. Stacking an inline button row to full-width stacked buttons (`layoutSizingHorizontal='FILL'`).

**Never re-order sections per breakpoint.** Re-ordering silently forks the funnel.

**Responsive components carry the reflow, not the page.** A component that changes shape across
breakpoints (Header → hamburger, Footer → stacked, Hero → stacked CTAs, Newsletter → stacked
form) is **one variant set with a `Breakpoint` axis** — author all three variants, then the page
just places the matching variant. Width-agnostic components (Card, Section-Header, Button) need
no breakpoint variant; they FILL their container and reflow automatically.

### 5c. Page-by-page build (from page-skeletons.md)

For each required page, instantiate the section stack from `page-skeletons.md` in order:

1. Place `GLOBAL CHROME` (header component instance) as the first section
2. Add a breadcrumb instance as the first in-body section on deep/transactional pages (PLP, PDP, Cart, Checkout, Blog article, Account, Auth, Legal); homepage gets none
3. Instantiate the page's body stack in the prescribed section order
4. Close with `GLOBAL CHROME` footer component instance

Every section uses a component instance from Step 4 — never raw drawn shapes.

### 5d. Container contract (enforced per breakpoint)

| Breakpoint | Container behavior |
|---|---|
| Desktop | Capped + centered; `max-width: grid.breakpoints[desktop].container` |
| Tablet | Mid-width; `max-width: grid.breakpoints[tablet].container` |
| Mobile | Edge-to-edge; margin → 0, container inset = device padding |

Three independent padding families: device margin ≠ container inset ≠ section spacing.
All three values come from the spacing scale (Step 3d), never hardcoded.

---

## Step 6 — Verify

**Open `method/anti-slop.md`.** Run the full checklist. Fix any hit at the cheapest layer it
lives on, then re-check. Only a clean pass means the file is deliverable.

**Required checks:**

1. **Name the ONE bold move.** Point to the frame where it lives. If you cannot name it in one
   sentence and point to it, the file is not finished. (`brand-tokens.json → signatureMove`)

2. **Traceability audit.** Spot-check 10 random nodes across different pages:
   - Every color fill → a semantic variable (never a raw hex)
   - Every spacing value → a space variable (never a raw number)
   - Every type style → a text style from Step 3c (never a detached local style)
   - Every radius → a radius variable (never a hardcoded corner radius)
   A single raw value is a failure — fix it, then continue.

3. **Breakpoint parity.** Every page type has all three breakpoint frames. Desktop, tablet, and
   mobile frames share section identity; only layout differs.

4. **Component bindings.** Every page section is a component instance, not a flattened group.
   Unlinking a component for local edits is not permitted on the first draft.

5. **Anti-slop color pass.** No equal-lightness steps. No swatch without contrast verdict in
   the description. No `dark-` prefix name on a semantic variable.

6. **Layout-integrity pass (R1–R3).** Screenshot **every** breakpoint frame of **every** page
   and actually read it — this is not optional and not satisfiable by "I built it" (R7). Look for:
   collapsed/10px-tall nodes, overlapping text, clipped headings, unequal sibling cards, any
   frame shorter than its content. Equal-height card rows must be verified visually, not assumed.
   Confirm there is **no absolute-positioned layout** (only decorative art may be absolute, R1)
   and **no emoji iconography** (R6).

7. **Provisional-principle flags.** Any component or composition decision that traces to a
   provisional-tier principle in `evidence/VALIDATION.md` must be noted in the frame's
   annotation so the human reviewer knows it is a bet, not a proven law.

**Record (brief record §Figma):** the file key, variable collections created, component list,
and the page frames built per breakpoint, plus the named bold move and the traceability verdict.

---

## Honest limits (always state these)

- **Generated variables are only as good as the token file.** If `brand-tokens.json` has gaps
  (missing contrast ratios, incomplete spacing scale), the Figma file inherits them. Fix the
  token file; do not paper over gaps with raw values in Figma.
- **This is a strong first draft.** Component state coverage, edge-case content, real imagery,
  and motion layers are for the human iteration pass.
- **Figma variable aliasing has limits.** Text styles are not yet full Figma variables (as of
  2025). Composite type tokens are approximated as named text styles; until Figma releases full
  typography variable support, the face/weight/size/tracking composite is best captured as a
  named style with the full spec in its description.
- **The file key must be real.** If the user does not know the Figma file key, halt at Step 1
  and ask. Never guess, infer, or reuse a key from another project.
