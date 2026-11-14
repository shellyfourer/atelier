# Corpus inventory

The curated best-of set atelier distills from. **Not everything — only the strongest work.**
Distilling from an entire archive regresses to the mean, which is the failure mode atelier
exists to escape. Every entry must justify why it earned its place.

## How to add an entry

For each project, record:
- **Source & type** — Figma file / Shopify store / WordPress site; link or path.
- **Why it's here** — what specifically is strong (its taste, not just that it exists).
- **What to distill** — the tokens / patterns / components worth extracting.
- **Extraction status** — not started / in progress / done → links to `extraction/...`.

---

## Figma

### 1. Source 01 — large formal design-system / token library
- **Source & type:** Figma — exhaustive multi-page token library + full page set (anonymized)
- **Why it's here:** Exemplar of a *rigorous, formal* token architecture: tonal color ramps
  with per-step contrast, composite type tokens, a uniform primitive→semantic model across all
  foundations, and a deep component library. Teaches disciplined system construction.
- **What to distill:** two-tier primitive/semantic model, Family→Ramp→Step color, composite
  type tokens, 4-based spacing + semantic gaps, component atom→organism architecture, page
  composition rhythm.
- **Extraction status:** done → analyzed by layer in [analysis/figma/](./analysis/figma/)

### 2. Source 02 — product-configurator e-shop style guide + components
- **Source & type:** Figma — lean agency-built real-project system (anonymized)
- **Why it's here:** A *contrasting* method to Source 01 — pragmatic agency-built real-project
  system. Teaches category-color organization, role-assigned multi-typeface, "one small accent
  in a monochrome field" composition, and a container/section spacing system. Its difference
  from Source 01 is the point: it proves method pluralism and stops atelier overfitting to one way.
- **What to distill:** category-color method, multi-typeface-by-role, signature-detail
  discipline (tactile button, pill geometry), section/container padding system,
  old-and-new-layers-coexist meta-lesson.
- **Extraction status:** done → [analysis/figma/source-02-method.md](./analysis/figma/source-02-method.md)

### 3. Source 03 — data-dense product dashboard on shadcn/ui + Tailwind
- **Source & type:** Figma — a real product dashboard built on a shadcn/Tailwind atom system (anonymized)
- **Why it's here:** A *third*, distinct method — and it covers dimensions the commerce/marketing
  sources never did: **data-density UI**, **app-shell/state/role-adaptation**, and the
  **thin-semantic (shadcn/Tailwind) token method** (theme-by-mode on one name). Also the bridge
  toward emitting real shadcn/React, not just Figma.
- **What to distill:** thin-semantic token architecture (fg/bg pairs, single radius knob, HSL
  channel-split rings, state-as-enum, own-the-code atoms), data-density principles (tabular
  figures, weight-not-size emphasis, hairline dividers over whitespace), app-shell method
  (one parameterized rail, first-class empty/loading/error states, role-driven nav + guards).
- **Extraction status:** done → [analysis/figma/source-03-method.md](./analysis/figma/source-03-method.md)

## Shopify

_none yet_

## WordPress

_none yet_
