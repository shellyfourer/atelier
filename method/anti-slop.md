# atelier — anti-slop QA checklist

> **This file is the verification checklist, not a design guide.** You *build* from the method
> chapters (`00-decide` → `01-color` · `02-typography` · `03-space-grid` · `04-components` ·
> `05-composition`, each with a "Premium craft signals" section) and the brand book. You *verify*
> here. Run this before shipping any token system, component library, brand book, or page set.
>
> **How to run it:** every item is a **yes = FAIL**. Walk each box; if the answer is "yes, that's
> present," fix it at the cheapest layer it lives on, then re-check. A pass means **every box is
> no**. `[S0x]` tags cite the sources in `evidence/VALIDATION.md`; `[S0x·prov]` = single-source.
>
> **Two passes, run both** (they catch different failures — a file can pass A and fail B):
> **Pass A — method conformance** (is the system built right). **Pass B — aesthetic giveaways**
> (does the output *look* AI-made even though the system is clean). The figma skill's Step 6 runs
> both.

---

## Rule 0 — the override (check first)

- [ ] **Can you NOT name the one bold move** in the finished work, in one sentence, pointing to
  where it lives? A design with no point of view is slop no matter how clean its tokens are. Zero
  bold moves = templated; many = noise. (How to choose/spend it: `00-decide` premium bar + Standing
  Policy.) [all]

---

# PASS A — Method conformance

## A1 · Architecture / tokens

- [ ] Does any component or screen reference a **raw primitive or literal value** (a hue step, a
  hex, a bare px) instead of a semantic alias? Primitives bound into UI is the #1 immature-system
  tell. [S01,S03,S04,S05]
- [ ] Is any **semantic token named after its value** (`blue-button-color`) rather than its
  role/intent (`text-primary`, `icon-error-on-solid`)? [S01]
- [ ] Were any **tokens invented ad hoc per screen** instead of coming from a fixed matrix? [S01]
- [ ] Is **one naming grammar used across tiers** (abstract/t-shirt names leaking into primitives,
  or literals into semantics), or one domain special-cased to diverge from the others? [S01,S03,S04]
- [ ] Is a **foundation shipped as a bare value dump** (no explain-show-apply: definition + per-level
  demo + usage note)? [S01]

## A2 · Color

- [ ] Does any ramp **force a mid-step anchor** (symmetric 50→900 with the main color always at 500)?
  [S01,S07]
- [ ] Are ramp steps **equal-lightness / linearly interpolated** instead of perceptually spaced
  (denser in the lights)? [S01,S07]
- [ ] Are swatches shipped **without per-step contrast + an AA/AAA/fail verdict**? [S01,S07]
- [ ] Is a hue collapsed to **one ramp** that can't cover its warm/muted/tinted variants? [S01]
- [ ] (thin-semantic) Does a component **bind a ramp step directly** (a "600", a "-foreground-900")
  instead of a role token? [S03,S05]
- [ ] (thin-semantic) Are there **parallel light/dark component variants or a `dark-` palette**
  instead of one name with a value-mode column? [S03,S05]
- [ ] Is a **foreground shipped without its paired background** (orphan `on-color`)? [S03,S05]
- [ ] (category-color) Is a category minted as a **lone accent** instead of an {accent, tint} pair,
  or the accent not scoped (chrome=brand / content=category / else fallback)? [S08·prov]

## A3 · Typography

- [ ] Is any style defined as a **lone font-size** (not pinning line-height, tracking, weight,
  paragraph-spacing)? [S01,S04,S05,S08]
- [ ] Is the scale a **single flat linear ramp** (h1…h6 / one 12→96 list) instead of a role×size
  matrix? [S01]
- [ ] Is **letter-spacing hand-picked per step** rather than a consistent function of size? [S01]
- [ ] Is a **constant line-height multiplier** used across the whole scale (display and body want
  opposite leading)? [S01,S04]
- [ ] Are line-heights **arbitrary decimals off a rhythm grid**? [S01]
- [ ] Is **weight baked into the size step** ("heading = always bold") instead of an independent
  axis? [S01]
