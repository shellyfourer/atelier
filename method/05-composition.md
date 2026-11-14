# Page composition method

> How atelier composes a page from a system's tokens and components so it reads as *one authoring hand* — composed, not templated. Portable method only; no brand values, fonts, or screens. Validation tags cite the sources behind each claim (`[S0x]`); a single-source claim is marked `· provisional`. See `evidence/VALIDATION.md` for the ledger.

A page is not a pile of sections — it is an argument built from a fixed vocabulary. The method has four **load-bearing invariants** (independently confirmed across registers), a set of **postures** that select how those invariants are spent, and a layer of **refinements** that extend the vocabulary. Work the invariants first; they hold in every register. Reach for postures and refinements only when the product's register calls for them.

---

## The chassis

**Band chassis.** Build every page from a fixed vocabulary of full-width horizontal sections ("bands"), each owning one uniform outer margin and one top inner-padding, with **content setting height** rather than a fixed slot. A shared chassis is the single biggest driver of "composed, not templated." [S01,S04,S05,S06]

**One token ramp drives everything.** Every gap, padding, and width in the page resolves to the shared spacing/width scale; variety lives in composition and content, **never** in ad-hoc pixels. That one constraint is what reads as a single hand across an entire site. [S01,S04]

**Two nested width systems.** A wide container governs grids and media; a deliberately **narrower measure** governs reading-dominant content. Cap prose and section headers to a readable measure even inside full-width bands — a band may be full-bleed while its text is not. [S01,S04,S05,S06]

**Chrome / body split is the composition substrate.** Model every page as `GLOBAL CHROME + BODY STACK`. Chrome = {promo bar [opt] + header/nav [req] + footer [req]}, authored **once** and template-invariant; each template defines only its own body stack. Deep or transactional pages prepend a **breadcrumb as the first in-body element**; the homepage does not — breadcrumb presence is a portable signal of page depth. [S04,S06,S08]

---

## The four load-bearing laws

These four are confirmed across formal libraries, storefronts, apps, and brand-dominant and high-chroma registers alike. They are the non-negotiable core of composition.

### 1. Density oscillation

Never stack two tall, heavy sections back-to-back. Alternate a tall high-information band with a short calm one (trust strip, one-line quote, link row) to give the scroll a pulse and the eye recovery points. [S01,S04,S05,S06]

**Surface-weight is a second oscillation axis.** In an expressive or high-chroma register, oscillation runs on *two* axes, not one: the familiar **height** rhythm (tall info ↔ short calm) *and* a **surface-weight** rhythm (light/neutral surface ↔ saturated/inverted surface). A full-bleed saturated — or near-black — band reads as heavy *even when short*, so **never place two full-saturation full-bleed bands back-to-back**; intersperse a light/neutral band for recovery, exactly as you never stack two tall bands. In a brand-dominant register the color-field boundary *is* the section boundary, so color method and composition method fuse and this axis does the dividing work. [S06 · provisional]

### 2. Grid-break-as-narrowing

The intentional grid-break is a **narrowing** to a centered column for editorial, quote, or capture moments — **never** a widening of text to full-bleed. [S01,S04,S05,S06]

When a band narrows, its interior shifts from **grid/media logic to reading logic**: a constrained measure, a centered column, images interleaved *between* paragraphs rather than tiled. The narrowing therefore *selects a reading register that dictates the closer* (see the section-sequence law below). [S01,S04,S05]

In a high-chroma register the narrowing **may be doubly marked by surface inversion** — a dark or saturated full-bleed behind the narrowed column amplifies the reading-register switch. The narrowing stays load-bearing; the inversion is an optional register amplifier and must never be misread as a full-bleed *widening* break. [S06 · provisional]

### 3. Threaded proof

Thread proof throughout the page. Ratings, badges, before/after, pull-quotes recur at multiple depths — inside cards, in a dedicated reviews band, as standalone quotes — rather than clustering in a single testimonial block. [S01,S04,S05,S06]

In a colorful register, **proof rides the reserved accent**: threaded proof must be color-coded to the single reserved accent so "saturated = credible / commit" still reads — distribution across depths alone is insufficient on a loud ground. [S06 · provisional]

