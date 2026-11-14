# atelier — design-system construction methodology

> Synthesized by studying mature design systems for *method*. Portable principles only; no source-specific values, fonts, or layouts. This is how atelier builds a system from scratch for a new brand.

# atelier — Design-System Construction Methodology

A portable, bottom-up method for building a design system from scratch for any brand. These are the *rules of construction*, not any one brand's values. Work the layers in order — each rests on the one below it. Every layer shares one spine: **primitives carry value, semantics carry meaning, components bind meaning to a part, and nothing consumes a raw value directly.**

---

## Standing policy (decided — applies to every project)

These two calls are resolved at the skill level, not per project:

1. **Every design makes exactly one bold move.** The method *mandates* a single, deliberate
   departure from safe defaults per project — one place the system takes a real aesthetic
   risk (a type move, a layout break, an unexpected color decision, a density choice). Not
   zero (that reads as templated/safe). Not many (that reads as noise). **One**, chosen
   intentionally and made to feel inevitable. This is atelier's core anti-slop guarantee:
   a system with no point of view is slop no matter how clean its tokens are. *Where* to
   spend the boldness stays a per-project human call (see `_DECISIONS-NEEDED.md`), but
   *that* there is one is non-negotiable.

2. **Defaults, then per-project tuning.** Atelier ships with proven default constants (base
   unit, step scale, tracking, line-height ratios, ramp lengths, elevation offsets) so every
   project starts from a sane, consistent foundation — then *tunes* them against the specific
   brand's specimens, with human sign-off on the feel. Never ship raw defaults unexamined
   (that's generic); never start from a blank numeric slate every time (that's slow and
   inconsistent). Defaults are the floor, not the answer.

---

## 0. The spine (applies to every layer)

1. **Two hard tiers everywhere.** A *primitive* tier holds raw values with zero intent. A *semantic* tier holds role-named aliases that only ever point *at* primitives. Components consume semantics exclusively.
2. **One mental model across all domains.** Color, type, spacing, padding, sizing, radius, and effects all use the same primitive→semantic→component-scoped shape and the same naming grammar. Learn one foundation, you know them all.
3. **Name by intent at the semantic tier, by value at the primitive tier.** Words where a value is a reusable *decision* (`spacing-small`, `text-primary`); literal values where it's a raw *ingredient* (`spacing-4`, hue step `500`). Never mix the two conventions inside one tier.
4. **Document to teach, not to dump.** Every foundation ships as explain → show → apply: a plain-language definition, a live specimen of every level, and a per-level "where to use this" note, all on one shared column grid.
5. **Method pluralism — there is no single correct system.** Each layer below describes *more
   than one legitimate construction method*, and atelier **chooses the method per project**, not
   by dogma. (Learned by contrasting a large formal ramp-based library against a lean
   category-color agency project — both excellent, built oppositely.) Match the method to the
   product: a rich-UI app wants tonal ramps; a taxonomy-driven shop wants category colors. The
   failure is picking a method reflexively; the discipline is choosing it deliberately and
   stating *why* in the brief.
6. **Live components over style boards.** When a documented style sheet and the actual built
   components disagree, the components are the truer current state; the board is documentation
   that may lag. Read both, trust the build.

---

## 1. Color

**First, choose the color method (per spine rule 5):**
- **(A) Tonal-ramp system** — for rich, stateful UI (apps, dashboards, deep component trees).
  Full stepped ramps per hue. Detailed below; this is the default for product UI.
- **(B) Category-color system** — for taxonomy-driven commerce (a shop whose products fall into
  natural categories). Each category gets a **base + a light/tint pairing** used for
  surfaces/backgrounds, kept separate from a small **functional set** (primary, success, error,
  hover). Color becomes wayfinding — users learn categories by hue. Flat, lean, no deep ramps.
- Both still obey the spine: a semantic tier names roles; nothing in UI binds a raw value.

The rest of this section details method (A).

**Primitive ramps.** Organize as **Family → Ramp → Step**, three namespace levels. A family groups perceptually-adjacent ramps; allow **multiple ramps per hue family** (a warm variant, a muted variant, a tinted variant) rather than forcing one compromise ramp per hue.

