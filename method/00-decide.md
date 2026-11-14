# The decision engine — pick register, color posture, type strategy, methods per project

> The first thing an operator reads. Before any token is minted or any frame is drawn, you
> choose *how* this project is built. atelier is not one system applied everywhere — it is a
> set of legitimate construction methods, and the craft is **choosing the right ones for this
> brief and stating why.** This chapter is the chooser. Everything downstream (color, type,
> space, components, pages) assumes you have run it.

---

## The one invariant you never choose: the spine

Method is plural; the spine is not. Whatever you decide below, every layer obeys the same
two-tier shape: **primitives carry raw value with zero intent → semantics carry role-named
meaning → components bind to semantics only, and nothing in the UI ever consumes a raw value
directly.** [S01,S03,S04,S05,S06] One mental model and one naming grammar run across color,
type, space, radius, and effects — name by *intent* at the semantic tier, by *value* at the
primitive tier, and never mix the conventions inside one tier. [S01,S03,S04] The decisions in
this chapter choose *which* methods sit on top of that spine; they never suspend it.

**Method pluralism is the governing stance.** There is no single correct system — each layer
below offers more than one legitimate method, and atelier picks per project, not by dogma.
[S01,S02,S03] The failure mode is picking a method reflexively; the discipline is choosing it
deliberately and recording the *why* in the brief.

---

## Step 0 — Read the register

Before choosing any individual method, name the **register**: what kind of product is this,
and what is its organizing idea? The register is the single input that drives most of the
choices below — it decides the color posture, how many token tiers you expose, the type
strategy, and whether whole method layers (storefront anatomy, data density, app shell) are
even in scope. [S08] Treat register selection as the literal first step; the rest of the engine
reads from it.

Working register vocabulary (extend as the corpus grows):

- **Expressive / formal library** — a wide, reusable palette and type system; range and craft
  are the point.
- **Taxonomy commerce** — a shop whose products fall into natural categories users navigate by.
- **Rich app / dashboard / admin** — stateful, deep component trees that re-theme by mode.
- **Brand-dominant storefront** — a single strong identity, not a taxonomy, is the organizing
  idea.
- **Marketing / brand site** — page-led persuasion with light application surface.

Most briefs are a register *plus modifiers* (e.g. "clinical B2B taxonomy commerce"). Name the
base register first, then the modifiers that tune chroma, tracking, and density.

---

## Step 1 — The lead diagnostic: what does color DO on this page?

Color posture is the highest-leverage decision and the fastest tell of a reflexive, templated
system. Do not reach for a default palette. Ask the diagnostic — **what job is color doing
here?** — and the answer selects the posture. [S01⟂S02⟂S03⟂S06]

| If color's job is… | Posture | What it means |
|---|---|---|
| **Expressive range / role-tinting across a wide system** | **(A) Tonal ramp** | Full stepped ramps per hue, per-step measured contrast. For expressive/formal libraries. [S01,S04,S07] |
| **Wayfinding — users learn the taxonomy by hue** | **(B) Category-color** | Each category a paired `{accent, tint}` kit, kept separate from a small functional set. Flat, lean, no deep ramps. [S02,S08] |
| **Theming neutral app chrome by mode** | **(C) Thin-semantic** | A small closed set of role tokens in fg/bg pairs, theme-switched by value-mode on one name. [S03,S05] |
| **Carrying the whole brand identity as surface** | **(D) Brand-dominant** | One saturated brand hue is the primary full-bleed surface; the color-field boundary *is* the section boundary. [S06 · provisional] |

**Postures compose as TIERS — not a forced single choice.** The register decides how many you
expose. [S05 · provisional] The clearest case: a rich app stacks **(C) thin-semantic on top of
an (A) ramp primitive library** — the ramp sits underneath, the UI touches only the thin role
set. [S05 · provisional] Pick posture(s) by register, not by reflex; whichever you stack, the
spine holds and nothing in UI binds a raw value.

**Two cross-cutting rules survive every posture:**

- **Color is a scarce signal.** Ration saturated hue so it always carries information — this
  holds on neutral *and* high-chroma grounds alike. [S02,S06] The failure is decorative color
  that means nothing.
- **Accessibility lives on the value.** Per-step measured contrast with an explicit pass/fail
  verdict is a property of the primitive, not an afterthought on the anchor. In postures that
  adopt a palette rather than author one, verification *relocates* to the semantic-selection
  tier but never disappears. [S01,S04]

*(Full posture detail, the `{accent, tint}` category kit, scope-theming, alpha-ramps,
ground-aware pairs, and the composition rules live in the Color chapter. This engine only picks
the posture.)*

---

## Step 2 — Type strategy: how many faces, and why

Choose the typeface strategy the same deliberate way, driven by register. [S01/S04 vs S02,S05]

- **(A) Single-family, size-stepped** — one face carries all roles via the size × weight
  matrix. Cohesive and systematic; the default for UI-heavy products. [S01,S04]
- **(B) Role-assigned multi-typeface** — assign *distinct faces to distinct functions*
  (display vs reading vs UI/action), each role carrying its own named size + weight. More
  personality; legitimate **only if disciplined** — one face per function, never mixed ad hoc.
  Good for editorial/brand-forward work. [S02,S08]
- **A third face is a register marker, not a decoration.** Where used, give it a *job* —
  e.g. a monospace reserved for a micro/status register (trust bars, counters, timestamps) that
  signals "system/technical/factual metadata," or a face reserved exclusively for
  interactive/navigational roles. Cap at ~3 faces, each owning a clear band; never let a
  special-purpose face leak into headings or reading copy. [S08 · provisional]