- [ ] Is **one font family hardcoded everywhere** (no display/body slots provisioned)? [S01,S04]
- [ ] Are styles **size-only with no per-breakpoint resolution**? [S01,S04]
- [ ] (register) Is **negative tracking applied to display reflexively** on a clinical/technical/B2B
  brand (tracking is a register knob; default 0)? [S05·prov]
- [ ] Do single-line centered roles (button/nav/chip) carry **body line-height** instead of ~1.0?
  [S05·prov]

## A4 · Space / radius / elevation / grid

- [ ] Is there a **single global border-radius** instead of size-keyed per-component radius (or a
  deliberately-chosen single-knob for a flat app)? [S01,S04 / tension S03,S05]
- [ ] Is elevation **one flat drop shadow** instead of two stacked layers (ambient + contact) on an
  ordered ramp (or the deliberate 1px-ring for dense UI)? [S01,S04 / tension S03]
- [ ] Are shadows **invented per-component/inline** instead of mapped to a named, role-tied level?
  [S01]
- [ ] Are **spacing / padding / sizing collapsed into one token set** instead of separate role-named
  axes? [S01]
- [ ] Are primitives **number-indexed** (`space-1`) instead of named by literal value? [S01]
- [ ] Is **every effect forced onto one ramp length** (blur wants many steps, inner-shadow few,
  focus-ring categorical)? [S01]
- [ ] Are **`*-none` tokens missing** ("intentionally square/flush" must be a deliberate token)?
  [S01]
- [ ] Are **effect colors hardcoded** into each shadow instead of a tiny alpha-only tint set? [S01,S03]
- [ ] Is a **content width hardcoded**, or desktop gutters/margins reused on smaller tiers, instead
  of `margin=(device−container)/2` with gutters from the spacing scale and mobile→edge-to-edge?
  [S07,S04]

## A5 · Components

- [ ] Is there a **monolithic Button/Input/Card** with a sprawling variant matrix instead of
  job-scoped sibling families? [S01,S05]
- [ ] Is any component **forked per interaction state** (`Button Hover` as its own component) instead
  of states-as-variant-axes? [S01,S03,S05]
- [ ] Is a **base primitive anonymous/buried or copy-pasted** into each composite instead of named +
  instanced? [S01,S03,S05]
- [ ] Is **density/scale baked as a per-component variant** instead of a parallel compact library?
  [S01]
- [ ] Are components **in a flat namespace** instead of a path taxonomy + functional pages? [S01,S05]
- [ ] Is any component **missing a one-line usage note**? [S01]
- [ ] Is an **atom conflated with its labeled molecule** (bare field vs field group)? [S01]
- [ ] Is a **single-state element wrapped in a variant set** for symmetry? [S01]
- [ ] (responsive) Is a component shipped as **one fluid layout** instead of an explicit
  `Breakpoint` variant set with a priority reflow ladder? [S04,S05,S08]
- [ ] (responsive) Do **inline nav links survive to tablet/mobile** instead of collapsing to a
  hamburger at the threshold with bar height held constant? [S04]
- [ ] (responsive) Are **hit targets shrunk** to fit a toolbar instead of shedding low-priority icons
  by priority? [S04]
- [ ] (responsive) Is an **overlay/open-state authored as a separate screen** instead of co-located
  as a hidden state in the same variant? [S04]
- [ ] (density) Is importance signalled with **large type in a dense view** instead of weight +
  muted-color on the small scale? [S03]
- [ ] (density) Are **numeric columns left-aligned / proportional figures** instead of right-aligned
  tabular? [S03]
- [ ] (density) Is a table **one hardcoded block** instead of toggle-able toolbar/body/footer with
  pre-reserved checkbox/sort slots? [S03]
- [ ] (density) Does a stat/KPI card have **two competing focal points** instead of one dominant
  value? [S03]
- [ ] (app shell) Is there **one sidebar per role/mode** instead of one rail parameterized by
  (role, mode, active-page) from a permission matrix? [S03,S06]
- [ ] (app shell) Is any **empty/loading/error state blank or spinner-only** instead of a typed
  state (icon + title + support + role-aware CTA) with a layout-matching skeleton? [S03,S06]

## A6 · Page composition / skeletons