- Use **one fixed step scale across every ramp**, denser at the light end (extra ultra-light steps below the mid, one ultra-dark above). Uniform steps make ramps interchangeable — swap the hue, keep the step.
- **Do not space steps by equal lightness deltas.** Perceptual spacing is intentionally uneven: finer in the highlights, where tints get used most and the eye discriminates best.
- **Anchor each ramp at its most representative tone and name the ramp after that anchor.** A pale tint and a near-black neutral do not carry their character at the same lightness; don't force a mid-step anchor on every ramp.
- **Record measured contrast + an explicit AA/AAA/fail verdict on *every step*** against a fixed reference, not just the anchor. Accessibility is a property of the value, so it lives on the primitive, turning the palette into a lookup table.

**Semantic aliases.** Name on a matrix of **Role × Prominence/Status × Context**:
- *Role* = the thing being painted (text, surface, icon, border).
- *Prominence* = primary / secondary / tertiary.
- *Status* = success / warning / error.
- *Context* = a suffix like `-on-solid` for tokens meant to sit on a filled color.

Deriving tokens from a fixed matrix makes coverage auditable and missing combinations obvious. Give each hue family an **editorial header** — a human title and a short note on its psychological role and intended use — separate from the swatch grid.

---

## 2. Typography

**First, choose the typeface strategy (per spine rule 5):**
- **(A) Single-family, size-stepped** — one typeface carries all roles via the size/weight
  matrix below. Cohesive, systematic; default for UI-heavy products.
- **(B) Role-assigned multi-typeface** — assign *distinct faces to distinct functions* (display
  vs body vs UI/links/buttons), each role carrying its own named size + weight. More
  personality; legitimate and strong **only if disciplined** — one face per function, never
  mixed ad hoc. Good for editorial/brand-forward work.
- Either way, each style is still a composite token (below) and roles still come from a matrix.

Model each style as a **composite token**, never a bare font-size. Every step bundles: font-family, named weight/style, size, line-height, letter-spacing, paragraph-spacing, (and indent). Consumers reference one name; correct typesetting travels with it.

**Structure as a matrix, plus an orthogonal weight axis:**
- **Role families** on one axis (~5: a display/attention tier, headline, title/subhead, body/reading, label/UI-caption).
- **T-shirt size steps** on the other (XS…XL, extend as needed).
- **Weight as a third, independent axis** — emit one named style per (step × weight) cell; offer the full weight ladder only where it's used (display/headline) and restrict body/label to a few weights to prevent bloat.

**Encode the optical laws as functions, not hand-tuned per-step numbers:**
- **Letter-spacing ≈ a fixed fraction of size** — strongly negative on large display, trending toward zero/positive as size shrinks.
- **Line-height inversely proportional to size** — tight for display (~1.05–1.1×), loose for body (~1.3–1.45×) — and **snapped to a small rhythm grid** (multiples of 2/4) rather than arbitrary decimals.
- **Overlap adjacent families' size ranges deliberately** so the same optical size can carry a different personality by role (a body-adjacent title vs. a small headline at the same px).

**Provision two family slots from day one** — one display, one body — as tokens even if they currently resolve to the same face; the display/body split is the most common future change. **Store per-breakpoint values** (desktop/tablet/mobile) for size, line-height, tracking on each step so one name resizes fluidly; align the breakpoint delta to roughly one size notch. Name hierarchically (`Typography/<Family>/<Step>/<step>-<property>`; composite as `<Family>/<Step>/<Weight>`) and keep atomic sub-tokens independently addressable for edge cases.

---

## 3. Space, Sizing, Radius, Elevation

**One base unit; three parallel axes.** Generate every dimension as an integer multiple of a single small base. Keep **spacing** (gaps between siblings), **padding** (inset within a container), and **size** (fixed element dimensions) as **separate role-named axes** even though they share one number line — so "all internal padding" and "all inter-element spacing" can be reasoned about, and diverge later, independently. **Name primitives by literal value** (`spacing-4`, `padding-20`), not an index — self-documenting, collision-free, insertable without renumbering.

**Three tiers:** value-named primitives → t-shirt semantic aliases (`spacing-small/large/2x-large`) → **component-scoped tokens** that bind one part to a primitive and isolate its quirks (`button-radius`, `input-field-width`). Always include explicit **`*-none`** tokens so "intentionally square/flush" is a deliberate choice.

