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
1. A **validated method library** (`method/`) — the explicit, written-down rules of
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
leaking between projects. `evidence/sources/` holds **abstracted method notes, never a mirror of
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

## How atelier is organized

The method is the tool; the sources are its evidence.

- **`GENERATE.md`** — the runnable brief→full-design playbook. **Start every project here.**
- **`method/`** — the consolidated, validation-tagged method (the tool itself):
  `00-decide.md` (the decision engine) → `01-color` · `02-typography` · `03-space-grid` ·
  `04-components` · `05-composition` → `anti-slop.md` (verify checklist) ·
  `page-skeletons.md` (section stacks per page type).
- **`evidence/`** — why the method is trustworthy: `VALIDATION.md` (confidence ledger:
  principle → confirming sources → tier), `sources/` (per-source method notes, anonymized),
  `PROCESS-NOTES.md` (analysis-integrity rules).
- **`decisions/open-questions.md`** — per-project taste/scope calls kept for human curation.
- **`corpus.md`** — inventory of the curated best-of sources distilled from.
- **`system/`** — per-project generated output.

The corpus is **curated best-of work**, not everything — distilling from an entire archive
regresses to the mean, the exact failure mode atelier escapes. Sources are **teachers, not
templates** (see the rule above): method only, never a mirror of any source's values or screens.

## Generation procedure

Follow **[`GENERATE.md`](./GENERATE.md)** — the full runnable playbook. In brief:

1. **Intake the brief** → industry, register/direction, brand inputs, references, breakpoints,
   deliverables.
2. **Decide** (`method/00-decide.md`) → name the register; run "what does color DO?" to pick the
   color posture(s)/tiers; pick the type strategy and density; choose the **one bold move**.
3. **Build the system bottom-up** → tokens color→type→space/grid (the `method/` chapters), then
   components. Bind to tokens, never raw values.
4. **Assemble pages** (`method/page-skeletons.md`) → instantiate the section stacks; apply the
   container contract; keep section order breakpoint-invariant.
5. **Brand book** → color/type systems, usage rules, logo direction + candidates.
6. **Verify** (`method/anti-slop.md`) → every frame traces to tokens + a validated principle,
   and the one bold move is nameable. If you can't name it, it's not finished.

## Honest limits (state these; do not oversell)

- **Logos** are the weakest link in AI generation. Deliver direction + candidates + usage
  rules. A client-ready final logotype needs human iteration.
- **One-shot** means a strong, coherent, on-brand *first draft* — not a zero-edit final.
  Promising zero-edit full designs is how you ship confident slop.
- **Motion/interaction/live logic** is a later phase. It layers onto an existing component
  system; it is not part of v1.
- **Corpus quality caps output quality.** Distill from the best work only.

## Status

**Method v1.** Corpus v1 complete (8 Figma sources); the method is consolidated into `method/`
and validated in `evidence/VALIDATION.md` (core principles load-bearing across 3–5 sources). Next:
an SEO/CRO research pass to harden the page skeletons, then end-to-end generation tests. See
`README.md` for the map and `GENERATE.md` for the runnable playbook.
