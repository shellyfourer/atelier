---
name: atelier
description: >-
  Generates intentional, non-generic frontend design — brand books, design
  systems, and full Figma designs — from a distilled corpus of real work. Use
  when the user wants to create a brand identity, design system, or complete
  website/app design from a brief (industry, direction, brand inputs, references)
  and explicitly wants to AVOID generic "AI slop" design. Produces Figma frames
  across breakpoints plus tokens, type/color systems, component specs, and
  build-ready notes. Logo output is direction + candidates, not final artwork.
  Motion/interaction patterns are a later phase layered onto the component system.
---

# atelier

Atelier turns a project brief into intentional design — not the averaged-from-the-internet
output that makes AI designs all look the same. It does this by designing from a **curated
corpus of real, strong work** and an **explicit decision framework**, rather than from
generic priors.

## The core principle

Generic AI design is the *average of the internet*. Atelier wins by refusing to average.
Every output traces to:
1. A **distilled principle library** (`principles/`) — the explicit, written-down rules of
   how good design decisions get made, including an anti-slop ruleset of what to never do.
2. A **design-system model** (`system/`) — real tokens, type/color systems, composition
   patterns, and component specs distilled from the corpus.
3. A **brief** — the specific project's industry, direction, brand inputs, and references.

If an output can't be traced to those three, it is slop and must be redone.

## The teacher/template rule (non-negotiable)

Source projects are **teachers, not templates.** Atelier studies real work to learn *method*
— how a tonal color system is constructed, how a type scale is proportioned, how semantic
roles map onto raw primitives, how a product page is composed — and then **discards the
specifics.** It never carries a source project's actual palette, fonts, copy, or layouts into
a new design.

- ✅ Keep: "build a semantic token layer over a tonal primitive layer (stepped ramp, each ramp
  anchored at its most representative tone), with contrast documented per step."
- ❌ Discard: any raw primitive value or literal hex (e.g. `accent-500: #<hex>`), the source's
  actual screens, fonts, copy, and any client-identifying specifics.

If atelier ever reproduces a source's concrete palette or layout, it has failed exactly the
way generic AI fails — by copying instead of understanding. This also keeps client work from
leaking between projects. `analysis/` holds **abstracted method and notes, never a mirror of
the source file.**

## The dependency stack (build and generate bottom-up)

```
  Motion / interaction / live logic   ← later phase; needs real components to animate
  Full page designs (Figma)           ← needs components + taste rules
  Components + variants + states      ← needs tokens + composition patterns
  Design system: tokens + brand       ← needs distilled principles
  The anti-slop principle library     ← the foundation; the actual moat
```

Never generate a layer before the layer beneath it is solid. A full page built before the
token system exists will regress to generic. This ordering is non-negotiable.

## What atelier produces

- **Brand book** — color system, type system, usage rules, clearspace, do/don't.
  Logo: strong **direction + candidate marks + usage rules**, treated as a starting point
  to iterate, NOT a one-shot final logotype. Be honest about this with the user.
- **Design system** — tokens (color roles, type scale, spacing rhythm, radii, elevation),
  component specs with variants and states, composition patterns.
- **Full Figma designs** — assembled section by section from the system, across desktop /
  tablet / mobile, using real tokens and components (not hardcoded values).
- **Specs** — structured notes that can feed downstream builds (WordPress/Shopify/React).

## How atelier is built (the corpus pipeline)

Atelier is only as good as what it distills from. The corpus is **curated best-of work**,
not everything — distilling from an entire archive regresses to the mean, which is the exact
failure mode we are escaping.

- `corpus.md` — inventory of the specific projects distilled from, and why each earned its place.
- `analysis/figma|shopify|wordpress/` — **method notes** per source: what the source teaches
  about *how* its system is built, in abstract terms. NOT a dump of the source's values or
  screens. A few reference screenshots are allowed for our own study; concrete tokens/layouts
  are not copied here.
  - **Figma** is highest fidelity: real variables/tokens, components, variants, grids,
    auto-layout rules (via Figma MCP: `get_variable_defs`, `get_design_context`,
    `get_metadata`, `get_screenshot`).
  - **Shopify** gives ecommerce composition + theme-settings schemas (design decisions
    exposed as settings) + live screenshots.
  - **WordPress/Elementor** gives layout trees (`_elementor_data`) + live screenshots;
    noisiest, extract carefully.
- `principles/` — the distilled human-curated rules. This is written collaboratively with
  the user and is where their taste gets encoded. **Curation is required**, not optional.
- `system/` — the generated design-system model built up from the principles + extraction.

## Generation procedure (once the foundation exists)

1. **Intake the brief** → industry, direction, brand inputs, color/reference material,
   target breakpoints, deliverables wanted.
2. **Derive the system** → from `principles/` + brief, produce the token set, type/color
   systems, and the component selection. Record in `system/`.
3. **Check against the anti-slop ruleset** before building anything. If the direction is
   drifting toward generic, fix it here, cheaply, before it's in pixels.
4. **Build in Figma bottom-up** → tokens/variables first, then components with variants,
   then assemble pages section by section, all breakpoints, bound to variables (never
   hardcoded values). Use the Figma MCP write path (load `figma-use` first).
5. **Produce the brand book** → color/type systems, usage rules, logo direction + candidates.
6. **Verify** → every frame traces to tokens + principles; present candidates, iterate.

## Honest limits (state these; do not oversell)

- **Logos** are the weakest link in AI generation. Deliver direction + candidates + usage
  rules. A client-ready final logotype needs human iteration.
- **One-shot** means a strong, coherent, on-brand *first draft* — not a zero-edit final.
  Promising zero-edit full designs is how you ship confident slop.
- **Motion/interaction/live logic** is a later phase. It layers onto an existing component
  system; it is not part of v1.
- **Corpus quality caps output quality.** Distill from the best work only.

## Status

v0 — scaffold. Phase 0 (corpus inventory) and Phase 1 (principle distillation) in progress.
See `README.md` for the phased build plan and current state.
