# Typography method

Typography in this method is a **token system**, not a set of font declarations. Every text style
is a named composite that carries its own correct typesetting; roles come from a matrix; the
expressive dial (which faces, how tight the tracking) is register-tuned on top of an invariant
structure. This chapter states each law once, leading with the load-bearing invariants.

## The composite type token (invariant)

Model every text style as a **composite token**, never a bare font-size. Each step bundles, as one
addressable name: font-family, named weight/style, size, line-height, letter-spacing,
paragraph-spacing (and indent where it applies). Consumers reference one name and correct
typesetting travels with it — no style is ever reassembled by hand at the call site. [S01,S03,S04,S05,S08]

Keep the atomic sub-tokens (size, line-height, tracking) **independently addressable** underneath
the composite, for the edge cases that need to override one property without forking the style.
Name hierarchically so the composite and its parts are navigable (e.g.
`Typography/<Family>/<Step>/<Weight>` for the composite, `…/<step>-<property>` for the atoms). [S01,S04]

## Structure: a role × size matrix with an independent weight axis (invariant)

Roles come from a **matrix**, not from eyeballed one-offs. [S01,S04,S05,S08]

- **Role families** on one axis (~5): a display/attention tier, headline, title/subhead,
  body/reading, label/UI-caption.
- **Size steps** on the other axis (t-shirt steps XS…XL, extended as needed).
- **Weight as a third, independent axis** — emit one named style per (step × weight) cell. Offer
  the full weight ladder only where it is actually used (display/headline) and restrict body/label
  to a few weights to prevent token bloat. [S01,S04,S05,S08]
- **Overlap adjacent families' size ranges deliberately** so the same optical size can carry a
  different personality by role — a body-adjacent title versus a small headline at the same px. [S01,S04]

Two labellings of this same matrix are valid; pick per project: **role × t-shirt-size**, or
**semantic-ordinal** (H1/H2, Title 1/2, Body 1/2, Caption 1/2, Button). The ordinal labelling maps
more directly onto HTML/CMS heading semantics. [S05 · provisional]

Because roles are named by **intent, not resolved value**, two semantically different roles may
share identical family/size/weight and still remain **separate named tokens**. The model must
permit these intentional value-collisions, so visually-identical roles can diverge later per-context
or per-breakpoint without a rename. [S08 · provisional]

## Typeface strategy: single-family vs role-assigned (posture choice)

Choose the typeface strategy up front — this is a genuine method fork, both legs validated: [S01,S04 vs S02,S05]

- **(A) Single-family, size-stepped** — one typeface carries all roles via the size/weight matrix.
  Cohesive and systematic; the default for UI-heavy products. [S01,S04]
- **(B) Role-assigned multi-typeface** — assign *distinct faces to distinct functions*, each role
  carrying its own named size and weight. More personality; legitimate and strong **only if
  disciplined** — one face per function, never mixed ad hoc. Good for editorial/brand-forward work. [S02,S05]

Either way, each style is still a composite token and roles still come from the matrix.

**Provision two family slots from day one** — one display, one body — as tokens even if they
currently resolve to the same face. The display/body split is the single most common future change,
so pre-naming the slot makes it a value swap rather than a refactor. [S01,S04]

### The third face: a role-class signal, not just a size

Beyond display + body/UI, a **third face may be reserved for a specific role-class**, turning
typeface into a semantic axis of *function* (structure vs reading vs action) — separation achieved
without leaning on color. Two validated uses of the third slot: [S02,S08]

- **A monospace/system face reserved for a micro/status register** — trust bars, stock/status
  pills, timestamps, counters. The face signals "system / technical / factual metadata." Especially
  apt for clinical, B2B, and technical brands.
- **A face reserved for interactive/navigational roles** — links, buttons, footer utility — so the
  action role-class is legible by face.

Cap at **~3 faces**, each owning a clear band. Give the third face a defined job and never let it
leak into headings or reading copy.

### Interactive roles get their own size band

Tokenize action/navigation roles (buttons, links, footer utility) as **first-class type roles in a
mid size band** that may overlap the heading ramp *numerically* but stays a "control" token via a
separate family and medium weight. Size alone does not determine role — this is what blocks the slop
of styling a button as "a small bold heading." [S08 · provisional]

## Optical laws as functions, not hand-tuned per-step numbers

Encode the optical relationships as **functions of size**, so they stay consistent across the whole
ramp and survive a rescale.