Either way, every style is a **composite token** (size + line-height + tracking + weight +
spacing bundled) drawn from a role × size matrix with an independent weight axis — that part is
invariant, not a choice. [S01,S03,S04,S05,S08]

One register-tuned knob to decide here, because it is a common slop tell: **letter-spacing is a
register knob, not a law.** Default tracking to 0 — including large display — for
neutral/clinical/technical/B2B brands; reserve negative-on-display for editorial/luxury. Never
ship a tracking value you can't justify from the register. [S05]

---

## Step 3 — Density: does this product carry a data-dense surface?

Decide whether the product needs a genuinely dense surface (tables, dashboards, data cards) at
all, and if so where the density line falls. [S03 · provisional] This is a scope call with
large downstream consequences, because density **inverts** the marketing-page levers: you can't
push things apart with whitespace or signal importance with scale, so hierarchy is *drawn*
(weight + color, hairlines, micro-spacing) rather than spaced. If the answer is yes, the
Data-density method and often a parallel compact library come into scope; if no, don't pay for
them.

---

## Step 4 — Gate the conditional method layers

Several whole method layers are **conditional** — in scope only for certain registers. Decide
each explicitly rather than building reflexively:

- **Storefront anatomy** (header/utility-cluster, mega-menu, product card, cart drawer vs page,
  store-info footer, promo system) — only when the product *is* a transactional storefront.
  [S04,S08]
- **Page-skeleton library** (per-type body stacks, buybox sub-skeleton) — paired with storefront
  anatomy; [S04,S08] a commerce register pulls in the four-track catalogue (full pages /
  overlays / state variants / responsive rule). [S08 · provisional]
- **Application shell & state-as-design** (persistent frame, parameterized nav rail,
  permission-matrix, typed empty/loading/error states) — only for multi-role apps. [S05,S06]
- **Responsive-component discipline** — treated as *universal*: every component in every project
  is authored across its breakpoints from their own frames, with reflow as an ordered set of
  authored decisions (column count, nav disclosure, icon priority, stacking order), never
  emergent flexbox. [S04,S05,S08] This one is on-always, not gated.

---

## Step 5 — Apply the two standing policies

These are resolved at the method level, not re-litigated per project — but you *apply* them
every engagement.

1. **Every design makes exactly one bold move.** [S05,S06] The method mandates a single,
   deliberate departure from safe defaults — one place the system takes a real aesthetic risk
   (a type move, a layout break, an unexpected color decision, a density choice). **Not zero**
   (reads as templated), **not many** (reads as noise). One, chosen intentionally and made to
   feel inevitable. A system with no point of view is slop no matter how clean its tokens are.
   *Where* the boldness is spent is a per-project human call — and in registers where the usual
   levers are unavailable (e.g. a dense dashboard has no hero scale or decorative color), it
   must be spent elsewhere: a signature data-viz treatment, a distinctive nav behavior, a
   disciplined unexpected accent.

2. **Defaults, then per-project tuning.** atelier ships proven default constants (base unit,
   step scale, tracking, line-height ratios, ramp lengths, elevation offsets) so every project
   starts from a sane, consistent foundation — then *tunes* them against the brand's specimens,
   with human sign-off on the feel. Never ship raw defaults unexamined (generic); never start
   from a blank numeric slate every time (slow and inconsistent). Defaults are the floor, not
   the answer.

---

## The decision checklist (run at project start)

Work it top to bottom. Each line produces a recorded answer in the brief — a method chosen with
a stated *why*, which is the whole point of the engine.

- [ ] **Register named?** Base register + modifiers (chroma, tracking, density) written down. [S08]
- [ ] **Product archetype gated?** Storefront / dashboard / marketing-site / app — decided, so the
      conditional layers (storefront anatomy, page skeletons, app shell) are scoped in or out. [S04,S05]
- [ ] **Color's job answered?** "What does color DO on this page?" → posture **A / B / C / D**
      selected, and **how many tiers** you expose (e.g. C-on-A for an app) stated. [S01⟂S02⟂S03⟂S06, S05]
- [ ] **Scarce-signal + accessibility confirmed?** Saturated hue rationed to carry information;
      per-step contrast verification located (authored, or relocated to semantic selection). [S02,S06,S01,S04]
- [ ] **Type strategy chosen?** Single-family (A) vs role-assigned multi-face (B), face count ≤3
      each with a job; composite-token matrix assumed. [S01,S04,S02,S08]
- [ ] **Letter-spacing register set?** Tracking default 0 for neutral/technical; negative-on-display
      only for editorial/luxury — and justified. [S05]
- [ ] **Density line decided?** Is there a data-dense surface, and where does the density line fall?
      Micro-spacing + compact library scoped accordingly. [S03]
- [ ] **Responsive-component discipline assumed on?** Three breakpoints from their own frames,
      reflow as ordered decisions. [S04,S05,S08]
- [ ] **One bold move located?** Exactly one deliberate risk, placed where it won't fight the
      funnel (or, at density, spent on a non-obvious lever). [S05,S06]
- [ ] **Defaults-then-tuning staged?** Starting from shipped defaults; tuning pass against the
      brand's specimens scheduled with human sign-off. [resolved policy]

When every box carries a recorded answer, the register is set and the downstream chapters have
their inputs. Build from there.
