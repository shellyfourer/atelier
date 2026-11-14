---
name: brandbook
description: >-
  Creates a complete, professional brand book (brand guidelines) as a PDF AND
  generates the project's real design-system foundation, from intake to signed-off
  document. Use at the START of any brand/design project: if the client has no
  brand book, this skill creates one — asking the client questions first (logo?
  colors? fonts? direction?), then RUNNING the atelier method chapters to generate
  the actual foundation tokens (color posture + semantic roles, the composite
  type-scale matrix, spacing/radius/elevation/grid), rendering them into a 16:9 PDF
  from a proven agency structure. Nothing else in a project proceeds until the
  brand book is agreed and signed off. Output: an HTML/CSS → PDF brand book PLUS
  brand-tokens.json — the design system the rest of the cycle builds from.
---

# brandbook

Creates a real brand book — the kind an agency ships — as a **PDF document**, and treats it as
the **gate** for everything downstream. **It is also where the design system is born:** the brand
book RUNS the atelier `method/` chapters to generate the project's actual foundation tokens, and
`brand-tokens.json` **is** the design system that components, pages, and the production build
inherit. Get the brand book right and the whole cycle stands on a real foundation; get it wrong
and everything downstream inherits the error.

If the client doesn't have one, this skill makes it; and no token, component, or page is produced
until the client and the agent **agree on the brand book and sign it off.**

It is a standalone skill, and it is the first thing `atelier`'s `GENERATE.md` invokes.

## The non-negotiable flow

```
0. DECIDE — run method/00-decide.md. Record all decisions before anything else.
1. ASK  — intake questions first (never assume). Does the client have a logo? colors?
          fonts? a direction? references? existing assets?
2. GATHER — collect what exists; identify what's missing.
3. GENERATE — create everything missing using the atelier method, in strict order:
          00-decide → 01-color → 02-typography → 03-space-grid → brand-tokens.json (validated)
4. PRESENT — render the brand book PDF and show it to the client.
5. ITERATE — revise against feedback.
   ───────────────── HARD GATE: do not proceed past here without sign-off ─────────────────
6. SIGN-OFF — explicit client agreement on the brand book.
7. HANDOFF — emit brand tokens for the design-system / page build to consume.
```

**Steps 3–6 can loop many times.** The agent must not start the design system, components, or
pages until step 6 is reached. The brand book is the contract.

**Within Step 3, the sub-steps are an ordered pipeline with gates — not a flat list.** Each
sub-step produces a required output that the next one reads from. An agent may not skip ahead.

---

## Step 0 — Decisions first (run method/00-decide.md BEFORE intake)

Before asking the client a single intake question, run **`../method/00-decide.md`** and record
every answer to the decision checklist. These are the inputs the method chapters read from; no
token can be correctly computed without them.

**Every one of the following must be a recorded written answer before Step 1 begins:**

1. **Register** — name it (e.g. "editorial-warm-premium"). This is the single most load-bearing
   decision; everything else follows from it.
