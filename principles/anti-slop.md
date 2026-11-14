# atelier — anti-slop ruleset

> Concrete things to NEVER do. Each is a tell of generic / auto-generated design. Check every output against this before shipping.

## atelier — Anti-Slop Ruleset

Concrete things to never do. Deduped across all layers.

### Rule 0 — the one that overrides all others

**A design with no point of view is slop, no matter how clean its tokens are.** Every project
must make exactly one deliberate bold move (see Standing Policy in `methodology.md`). Zero bold
moves = templated and safe = slop. If you cannot name the one bold move in a finished design,
it is not finished.

### Architecture (all layers)
- **Never let a component or screen reference a raw primitive or literal value** (a hue step, a hex, a bare px). Always go through a semantic alias. Primitives bound directly into UI is the #1 tell of an immature system.
- **Never name a semantic token after its value** (`blue-button-color`). Name by role/intent (`text-primary`, `icon-error-on-solid`) so the value can change without the name lying.
- **Never invent tokens ad hoc per screen.** They must come from a fixed matrix so coverage is auditable and names predictable.
- **Never use one naming grammar everywhere.** Reserve abstract/t-shirt names for the semantic tier and literal values for primitives; don't mix conventions within a tier, and don't special-case one domain so it diverges from the others.
- **Never ship a foundation as a bare value dump.** Use explain-show-apply cards (definition + per-level live demo + usage note) so a token is adoptable from the doc alone.

### Color
- Don't force every ramp to anchor at a mid-step. A symmetric one-size ramp with the "main" color always in the middle is a generator default.
- Don't generate ramps as equal-lightness steps. Perceptual spacing is uneven on purpose — denser in the lights; linear interpolation betrays auto-generation.
- Never ship swatches without per-step contrast data and an explicit AA/AAA/fail verdict.
- Avoid one ramp per hue — a single "red" can't cover brick, rose, and torch; collapsing a family into one ramp is under-built.

### Typography
- Never define a style as a lone font-size. If it doesn't pin line-height, letter-spacing, weight, and paragraph-spacing, it's incomplete and will drift.
- Don't build a single flat linear ramp (h1…h6 / one 12→96 list). That collapses intent and magnitude into one axis.
- Don't hand-pick letter-spacing per step with arbitrary numbers; if tracking isn't a consistent function of size it can't extend cleanly.
- Don't use a constant line-height multiplier across the whole scale — display and body need opposite leading ratios.
- Don't leave line-heights as arbitrary decimals off a rhythm grid.
- Don't bake weight into the size step ("heading = always bold"); weight is an independent axis.
- Don't hardcode one font family everywhere; omitting the display/body split forecloses the likeliest future change.
- Don't ship size-only styles with no responsive behavior; one fixed px forces per-breakpoint overrides downstream.

### Space / Radius / Elevation
- Don't ship a single global border-radius. Radius scales with element size via per-component, size-keyed tokens.
- Don't fake elevation with one flat drop shadow. Real depth is two stacked layers (ambient + contact) scaling together across an ordered ramp.
- Don't invent shadows per-component or inline. Every surface maps to a named level tied to a component-role roster.
- Don't collapse spacing, padding, and fixed sizing into one token set — keep separate role-named axes even on a shared number line.
- Don't number-index primitives (`space-1`); name by literal value.
- Don't force every effect onto one ramp length — match resolution to the effect (fine for blur, few for inner shadow, categorical for focus rings).
- Don't skip explicit `*-none` tokens; "intentionally square/flush" is a deliberate choice.
- Don't hardcode effect colors into each shadow — centralize tint as a tiny set of alpha-only tokens.

### Components
- Don't build one monolithic Button/Input/Card with a sprawling variant matrix. Split into named siblings scoped to one job each.
- Don't fork a component per interaction state (`Button Hover` as its own component). States are variant axes of one set.
- Don't leave the base primitive anonymous or buried, or copy-paste it into each composite.
- Don't bake density/scale into every component as a variant when a parallel compact library expresses it once at the library level.
- Don't dump components into a flat namespace. Use path taxonomy, category prefixes, and functional pages.
- Don't ship components without a one-line usage description.
- Don't conflate an atom with its labeled molecule — keep the bare field separate from the field group.
- Don't wrap single-state elements in a variant set for symmetry.

### Page composition
- Don't stack two tall, dense sections consecutively; insert a short calm band between heavy ones.
- Don't give every section the same height or content weight — uniform bands signal a template.
- Don't repeat the same 50/50 split orientation twice in a row; flip sides each time.
- Don't let text run the full container width in reading-heavy sections; cap prose and headers to a readable measure.
- Don't break the grid by widening/going full-bleed for text — the intentional break is a narrowing to a centered column.
- Don't overload the hero with copy, multiple CTAs, and feature lists; keep it a light stage and move proof to the band below.
- Don't invent ad-hoc spacing or widths per section; resolve every value to the shared ramp.
- Don't cluster all social proof into one block; thread it through the whole scroll.
- Don't order sections arbitrarily; sequence as a decision narrative with the primary action reachable throughout.
- Don't mix multiple type families or leave headline tracking loose at large sizes.
- Don't drop a section in without a recognizable header grammar.