**Radius scales with element size.** Reject a single global radius. Tiny chips get a hair of radius, buttons a little more, large blocks often zero. **Key the radius token's name to the component's size** so radius tracks element scale by rule.

**Elevation as a composite, role-mapped ramp (1…N):**
- Each level stacks **two shadows** — a soft ambient layer (large blur/spread, low alpha) plus a tight contact layer (small blur, higher alpha). One flat drop shadow is the tell of a fake.
- Both pull tint from a **tiny set of alpha-only color tokens**, so the whole system re-tints (or dark-mode-inverts) from two values.
- **Geometry scales monotonically** — y-offset, blur, spread grow together as level rises, keeping the ramp perceptually ordered.
- **Bind each level to a documented component/state roster** (resting cards, buttons, menus, dropdowns, modals) so z-depth is a system-wide contract, not an eyeball.

**Each effect gets its own scale shape.** Match ramp resolution to expressive need: fine-grained for blur, few steps for inner shadow, **categorical semantic variants** (not sizes) for focus rings. Don't force one ramp length onto effects that don't want it.

---

## 4. Components

- **Name explicit base atoms** and tag them (`Cell (Base)`). Higher structures *instance* the base; one edit propagates. Never copy-paste a primitive into each composite.
- **Encode the composition ladder in the name.** Atom keeps the bare noun (`Field`); its molecule appends a role word (`Field group`) bundling the atom with its satellites (label, helper, affordances). Altitude is readable from the name; the group is the intended unit of reuse.
- **Prefer a family of specialized siblings over one mega-component.** A button "need" is a family — generic action, icon-only, filter, floating-action, selectable — each scoped to one job with small, orthogonal axes (size × state), not one set with an exploding matrix.
- **Variant sets only where a real axis exists.** Interactive controls and multi-kind cells get sets; a static card or a lone glyph stays a plain component. Don't wrap single-state elements in a set for symmetry.
- **States and kinds are variant axes, never forked copies.** One set holds default/hover/disabled/error so every state shares geometry and tokens and the full inventory is inspectable in one place.
- **Hoist density/scale to the library level.** Ship parallel libraries (full + compact) with *identical* component names rather than adding a density variant to every component — swap the subscribed library to rescale a whole project losslessly.
- **Strict path taxonomy + functional pages.** `design_system/<library>/components/<Name>`, with category prefixes for catalog-like items; group editor pages by UI function with a stable marker.
- **One-line usage description on every component** — what it is and when to use it — so the library is a self-describing API.

---

## 5. Page composition

- **Band chassis.** Build pages from a fixed vocabulary of full-width horizontal sections, each owning one uniform outer margin and one top inner-padding; let **content set height**, not a fixed slot. Shared chassis is the biggest driver of "composed, not templated."
- **Oscillate density.** Never stack two tall, heavy sections back-to-back. Alternate a tall high-information band with a short calm one (trust strip, one-line quote, link row) to give the scroll a pulse and the eye recovery points.
- **Hero as a stage, not a container.** Full-viewport but visually light (one image/moment, minimal copy); hand proof immediately to a thin credibility strip right below. Separate *impression* from *justification*.
- **Two nested width systems.** A wide container for grids/media; a deliberately **narrower measure** for reading-dominant content. **The intentional grid-break is a *narrowing*** to a centered column for editorial/quote/capture moments — never a widening of text to full-bleed. Cap prose and section headers to a readable measure even inside full-width bands.
- **Flip the 50/50 split.** Use image+content splits as a repeatable unit and **alternate sides** on each consecutive use, guiding the eye diagonally down the page.
- **One token ramp drives everything.** Every gap, padding, and width resolves to the shared scale; variety lives in composition and content, not ad-hoc pixels. That constraint is what reads as one authoring hand.
- **Thread proof throughout.** Ratings, badges, before/after, pull-quotes recur at multiple depths (in cards, a reviews band, standalone quotes) rather than clustering in one testimonial block.
- **Order sections as a decision narrative.** Sequence by the user's journey — desire → justify → handle objections → next step — and keep the primary action reachable across the arc (e.g. a persistent commitment bar on long transactional pages). Section order is an argument, not a stack.
- **Consistent section-opening grammar.** A reusable header unit (optional badge + heading + support line, held to the narrow measure) opens most bands so every new topic has a predictable entry point while its interior varies freely.