- [ ] Are **two tall/dense sections stacked** with no short calm band between? [S01,S04,S05,S06]
- [ ] (high-chroma) Are **two full-saturation full-bleed bands back-to-back** (surface-weight is a
  second oscillation axis)? [S06·prov]
- [ ] Does **every section share the same height/content weight** (uniform = template)? [S01,S04,S05,S06]
- [ ] Is the **same 50/50 split orientation repeated** instead of flipping sides each time? [S01,S04,S05]
- [ ] Does **text run full container width** in reading sections instead of a capped measure?
  [S01,S04,S05,S06]
- [ ] Is a grid break a **widening / full-bleed for text** instead of a narrowing to a centered
  column? [S01,S04,S05,S06]
- [ ] Is the **hero overloaded** with copy / multiple CTAs / feature lists instead of a light stage
  handing proof to the band below? [S01,S04,S05]
- [ ] Is any **spacing/width ad-hoc per section** instead of resolved to the shared ramp? [S01,S04]
- [ ] Is **proof clustered in one block** instead of threaded at multiple depths? [S01,S04,S05,S06,S08]
- [ ] Are **sections ordered arbitrarily** instead of a decision narrative with the primary action
  reachable throughout? [S01,S04,S05]
- [ ] Does a section **lack the reusable header grammar** (eyebrow?/heading/support?)? [S01,S04,S05,S06]
- [ ] (homepage) Are **two same-purpose bands adjacent** (two product rails, or two story bands)
  instead of convince/convert alternation? [S05·prov]
- [ ] Is a page modeled as a **flat section list** instead of GLOBAL CHROME (once) + per-template
  BODY stack, with a breadcrumb on deep pages only? [S04,S05]
- [ ] Are **sections re-ordered per breakpoint** instead of invariant order + column-collapse +
  drawer-izing? [S04,S05,S08]
- [ ] Is any **required skeleton section missing or out of order** for the page type (check each page
  against `page-skeletons.md`), or a **recommended** one dropped with no reason? [S04,S08]
- [ ] Is a **buybox flattened** to "title + price + button" instead of its ordered sub-skeleton?
  [S04]
- [ ] Does an **editorial/long-form page** end on a buy-CTA / dead end instead of a lateral
  (related/next) close at a readable measure? [S04,S05]
- [ ] Is the **PLP toolbar (result count + sort)** or a progressive-load affordance missing? [S04]

---

# PASS B — Aesthetic giveaways (does it *look* AI-made)

> A file can pass all of Pass A and still fail here — these live in appearance, not method. This is
> the pass that was missing when a real build shipped arrows-on-links, dot-joined meta, and an
> eyebrow over every heading. The positive "what to do instead" is in the chapters' "Premium craft
> signals" + the `00-decide` premium bar; this is the scan.

## B0 · The two gates

