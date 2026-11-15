# atelier

**A tool for making web development high-quality and easier, by designing from validated
method instead of generic defaults.**

Most AI-generated (and a lot of human-generated) web design looks the same because it's built
from the *average of the internet*. atelier refuses to average. It takes a brief and produces
**intentional, non-generic design**: a brand book, a design system, and full Figma pages across
breakpoints, by following a method distilled from real, strong work and **validated across many
independent sources**.

It works two ways, equally:

- **As a Claude skill:** an agent runs `atelier` to go from *"build me a store for X"* to a
  complete design system + pages, following [`GENERATE.md`](./GENERATE.md).
- **As a human handbook:** your team reads the [`method/`](./method/) chapters and
  [`page-skeletons`](./method/page-skeletons.md) as a design-system playbook and quality checklist
  while building by hand.

---

## What makes it different

1. **Method, not templates.** atelier learns *how* good design systems are constructed and
   discards the specifics. It never reproduces a source's palette, fonts, or layouts. It carries
   recipes, not dishes. (See the teacher/template rule in [`SKILL.md`](./SKILL.md).)
2. **Validated, not asserted.** Every principle carries a confidence tier based on how many
   independent sources confirm it. See the ledger in [`evidence/VALIDATION.md`](./evidence/VALIDATION.md).
   Load-bearing principles are confirmed by 3-5 sources; provisional ones are flagged honestly.
3. **One deliberate bold move, always.** A design with no point of view is slop no matter how
   clean its tokens are. atelier mandates exactly one signature risk per project, its core
   anti-slop guarantee.
4. **Conversion- and structure-aware pages.** The [page-skeleton library](./method/page-skeletons.md)
   encodes what sections each page type should have, in what order, and why, built toward
   converting, well-structured, SEO-sound first drafts. Includes storefront, editorial, blog,
   personal brand, and application page types.

---

## How to use it

**Start here:** [`GENERATE.md`](./GENERATE.md), the runnable brief-to-full-design playbook.

The loop, in one glance:

```
brief -> DECIDE (method/00-decide.md)
      -> BRAND BOOK  <-- hard gate: create it, agree it, sign off (brandbook/)
      -> design system (tokens -> components) -> assemble pages (method/page-skeletons.md)
      -> build in Figma (3 breakpoints) -> VERIFY (method/anti-slop.md)
```

**The brand book is the gate.** If the client has no brand book, the agent creates one, asking
the client questions first (logo? colors? fonts?), generating what's missing (a wordmark when
there's no logo), and rendering a **PDF**. Nothing downstream begins until it's signed off. See
the [`brandbook/`](./brandbook/) skill.

---

## Repository map

```
atelier/
├── GENERATE.md            # the runnable brief-to-full-design playbook (start here)
├── SKILL.md               #   the skill's operating contract
│
├── brandbook/             # THE GATE: a standalone skill that creates the brand book (PDF)
│   ├── SKILL.md           #   intake -> generate (wordmark if no logo) -> PDF -> sign-off gate
│   ├── intake/questions.md#   the client questionnaire (ask before generating)
│   └── template/          #   HTML/CSS -> PDF chassis, page specs, brand-tokens schema
│
├── method/                # THE METHOD: the tool itself (clean, deduped, validation-tagged)
│   ├── 00-decide.md       #   the decision engine: register, color posture, type, density
│   ├── 01-color.md        #   four color postures (A/B/C/D) + the two-tier spine
│   ├── 02-typography.md   #   composite type tokens, role×size, typeface strategy
│   ├── 03-space-grid.md   #   spacing/radius/elevation + the tokenized grid system
│   ├── 04-components.md   #   atom->organism, states, app-shell, data-density
│   ├── 05-composition.md  #   band chassis, density oscillation, the composition laws
│   ├── anti-slop.md       #   the never-do-this ruleset (run as a verify checklist)
│   └── page-skeletons.md  #   canonical section stacks per page type (15 page types)
│
├── evidence/              # THE PROOF: why the method is trustworthy
│   ├── VALIDATION.md      #   confidence ledger (principle -> confirming sources -> tier)
│   ├── sources/           #   per-source method notes (anonymized provenance)
│   └── PROCESS-NOTES.md   #   analysis-integrity rules (how void runs are handled)
│
├── decisions/
│   └── open-questions.md  #   per-project taste/scope calls kept for human curation
│
├── corpus.md              #   inventory of the sources distilled from
└── system/                #   per-project generated output lives here
```

**Reading order:** `GENERATE.md` to use it. `method/00-decide.md` for how choices are made.
The topic chapters for depth. `evidence/VALIDATION.md` to see how strongly each claim is backed.

---

## Status

**Corpus v1 complete, method extended to cover personal brand / editorial blog register.**

8 Figma sources span a formal token library, a commerce configurator, a shadcn dashboard, a warm
storefront, an app-leaning store, a brand-dominant storefront, a reproducibility twin, and a
high-chroma catalog. The spine, method pluralism, four color postures, composite type tokens,
atom-to-organism, the grid system, and the four composition laws are **load-bearing** (3-5
independent sources each).

The page-skeleton library now covers 15 page types including personal brand home and about pages.
The anti-slop checklist includes a dedicated editorial/personal-blog section covering photography,
hero text legibility, register mapping, and signature identity component requirements, confirmed
by a real end-to-end build.

**Next:** a dedicated SEO/AEO/CRO research pass to harden the page skeletons for conversion,
semantic HTML, structured data, and AI-crawl depth; then end-to-end generation tests across
multiple register types.

---

## Honest limits

- **Logos** are AI's weakest link. atelier delivers direction + candidates + usage rules, not a
  final logotype.
- **"One-shot" means a strong first draft**, not a zero-edit final. Promising zero-edit full
  designs is how you ship confident slop.
- **Motion / interaction** is a later phase, layered onto the component system.
- **Output quality is capped by the brief.** How well the register and direction are named up
  front determines how non-generic the result can be.
