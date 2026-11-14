# atelier

A Claude skill that generates **intentional, non-generic frontend design** — brand books,
design systems, and full Figma designs — from a distilled corpus of real work.

Most AI design looks the same because models design from the *average of the internet*.
Atelier refuses to average: every output traces back to a curated corpus of strong real
work and an explicit, written-down design decision framework (including an anti-slop
ruleset). The result is design that looks *intentional*, not templated.

**Source projects are teachers, not templates.** Atelier studies real work to learn *how good
design systems are built* — then discards the specifics. It never copies a source's palette,
fonts, or layouts into a new design. It learns method; it produces a system. (See the
teacher/template rule in `SKILL.md`.)

## What it produces

- **Brand book** — color system, type system, usage rules; logo *direction + candidates*
  (not one-shot final artwork).
- **Design system** — tokens, type/color systems, component specs with variants and states.
- **Full Figma designs** — assembled from the system, across desktop / tablet / mobile.
- **Build-ready specs** — structured notes that can feed WordPress / Shopify / React builds.

See [`SKILL.md`](./SKILL.md) for the full operating contract.

## How it works: the dependency stack

Built and generated **bottom-up** — never a layer before the one beneath it is solid:

```
  Motion / interaction / live logic   ← later phase
  Full page designs (Figma)
  Components + variants + states
  Design system: tokens + brand
  The anti-slop principle library     ← the foundation, the moat
```

## Repository layout

```
atelier/
├── SKILL.md         # the skill's operating contract (its brain)
├── README.md        # this file
├── corpus.md        # inventory of projects distilled from, and why each qualifies
├── principles/      # the distilled, human-curated design knowledge
│   ├── methodology.md       # bottom-up construction method (color→type→…→composition)
│   ├── anti-slop.md         # concrete "never do this" ruleset
│   ├── page-skeletons.md    # canonical section structure per page type (conversion/SEO/structure)
│   ├── VALIDATION.md        # confidence ledger — how many sources confirm each principle
│   └── _DECISIONS-NEEDED.md # taste/scope calls kept for collaborative curation
├── analysis/        # METHOD notes per source — what each teaches, abstracted
│   ├── figma/       # how its tokens/type/components/composition are *constructed*
│   ├── shopify/     # ecommerce composition method + settings-schema patterns
│   └── wordpress/   # layout-system method from Elementor builds
└── system/          # atelier's own synthesized design-system method
```

## Build plan (depth over speed — results take time)

This is built to be *worth using*, not shipped fast. Every principle is validated across many
sources; confirmation is a first-class output tracked in `principles/VALIDATION.md`. Variety of
sources is the goal — different registers, industries, and platforms make the findings stronger.

- **Phase 0 — Corpus inventory.** Curate a best-of set across registers and platforms. `corpus.md`.
- **Phase 1 — Distill + validate the foundation (ongoing).** Study each source for METHOD,
  separating CONFIRMS (strengthens the ledger) from NEW (extends the method). Write principles,
  anti-slop rules, and page skeletons. Keep going — more sources = stronger validation.
- **Phase 1b — SEO / AEO / CRO research pass (planned).** Harden `page-skeletons.md` with
  dedicated research: conversion funnels, semantic HTML, heading hierarchy, structured data
  (schema.org), and content depth for AI crawlers. Until done, the skeletons' conversion/SEO
  notes are provisional.
- **Phase 2 — Encode + prove.** Package the principles as the working skill; generate from a
  brief; judge intentional vs generic; fix before scaling.
- **Phase 3 — Scale deliverables.** Brand-book + logo-direction generation; more sources.
- **Phase 4 — Motion & live logic.** Distill animation/interaction from real live sites.

**Current status:** Phase 1 ongoing — 4 sources integrated, validation ledger live, page-skeleton
library started. More sources queued; SEO/CRO research pass to follow.

## Honest limits

- Logos: AI's weakest link — direction + candidates, not final artwork.
- "One-shot" = strong first draft, not zero-edit final.
- Output quality is capped by corpus quality — distill from the best work only.