2. **Product archetype** — which of: storefront / marketing / editorial / dashboard / app.
3. **Color's job** — answer "what does color DO in this brand?" then select posture A/B/C/D and
   state *why* (e.g. "posture A — tonal ramp — because the brand needs a full neutral range; color
   is a signal not a palette"). A posture picked without a stated reason is a guess.
4. **Tier count and scarce-signal rule** — how many postures are stacked; which hue carries
   information; which surfaces are neutral.
5. **Type strategy** — A (single family) or B (role-assigned multi). If B: each face must have a
   named job, and face count ≤ 3.
6. **Tracking / letter-spacing register** — explicitly stated: "0 by default" OR "negative on
   display, editorial/luxury register, justified." An agent that ships negative tracking on a
   clinical brand has failed this check.
7. **Density line** — compact / balanced / generous.
8. **Responsive discipline** — confirm: 3 breakpoints (desktop / tablet / mobile), all ordered
   decisions, reflow only where the layout breaks.
9. **The one bold move** — name it and place it ("the brand's signature risk is X, spent on Y
   page/component"). Must be nameable before Step 3 ends; "not sure yet" fails.
10. **Accessibility baseline** — AA or AAA; which surfaces carry body text; note any accent that
    will only pass at large/graphic sizes and scope it explicitly.

Record these as a decision block at the top of `brandbook/intake/<project>.md`. They must be
present before generation starts.

---

## Step 1 — Intake questions

Collect before generating anything. Ask conversationally; don't dump all at once if a few
answers make others moot. Use **`intake/questions.md`** as the canonical question list (the
summary below is a quick reference — `questions.md` is authoritative; keep them in sync).

**Brand basics**
- Brand / company name, and the one-line "what it is".
- Industry / register, and the organizing idea (what makes it *this* brand, not a competitor).
- Audience and tone (3–5 adjectives: e.g. clinical, playful, premium, warm, technical).

**Existing assets (the key branching questions)**
- **Do you have a logo?** If yes → ask for the file (SVG/PNG/PDF) and whether it's final.
  If no → the skill will generate a **wordmark direction + candidates** (see below).
- **Do you have brand colors?** If yes → collect exact values (HEX/RGB/Pantone/CMYK if print).
  If no → generate a palette per the color method.
- **Do you have brand fonts?** If yes → names + licensing/source. If no → propose a pairing.
- **Do you have brand photography?** If yes → use it on the placement/imagery pages. If no → the
  skill sources real, mood + color-matched licensed stock (`template/photography.md`) — **never a
  placeholder block.**
- **Any existing brand book, references, or sites** you like (and dislike)?
- **Where will this brand live?** (web, print, app, packaging) — decides which pages matter.

**Logistics**
- Primary language; any secondary languages.
- Who signs off, and by when.

Record answers appended to the decision block already written in `brandbook/intake/<project>.md`.

---

## The no-logo path — generate a wordmark

When the client has no logo, **do not block and do not fake a final mark.** Generate a
**typographic wordmark direction + a few candidates**:

- Build 2–4 wordmark candidates from the chosen/proposed typeface, each making one deliberate
  letterform move (a distinctive terminal, an italic swap, a ligature, a cut).
- Present them honestly as **direction to iterate**, not a finished logotype (per atelier's logo
  limits: a client-ready final mark needs human iteration).
- Once the client picks one, it becomes the book's logo and all logo pages are built around it.

---

## Step 3 — Generate the REAL design system by running the method chapters

**This is the most important thing the brand book does.** It is not a standalone PDF — it is
**where the design system is born.** The method chapters are the single source of truth; the
brand book never invents its own parallel logic.

**The pipeline is strictly ordered. Each stage produces a required output; do not proceed to
the next until that output is complete and recorded.**

### 3a — Color (run `../method/01-color.md`)

Required output — both tiers, with contrast:

1. **Primitive tier** — raw named color values (ramp or palette). Never consumed by UI directly.
   Brand-colors page renders these (HEX always; RGB always; Pantone/CMYK if print is in scope).
2. **Semantic role tier** — role-named aliases pointing only at primitives:
   `text-primary`, `text-secondary`, `surface`, `surface-alt`, `surface-inverse`, `accent`,
   `border`, `text-on-dark`, plus any brand-specific roles. UI binds to these, never raw hex.
3. **Contrast ratios — recorded as literal values, not implied.** For every semantic role that
   carries text, record the actual measured ratio and pass/fail verdict in `brand-tokens.json`
   under `colors.semanticRoles[*].contrast` (e.g. `"7.1:1 — AAA"`). A role without a recorded
   contrast value is an **incomplete token**; do not proceed to 3b until all text-bearing roles
   have verdicts. Any accent that only passes at large/graphic sizes must be scoped explicitly.

Do not proceed to 3b until `colors.roles` and `colors.semanticRoles` (with contrast) are
written and internally consistent.

### 3b — Typography (run `../method/02-typography.md` + `template/fonts.md`)

Two required parts, both must be complete before 3c:

**Part 1 — Font study.** Genuinely study the register (see `template/fonts.md`). Pick real,
self-hostable faces (Fontshare/Google Fonts, OFL/free-commercial). Never a reflexive default.
Serif body for editorial/long-form registers. Record the exact `@font-face` source in
`brand-tokens.json → type.faces`.

**Part 2 — The composite type-scale matrix.** Every role must carry all of these fields:

| Field | Rule |
|---|---|
| `face` | named slot (display / body / accent) |
| `weight` | named (Semibold / Regular / Medium…) |
| `size` | px value derived from base × ratio — **not eyeballed** |
| `lineHeight` | function of size: inverse to size, snapped to 2/4px grid; 1.0 for single-line roles (button, label) |
| `tracking` | register knob: 0 by default; negative on display **only** for editorial/luxury; never negative on body/caption |
| `mobile` | per-breakpoint swap — the whole composite ~one size notch down; this field is **not optional** — the production build needs it |

Roles: Display/H1, Headline/H2, Title/H3, Subtitle/deck, Subheading/label, Body, Caption/meta,
Button/nav. Add a Script/accent role only if the brand has an accent face.

Record scale derivation params (`base`, `ratio`, `rhythmGrid`, rules) in `brand-tokens.json →
type.scale` and the full composite matrix in `brand-tokens.json → type.roles`.

The brand book gets a **Type scale page** showing these specs with live specimens. Eyeballed
per-page font sizes are a FAIL — the scale is a studied, computed system.

### 3c — Spacing / sizing / radius / elevation / grid (run `../method/03-space-grid.md`)

Required decisions — both postures must be explicitly chosen and stated:

- **Radius posture A** (size-keyed to component tier) or **posture B** (single global knob) —
  record which and why.
- **Elevation posture A** (two-layer: ambient + contact shadow) or **posture B** (1px ring) —
  record which and why.

Required output in `brand-tokens.json → space` and `→ grid`:

- `baseUnit` (e.g. `4px`)
- `scale` — integer-multiple steps: 4, 8, 12, 16, 24, 32, 48, 64 (and 96/128 if needed)
- `radius` — ramp per chosen posture, plus `pill` and `none` tokens
- `elevation` — ramp per chosen posture, tokenized and bound to component roster
- `grid.breakpoints` — for each of desktop / tablet / mobile:
  - `container` max-width
  - `columns` count
  - `gutter` — from the shared spacing scale; **one value per breakpoint × column-count
    combination** (a 12-col desktop and an 8-col tablet can have different gutters)
  - `margin` = (device width − container) / 2

These may not all get a dedicated brand-book page, but **all must be in `brand-tokens.json`** —
the design-system build requires them.

### 3d — Signature move

Name the brand's one bold move and place it on its dedicated spread. It must be nameable: "the
signature is X, it lives on Y" is done; "not sure yet" means Step 3 is not done.

### 3e — Photography

Per `template/photography.md`. Client photos if supplied; real, mood + color-matched licensed
stock otherwise. **Never a placeholder block.** Embed as base64; credit photographer.

### 3f — Validate brand-tokens.json (gate before Step 4)

**Before rendering a single page, validate `brand-tokens.json` against
`brandbook/template/brand-tokens.schema.json`.** Every required field must be present.
Run through this checklist:

- [ ] `colors.roles` — all primitives with HEX and RGB
- [ ] `colors.semanticRoles` — all roles with `token`, `primitive`, and `contrast` (literal ratio)
- [ ] `type.scale` — base, ratio, rhythmGrid, lineHeightRule, trackingRule, breakpointRule
- [ ] `type.roles` — every role has face / weight / size / lineHeight / tracking / **mobile**
- [ ] `space.scale` — full step list
- [ ] `space.radius` — all tiers from chosen posture, plus pill and none
- [ ] `space.elevation` — all tiers from chosen posture
- [ ] `grid.breakpoints` — desktop / tablet / mobile each with container / columns / gutter / margin
- [ ] `signedOff.status` is `"draft"` (will be changed to `"signed-off"` at Step 6)

**A missing field means Step 3 is not done. Return and complete it. Do not proceed to Step 4
until every checkbox above passes.** The JSON is the design system; an incomplete JSON means
an incomplete foundation.

---

## Quality bar — non-negotiable execution rules

These are hard-won from real runs: a first pass that violated them read as weak/templated; fixing
them made the output genuinely premium. **Run `template/QUALITY.md` as a pre-ship checklist
every time, before Step 4.** The load-bearing rules:

1. **Render the client's REAL logo — never reconstruct, redraw, or recolor it.** Place the actual
   supplied logo file (SVG/PNG) directly, as an image, on every page the logo appears. Do **not**
   rebuild the mark in HTML/CSS/SVG by hand — it will change letterforms, script, proportions, and
   that is the exact "don't alter the logo" sin the book itself preaches.
   - If the logo doesn't contrast with a ground (e.g. a dark logo on a dark cover), **change the
     ground or frame the logo** (e.g. place it in a light tile) — never recolor the mark.
     A legitimate inverted/mono "color version" is allowed *only* as an explicit, labelled color
     version, generated from the real asset, never as a silent substitute.
   - Embed the logo (data URI or local file) so the PDF is self-contained.

2. **Use REAL fonts that actually render — never generic fallbacks, never a reflexive default.**
   - Do a genuine **font study** for the register (see `template/fonts.md`). Pick real,
     self-hostable faces (Fontshare / Google Fonts, OFL/free-commercial).
   - **EMBED the font files** (`@font-face` with base64 or local woff2/ttf) so they render in the
     PDF — a system/serif fallback is a fail. Verify the specimen is the actual face, not Georgia.
   - **Match the face to the register.** For editorial / long-form / warm-premium brands, prefer a
     **serif reading body** — a UI sans (Inter/Roboto-class) under long essays reads "SaaS
     dashboard," the opposite of the intended warmth.
   - Record the exact `next/font` / `@font-face` setup in `brand-tokens.json` so the same faces
     drop into the client's production site.

3. **Hold the measured layout standard.**
   - Chrome: a small **tracked eyebrow** (brand name, accent color, uppercase, letter-spaced) + the
     page **title in the display face**, tight top-left stack, on a strict left margin line.
   - **Generous, consistent outer margins**; content/tint panels inset equally; everything hangs
     off the same grid lines. No drifting insets.
   - **Confident scale + whitespace.** Typeface specimens are *huge*; spec pages breathe. Timid,
     cramped pages read as templated. Source URLs top-right on the typeface pages (accent-underlined).
   - One idea per page. Cover: single axis, single layout direction — no competing alignment axes.

4. **Verify by rendering, then critically review every page before calling it done.** Render to
   PDF/image and actually look. "Looks fine in my head" is not verification. Check against
   `template/QUALITY.md` section by section.

---

## The page structure

A complete book is ~18–24 landscape (16:9) pages. Build the pages the brief needs; this is the
canonical superset and order. See **`template/pages.md`** for the detailed per-page spec.

| # | Page | Required? | Contents |
|---|---|---|---|
| 1 | **Cover** | required | Wordmark, "Brand Guidelines", year / version, author / agency |
| 2 | **Logo** | required | Primary logo, clean, on white |
| 3 | **Exclusion zone** | required | Clearspace in logo-derived units |
| 4 | **Logo guidelines / construction** | recommended | Cap-height / baseline, proportions |
| 5 | **Color versions** | required | Primary / secondary / achromatic lockups |
| 6 | **Brand colors** | required | Swatches with HEX / RGB / (Pantone / CMYK if print) |
| 7 | **Logo icon** | recommended | App-icon treatments (circle, squircle, tiny sizes) |
| 8 | **Minimum size** | recommended | Smallest legible size (print mm / screen px) |
| 9 | **Main typeface** | required | Primary font, specimen, source |
| 10 | **Secondary typeface** | recommended | Secondary font, specimen, source |
| 11 | **Typographic hierarchy** | required | Title / Subtitle / Subheading / Body roles |
| 11b | **Type scale** | required | Composite-token matrix: each role with real size / line-height / tracking / weight + live specimen. Not just role names. |
| 12 | **Typographic hierarchy — color variations** | optional | Hierarchy across grounds |
| 12b | **Design foundations** | required | Semantic roles + spacing cadence + radius + grid |
| 13 | **The signature move** | recommended | The brand's one bold move, shown |
| 14 | **The signature move — guidelines** | optional | Construction / application rules |
| 15 | **Interactive / UI text elements** | optional (web) | Buttons/links across grounds + states |
| 16 | **Logo composition rules** | recommended | Logo in H / square / V formats |
| 17 | **Logo composition — guidelines** | optional | Construction of the above |
| 18 | **Logo placement** | recommended | Logo on photography, corner anchoring |
| 19 | **Logo placement — guidelines** | optional | Safe-area construction |
| 20 | **Logo on background image** | recommended | Legibility over real imagery |
| 21 | **Logo misuse** | required | Don'ts grid (stretch, recolor, rotate, crowd…) |
| 22 | **Co-branding** | optional | Partner lockups |

**Page chrome (every inner page):** a small brand-name eyebrow (accent color) + the page title,
top-left; generous margins; one idea per page. Cover and section pages may use a full brand-color
ground; spec pages are on white/surface.

---

## Step 7 — Output

1. **The PDF** — `system/<project>/brandbook.pdf`, rendered HTML/CSS → PDF (see `template/render.md`).
2. **Brand tokens** — `system/<project>/brand-tokens.json`: the agreed logo path(s), color
   values (named + HEX/RGB/print), type roles + faces + mobile values, spacing/radius/elevation/grid,
   the signature move. This is what the design-system / page build consumes downstream.
   Set `signedOff.status` to `"signed-off"` and record `approver` and `date`.
   The PDF is for humans; the tokens are for the next tool.

---

## How the PDF is built (HTML/CSS → PDF)

- Each page is an HTML section sized to a 16:9 page box; print CSS gives one page per section.
- A single stylesheet carries the brand tokens as CSS variables, so the book is *itself* on-brand.
- Render with headless Chrome print-to-PDF (see **`template/render.md`** for the exact pipeline,
  page setup, **font embedding**, and **real-logo embedding**).
- **Fonts must be embedded** (base64 `@font-face` or local woff2/ttf) and **the real logo embedded**
  (data URI / local file) so the PDF renders self-contained with the true faces and mark.
- The template is in `template/` — adapt it per project by setting the token variables and
  filling each page's content; don't rebuild the chassis each time.
- **Verify by rendering** and run `template/QUALITY.md` before presenting (Quality rule 4).

---

## Honest limits

- **Logo = direction, not final.** When generated, it's a wordmark direction + candidates to
  iterate, never presented as a finished, trademark-ready logotype.
- **The gate is real.** If the user tries to skip to the website/design system, stop and point
  back to sign-off. An unsigned brand book means the foundation isn't agreed yet.
- **Print values** (Pantone/CMYK) are only generated when print is in scope; otherwise HEX/RGB.
- **Downstream tools must check** `brand-tokens.json → signedOff.status === "signed-off"` before
  building. A draft token file is not a valid foundation.
