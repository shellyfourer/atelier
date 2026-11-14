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
├── principles/      # the distilled, human-curated anti-slop design principles
├── analysis/        # METHOD notes per source — what each teaches, abstracted
│   ├── figma/       # how its tokens/type/components/composition are *constructed*
│   ├── shopify/     # ecommerce composition method + settings-schema patterns
│   └── wordpress/   # layout-system method from Elementor builds
└── system/          # atelier's own synthesized design-system method
```

## Build plan (phased — proof before scale)

- **Phase 0 — Corpus inventory.** Hand-pick a small best-of set (start with strongest Figma
  files; add standout Shopify / WordPress projects). Recorded in `corpus.md`.
- **Phase 1 — Distill the foundation.** Extract tokens + composition patterns from the
  curated set; collaboratively write the principles + anti-slop ruleset into `principles/`.
  This is where taste gets encoded.
- **Phase 2 — Encode + prove.** Package Phase 1 as the working skill; test on one fake
  brief; judge whether output looks intentional or generic; fix principles before scaling.
- **Phase 3 — Scale.** More projects, Shopify/WP composition patterns, brand-book + logo-
  direction generation.
- **Phase 4 — Motion & live logic.** Distill animation/interaction patterns from real live
  sites and attach motion specs to the component library.

**Current status:** v0 scaffold. Starting Phase 0.

## Honest limits

- Logos: AI's weakest link — direction + candidates, not final artwork.
- "One-shot" = strong first draft, not zero-edit final.
- Output quality is capped by corpus quality — distill from the best work only.