### 4. Section-opening grammar

A reusable **Section-Header organism** opens most bands: slotted `{ eyebrow? / heading / supporting? }` plus an optional trailing action, held to the narrow measure, slots toggled via hidden-layer flags and **never redrawn**. Every new topic gets a predictable entry point while each band's interior varies freely. [S01,S04,S05,S06]

---

## Postures — how the invariants are spent

The invariants hold everywhere; *how* a page deploys them is a register-selected posture.

**Order sections as a decision narrative.** Sequence by the user's journey — desire → justify → handle objections → next step — and keep the primary action reachable across the whole arc (e.g. a persistent commitment bar on long transactional pages). Section order is an argument, not a stack. [S01,S04,S05]

**Section order is breakpoint-invariant.** The decision-narrative order *is* the content model. Author the desktop frame as canonical and derive mobile **only** by column-collapse (N → N/2 → 1) and by drawer-izing filters behind a trigger plus a sticky commit bar — **never** by re-sequencing. Re-ordering per breakpoint silently forks the funnel. [S05 · provisional]

**Hero as a stage, not a container.** The hero is full-viewport but visually light — one image or moment, minimal copy — and hands proof immediately to a thin credibility strip right below it. Separate *impression* from *justification*. [S01,S04,S05]

**Hero copy lives in the image's negative space** — not a scrimmed overlay, not a split column. Compose the headline and single CTA into a pre-planned empty region of the image so the hero stays one authored image, a light stage, while still carrying copy. [S05 · provisional]

**Flip the split.** Use image+content splits as a repeatable unit and **alternate sides** on each consecutive use, guiding the eye diagonally down the page. [S01,S04,S05]

**Convince / convert purpose alternation** (a homepage law distinct from density oscillation). Tag each home band as **product-discovery** (rails, shoppable grids, bestsellers) or **trust/story** (USP ticker, value-props, reviews wall, journal, press), and refuse two same-*purpose* bands in a row. Weight-oscillation prevents *visual* fatigue; purpose-alternation prevents the "catalog dump" *semantic* failure that weight-oscillation alone cannot catch. [S05 · provisional]

**Closer must match the reading register the band selected.** Because grid-narrowing selects a register, the page's closer is dictated by type: editorial / long-form pages hold the narrow measure for the whole body and close on **lateral navigation** (related / next); commerce pages close on a **cross-sell rail**. Mixing closers — a buy-CTA on a story page, a dead-end on a product page — is the register error. [S01,S04,S05]

---

## Refinements — extending the vocabulary

Additions to the composition kit for specific registers. Each is single-sourced; treat as provisional until a second register confirms.

**New composition primitives (angled + stacked vocabulary).** Four section-level primitives beyond orthogonal grid splits, for playful / high-chroma registers: [S08 · provisional]

1. **Diagonal seam** — split a section with a slanted color-block edge and let the focal cluster straddle the slant. A first-class angled divide, distinct from a vertical gutter.
2. **Stacked-deck fan** — render a set of same-type peer cards as one overlapping, slightly-rotated object so an inherent *set* reads as a single tactile thing; keep rotations subtle and the grid inside each card clean.
3. **Tilted divider planes** — separate stacked sections with subtly skewed white sheets so the page reads as overlapping planes; a low-cost "playful" rhythm device that keeps each section's internal grid clean.
4. **Interstitial reset band** — a short full-bleed saturated band between two white sections acting as a palette-cleanser that re-sets vertical rhythm. Its structural role (the reset) is independent of its content — it may carry proof, but the role is the reset.

**Conversion-ribbon micro-section.** A thin band of 3–4 equal-width icon+title+subtitle value props, recurring under the hero and inside a PDP buybox — a tokenized, reusable proof/value primitive. [S06 · provisional]

---

> **Cross-references.** The band grammar here sits *above* the grid/layout token system (`07` — breakpoint-first tokenized grid) and *above* the storefront/page-skeleton libraries (which fix *which* sections, in what order, per page type). Responsive-component discipline (how a single component spans breakpoints) governs reflow *inside* a band and is a separate contract. This chapter governs the page-level composition; those chapters govern the parts it arranges.
