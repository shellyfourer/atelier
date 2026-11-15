# Source 09 — aesthetic-slop research input (ruleset study)

- **Type:** A study input, **not** a Figma design corpus source like S01–S08, and not a client.
  It is research atelier read to sharpen its own anti-slop ruleset — treated as a **teacher**:
  we learned the method, wrote our own rules in our own words, and discarded the source's
  specific wording. Nothing was copied verbatim; no outside names or project specifics enter the
  repo (consistent with the teacher/template rule in `SKILL.md`).
- **Why it exists:** The first real end-to-end Figma build exposed that atelier's
  `method/anti-slop.md` covered **construction method only** — token architecture, ramp math,
  type-token completeness, component/variant structure, section stacks, grid math. It had **no
  visual / aesthetic anti-slop rules**: the *tells* that make an output read as machine-made even
  when its token architecture is flawless. The study material was read to close that gap.

## What was distilled into `method/anti-slop.md`

A new **"Visual / aesthetic anti-slop"** section, written in atelier's own voice, covering the
tell families the method was missing:

- **Visual/color tells** — generic blue-purple/neon gradients, glassmorphism-everywhere,
  glow-everywhere, the "AI default palette," too-many-colors, one accent on everything,
  background grid/dot patterns, dark-mode-for-no-reason, skeleton-as-product-shot, and the
  **sterile over-filtered default** (removing slop ≠ good design).
- **Layout/component tells** — the monotonous template stack (Hero + 3 cards / Hero + feature
  grid / fake stats), copy-paste identical feature cards, default bento grid, fake terminal
  window, uniform spacing, uniform section rhythm, alternating-background-only variation,
  "How It Works always 3 steps," "Trusted By" logo bar, "Most Popular" middle tier, 3 pricing
  columns, 4-column template footer.
- **Decoration tells** — generic AI icons (sparkle/star/magic/orb), the single-icon-library
  default look, colored left stripe on cards, **arrows (→/↗) on every button**, AI capsule
  badges, the **eyebrow label parked above the headline repeating what the headline says**,
  large-mono / wide-tracked-uppercase "AI typography," a typeface picked with no stated reason.
- **Copy tells (design-adjacent)** — the **em dash as an AI tell**, generic CTAs, AI buzzwords,
  fabricated stats / testimonials / trust claims, demo-without-a-product.
- **The purpose test + liveliness bar** — technique with no written purpose is slop; removing
  slop leaves a void that must be filled with real liveliness, not more bans. This operationalizes
  atelier's existing "one bold move" (Rule 0) rather than replacing it.

## How it maps to the Kristina build's real failures

The first Kristina Figma build passed the method-only anti-slop clean, yet carried three tells
these rules now catch:

- `Read article →` on card links → arrow-on-every-button.
- `· 8 min read ·` / `A · B · C` meta → middle-dot meta string.
- ALL-CAPS tracked eyebrow above every heading → eyebrow-above-headline + wide-tracked-uppercase.

We independently hit those in a real build; the study material named them crisply. That overlap
is why the new rules tagged `[S09]` in `anti-slop.md` are treated as **🟡 corroborated** where
they match a tell we actually produced (arrow, eyebrow, meta-dots, palette discipline) and
**🟠 provisional** otherwise — promoted as our own builds confirm them.

## Tier note

A ruleset study does **not** move the S01–S08 method confidence tiers.