- [ ] **Swap test fails:** if you swapped the logo + brand name, could this belong to any product?
  (Too generic = the identity isn't working.) [S09]
- [ ] **Void test fails:** after cutting tells, is the result merely *clean* — flat-white, thin-grey
  borders, default font, no identity motif, no deliberate accent — rather than *alive and specific*?
  The over-filtered sterile default is its own slop. [S09]
- [ ] **Purpose test fails:** is any technique present (gradient, shadow, eyebrow, arrow, badge,
  card, pattern) whose one-line purpose you **cannot write**? "Looks modern / AI-safe" is not a
  purpose. [S09]

## B1 · Visual / color

- [ ] A **generated-palette default**: blue→purple / blue→cyan / purple→pink gradient, full-page
  colored glow, neon accent, pastel blocks, radial orbs, purple-and-black "tech" scheme? [S09]
- [ ] **Trend-stacking** with no purpose (glassmorphism + mesh gradient + glow + grid + mono +
  pill-everything)? [S09]
- [ ] **Glassmorphism on >1–2 elements** (navbar + cards + modal + sidebar at once)? [S09]
- [ ] A **soft shadow or glow on everything** so the page floats? [S09]
- [ ] **One accent spent on everything** (buttons + icons + badges + links + rules + backgrounds)
  instead of rationed? [S09 / S01,S03,S06]
- [ ] A **background grid / dot / blueprint / graph-paper** pattern with no identity reason? [S09]
- [ ] **Dark mode defaulted** "because it looks tech," with no brand/user reason? [S09]
- [ ] **Grey skeleton bars used as the hero/product shot**? [S09]
- [ ] **Pure #000 / #fff / a flat mid-grey** where a register-tuned neutral was warranted? [S04 / S09]

## B2 · Layout / section

- [ ] The **template stack** on autopilot (Hero → subtitle → 2 CTAs → screenshot → feature grid →
  testimonials → FAQ → CTA → footer) rather than content-driven order? [S09]
- [ ] **Uniform section rhythm** (every section = centered title + subtitle + identical card grid),
  or the only variation being the background flipping every other section? [S09]
- [ ] **Copy-paste feature cards** (identical size/icon/padding/height) with no hierarchy? [S09]
- [ ] A **default bento mosaic**, a **fake terminal window** hero, or **"How It Works" as exactly 3
  round-icon numbered steps** when the content isn't a real sequence? [S09]
- [ ] Reflex furniture: **"Trusted By" logo bar** under the hero, **"Most Popular" middle tier**,
  **exactly 3 pricing columns**, **4-column Product/Company/Resources/Legal footer** — not matched
  to real content? [S09]

## B3 · Decoration / typographic

- [ ] An **arrow (→ / ↗) appended to link/button text** as default identity? [S09 · Kristina build]
- [ ] A **tracked-out ALL-CAPS eyebrow / pill above a heading** (especially restating the heading,
  or appearing over *every* section)? [S09 · Kristina build]
- [ ] **Middle-dot-joined meta** (`Author · 8 min read · Date`, `A · B · C`) as a reflex? [S09 · Kristina build]
- [ ] A **`WORD — fragment` spaced-em-dash label**, **monospace for small data labels**, or
  **large-mono / extreme-tracked-uppercase** "AI typography"? [S09]
- [ ] **One word accented in a headline** (italic/colored/bold for pop) instead of the line set
  whole? [S09]
- [ ] **Generic AI glyph icons** (sparkle, star, magic, lightning, diamond, cube, robot, orb), or an
  icon set picked for its **recognizable-library look** rather than relevance? [S09]
- [ ] A **colored left-stripe** on cards/rows as decoration, or **AI capsule badges** ("AI Powered",
  "Beta", "New" as pill + thin border + glow + dot + uppercase) with no real status? [S09]
- [ ] A **typeface chosen with no written reason** / the model-default (Inter, Geist, Space Grotesk)
  reached for because it's safe? [S09]

## B4 · Copy (design-adjacent)

- [ ] An **em dash (—)** used as a reflex connective in UI copy the agent wrote? [S09]
- [ ] A **generic CTA** ("Get Started", "Learn More", "Try Now", "Explore", "Discover") instead of
  the named action? [S09]
- [ ] **AI buzzwords** (AI-powered, seamless, revolutionary, next-generation, cutting-edge, unlock,
  elevate, empower, game-changing)? [S09]
- [ ] Any **fabricated** statistic, testimonial, logo, name, trust/compliance claim, or ghost nav
  link — anything that looks real but isn't? (No real data → show nothing.) [S09]

## B5 · Liveliness (the add-back — these must be YES, not no)

> After the cuts, confirm the design is alive. Unlike every box above, **a "no" here is a fail.**

- [ ] **Dials set and held?** ENERGY / RHYTHM / MOTION declared (from the brand book) and the output
  actually matches (a "bold/varied" claim that renders uniform is a fail). [S09]
- [ ] **One focal point per screen?** [S09]
- [ ] **Whitespace used as structure**, not leftover? [S09]
- [ ] **One deliberate accent** present (not zero, not everywhere)? [S09]
- [ ] **One identity motif** — a specific, repeated pattern/gesture/typographic voice that makes the
  design belong to this brand (the one bold move, recurring)? [S09 / all]

---

## Figma-read discipline (when auditing an existing file)

- [ ] Did you **halt on a missing/placeholder fileKey** (`undefined`/`null`/`{{…}}`) rather than
  guess one, reuse another project's, or synthesize findings? An empty findings list is the honest
  output when the source can't be read. [S05·prov]
- [ ] Did you **drill page→child-frame IDs before screenshotting** rather than read a 30000px canvas
  as one unreadable thumbnail? [S08·prov]