- **Line-height is inversely proportional to size** — tight for display (~1.05–1.1×), loose for body
  (~1.3–1.45×) — and **snapped to a small rhythm grid** (multiples of 2/4) rather than arbitrary
  decimals. [S01,S04,S05]
  - *Refinement:* the real deciding variable is the **layout job**. Pin line-height to **1.0 for
    single-line, vertically-centered roles** (buttons, nav items, chips/pills, inline run-in labels,
    same-size bold "Title" labels) and keep **~1.5 only for flowing body**. At one shared base size,
    Button/Title/run-in use 1.0 while Body uses 1.5. [S05 · provisional]

- **Letter-spacing is a REGISTER KNOB, not a fixed law.** *(Revised.)* An earlier formulation stated
  tracking as a universal law — "strongly negative on large display, trending toward zero as size
  shrinks." That is now reframed: tracking's sign and magnitude are a **brand-register dial, not a
  constant.** **Default to 0** for neutral/clinical/technical/B2B brands, including large display;
  reserve negative-on-display for editorial/luxury registers. Never ship a tracking value you can't
  justify from the register. [S01,S04 (law) → S05 (reframed) · corroborated]

## Per-breakpoint composite swap

Responsiveness is handled by **swapping the whole composite per breakpoint**, not by fluid-scaling a
single property. Store per-breakpoint values (desktop / tablet / mobile) for size, line-height, and
tracking on each step so one name resizes correctly across devices. Align the breakpoint delta to
roughly **one size notch**. The composite stays the unit of change — a step resolves to a complete,
authored style at each tier rather than interpolating one axis. [S04,S05,S08]

## Centralization: two independent substrates

"Has named text styles" and "is variable-bound" are **separate questions.** A file can fully
centralize typography through named text styles while binding zero type to variables (reserving
variables for color and number). When reverse-engineering, audit **both** substrates; when building,
decide each on purpose. Variable-binding is not a prerequisite for centralization. [S05 · provisional]

---

## Premium craft signals (what makes type read as *authored*, not generated)

Type carries more of the "is this premium" verdict than any other layer. The rules above make the
scale *correct*; these make it read as *set by a typographer*.

- **Pick faces for brand character, and write the reason** — never reach for the model-default
  (Inter / Geist / Space Grotesk for sans; the usual monos) because it's safe. A popular face is
  still fine *with* a reason. The display/body pairing should feel chosen for *this* subject's world.
  [S02,S08 · 🟡 / anti-slop S09]
- **Tracking is a register knob, not a reflex.** Hold tracking at 0 across the whole scale for
  clinical / technical / B2B brands; reach for negative-on-large-display **only** for editorial /
  luxury, and justify it. Tracked-out ALL-CAPS everywhere is a generated tell, not sophistication.
  [S05 · 🟠]
- **Let line-height follow the role, not a constant multiplier.** Tight for display (~1.05–1.1),
  loose for body (~1.4–1.5), snapped to a rhythm grid — and **1.0 for single-line centered roles**
  (buttons, nav, chips, run-in labels). One ratio for everything is a dead giveaway. [S01,S04,S05 · 🟡]
- **Make tracking a proportional function of size** (large display tighter, small UI near-zero), so
  the ramp is self-consistent and extends cleanly — not hand-tuned per step. [S01 · 🟠]
- **Overlap size ranges deliberately** so the same optical size can carry a different personality by
  role (a 24px title vs a 24px small-headline differ in LH/weight/tracking, not px). This is what a
  linear h1…h6 ramp can't do. [S01,S08 · 🟡]
- **Give every type role a JOB; a third face must earn its place.** A mono reserved strictly for
  status/metadata/timestamps *signals* "system/factual"; an interactive-role face owns buttons/nav.
  Never add a third face as decoration or let it leak into headings/body. Interactive roles get
  their **own** named tokens — not "small bold headings." [S05,S08,S02 · 🟡]
- **Set headlines whole — never accent one word** (one word italic/colored/bold for pop is a
  generated tell). Let the whole type treatment carry the line; make the treatment itself the
  memorable thing, not a neutral delivery vehicle. [anti-slop S09]
- **Spend the eyebrow sparingly.** A tracked-caps kicker over *every* heading is template chrome;
  use it on a few genuine section openers and let other sections open on the heading alone. When an
  eyebrow just restates the heading, cut it. [anti-slop S09]
- **Document each family with a usage line + a live specimen**, so the right style is the easy style
  to reach for. An unlabeled token dump gets misused. [S01 · 🟠]
