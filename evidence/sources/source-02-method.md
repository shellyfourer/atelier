# Source 02 — method notes (second source)

_Confidence: high (direct study of style-guide + token layer + a composed section)._

A real agency-built project system for a **product-configurator e-shop** (a taxonomy-driven
commerce project). Studied as a *teacher*: its value is that it uses a **different method** from
Source 01, which keeps atelier from overfitting to one "correct" way to build a system. No
specifics copied — method only.

**Portable vs discard:** Portable = the category-color method, the role-assigned multi-typeface
approach, the "one small accent in a monochrome field" composition move, the container/section
padding system, and the lesson that *old and new token layers coexist as a system evolves*.
Discard = the actual hues, the specific font choices, the product
taxonomy names, and every concrete px value.

## What makes this source a useful contrast to Source 01

| Dimension | Source 01 | Source 02 | Lesson for atelier |
|---|---|---|---|
| Color organization | Tonal ramps (25→950) per hue | **Category colors** — hues named by product taxonomy, base + "Light" pair | Both are valid. Ramps suit rich UI; category-color suits taxonomy-driven commerce. Pick by product, not dogma. |
| Color depth | 12-step ramps, per-step WCAG | Flat swatches, functional set (Primary/Success/Error/Hover) + category set | A leaner system is not a worse system — match depth to project scale. |
| Type | One family, size-stepped | **Multiple faces assigned by role** (heading / body / UI) | Role-based typeface pairing is a legitimate, expressive alternative to a single-family scale. |
| Maturity | Exhaustive formal library | Pragmatic hand-made guide **+ a newer semantic token layer underneath** | Real systems are layered in time — a hand guide on top, a migrating token system below. |

## Method principles learned here

- **Category-color method:** when a product domain has natural categories, encode the taxonomy
  *in the palette* — each category gets a base + a tint ("Light") pairing used for
  backgrounds/surfaces. Keep this separate from the small **functional** set (primary, success,
  error, hover). *Why:* color becomes a wayfinding system, not just decoration — users learn
  the categories by hue.
- **Role-assigned multi-typeface:** assign distinct typefaces to distinct *functions* (display
  vs body vs UI/links/buttons), each role carrying its own named size + weight. *Why:* a
  deliberate face-per-role pairing gives personality a single family can't, as long as roles
  are disciplined (one face per function, never mixed ad hoc).
- **One small accent in a monochrome field:** the composed hero is near-monochrome (black /
  white / gray) with a *single* small color pop (a yellow eyebrow pill). *Why:* this is the
  "one bold move" discipline in miniature — restraint everywhere, one intentional accent. Reads
  as confident, not timid; expensive, not busy.
- **Container/section spacing system:** spacing is tokenized at two altitudes — section-level
  padding (large: generous vertical breathing room) and container-level padding (tighter), plus
  named block widths (e.g. a 2-column block width). *Why:* page rhythm comes from a *system* of
  nested paddings, not ad-hoc margins; this is what makes whitespace feel composed.
- **Skeuomorphic button as signature detail:** buttons carry a layered effect (subtle drop +
  inner shadows + a hairline inner highlight) rather than a flat fill. *Why:* a single
  well-chosen tactile detail, applied consistently, lifts a whole system above flat-default
  genericness — but only if it's *one* detail used everywhere, not scattered effects.
- **Pill geometry as identity:** fully-rounded buttons (radius large enough to pill) paired
  with squared cards. *Why:* a consistent, slightly unexpected geometry contract is itself a
  design signature.
- **Systems coexist across time:** the hand-made style board uses one font set; the live
  components reference a newer semantic token layer with different fonts. *Why (meta-lesson):*
  atelier should expect to *migrate* a system, not assume one clean layer — and should read the
  live components as the truer current state, the style board as documentation that may lag.

## Anti-slop rules learned / reinforced here

- Don't default to tonal ramps for every project. A taxonomy-driven shop is better served by a
  **category-color** system; forcing ramps onto it is architecture for its own sake.
- Don't fear multiple typefaces — fear *undisciplined* ones. Role-assigned faces are strong;
  random mixing is slop.
- Monochrome + one accent beats a rainbow. More than one "look at me" color per view dilutes
  all of them.
- One tactile button treatment used everywhere > flat-default buttons OR scattered random
  effects. Pick the signature detail and commit.
- Trust the live components over the style-guide board when they disagree — a stale swatch sheet
  is documentation debt, not the system.
