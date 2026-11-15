# Color method — four postures, the two-tier spine, and all refinements

> Portable construction method, not any one brand's palette. No client names, no hex, no
> fonts. Validation tags like `[S01,S04,S07]` cite the sources in `evidence/VALIDATION.md`
> that confirm each principle; `[S0x · provisional]` marks a principle seen in a single source.

Color is built in two movements. First the **spine** — an invariant that holds no matter what
the brand is. Then a **posture** — one of four register-selected ways to spend hue on top of
that spine. The spine is non-negotiable; the posture is a deliberate, stated choice. Everything
after is refinement that attaches to one posture or cuts across all of them.

---

## 1. The two-tier spine (invariant)

Every color system, in every posture, rests on the same two tiers. This never changes.

- **Two hard tiers.** A **primitive** tier holds raw color values with zero intent. A
  **semantic** tier holds role-named aliases that only ever point *at* primitives. **UI binds
  to semantics exclusively — nothing in the interface ever consumes a raw value directly.**
  [S01,S03,S04,S05,S06]
- **Name by intent at the semantic tier, by value at the primitive tier.** Primitives read as
  ingredients (a hue step like `500`); semantics read as decisions (a role like `text-primary`).
  Never mix the two conventions inside one tier. [S01,S03,S04]
- **The tier is encoded in the name so a primitive can't be grabbed by accident.** Primitives
  carry a **library/family prefix** (`library/family/step`); semantics are **bare role names**.
  [S05 · provisional]
- **The semantic/alias layer always resolves to primitive steps — never to loose hexes.**
  Theming, mode-switching, and re-skinning all happen by re-pointing semantics at primitives.
  [S01,S03,S04,S05]
- **Document to teach: explain → show → apply.** A plain-language role definition, a live
  specimen of every token, and a per-token "where to use this" note. [S01,S04]
- **Color is a scarce signal — ration saturated hue.** Holds on a neutral ground *and* on a
  high-chroma ground; only the *amount* and *placement* of hue change by posture, never the
  discipline of spending it deliberately. [S02,S06]

---

## 2. Posture is register-selected (the method-pluralism rule)

There is **no single correct color system.** The posture is chosen per project from the
product's register, and the choice is stated in the brief — picking a posture reflexively is the
failure. Four postures are now evidenced across the corpus. [S01⟂S02⟂S03⟂S06]

- **(A) Tonal-ramp** — expressive/formal libraries with a wide chromatic range; full stepped
  ramps per hue with per-step contrast.
- **(B) Category-color** — taxonomy-driven commerce; color becomes wayfinding, users learn
  categories by hue.
- **(C) Thin-semantic** — rich, stateful apps/dashboards that re-theme; a small closed role set
  theme-switched by mode.
- **(D) Brand-dominant** — brand-led storefronts where one saturated identity is the organizing
  idea; the brand hue *is* the primary surface.

Each posture is detailed below. All four obey the spine without exception.

---

## 3. Posture A — tonal ramp (expressive / formal libraries)

For expressive or formal libraries with a wide chromatic range. The craft budget goes into
authoring full, measured ramps.

**Primitive ramps — organize as Family → Ramp → Step** (three namespace levels). A family groups
perceptually-adjacent ramps. [S01,S04,S07]

- **Allow multiple named sibling ramps per hue family** — a warm variant, a muted variant, a
  tinted variant — rather than forcing one compromise ramp per hue. [S01,S04]
- **One fixed step scale shared across every ramp**, denser at the light end (extra ultra-light
  steps below the mid, one ultra-dark above). Uniform steps make ramps interchangeable: swap the
  hue, keep the step. [S01,S04,S07]
- **Do not space steps by equal lightness deltas.** Perceptual spacing is intentionally uneven —
  finer in the highlights, where tints get used most and the eye discriminates best. [S01,S04]
- **Anchor each ramp at its most representative tone and name the ramp after that anchor.** A
  pale tint and a near-black neutral don't carry their character at the same lightness; don't
  force a mid-step anchor on every ramp. [S01,S04]

**Semantic aliases — name on a matrix of Role × Prominence/Status × Context.** [S01]
- *Role* = the thing painted (text, surface, icon, border).
- *Prominence* = primary / secondary / tertiary.
- *Status* = success / warning / error.
- *Context* = a suffix like `-on-solid` for tokens meant to sit on a filled color.

Deriving tokens from a fixed matrix makes coverage auditable and missing combinations obvious.
Give each hue family an **editorial header** — a human title and a short note on its
psychological role and intended use — kept separate from the swatch grid. [S01]

**Accessibility lives on the primitive here.** Record **measured contrast + an explicit
AA/AAA/fail verdict on every step** against a fixed reference, not just the anchor — turning the
palette into a lookup table. (In other postures this verification relocates; see §8.) [S01,S04]

**Warm-register tuning** (one evidenced instance): drift the dark end warm and draw surfaces
from the lightest ramp steps. [S04 · provisional]

---

## 4. Posture B — category color (taxonomy-driven commerce)

For a shop whose products fall into natural categories. Color becomes wayfinding — flat and
lean, no deep ramps. This is **one option, not a storefront default** (a brand-dominant shop
contra-indicates it as the reflex choice). [S02,S08]

- **Mint each category as a paired {accent, tint} two-token kit** — a saturated accent *and* a
  matched pale tint of the same hue — not a lone hue. Wire the **accent to interactive/active
  surfaces** (nav pill, price tag, add-to-cart, badge chips, favorite affordance) and the
  **tint to calm backing surfaces** (active-pill background, card wash, section band). One
  binding themes both foreground and background, so the flat method becomes a mini-ramp per
  category and the tint never drifts off-hue from its accent. [S08 · provisional]
- **Keep the category palette separate from a small functional set** (primary, success, error,
  hover). Categories carry taxonomy; the functional set carries status. [S02]
- **Accent is a scope function with an explicit brand fallback — not hardcoded per page.** The
  contract: **chrome = brand constant** (header, footer, persistent/newsletter bands never
  swap); **content region = category variable** (a category in scope re-themes every accent
  surface to its pair); **default = brand primary** when no single category is in scope ('All'
  view, global filter sheet). State the fallback explicitly so un-categorized surfaces are never
  left to guesswork. [S08 · provisional]
- **Bind accent at the smallest meaningful unit; let a page-scope override collapse it** — one
  mechanism doing two legibility jobs by composition density:
  - **Mixed list** (aggregated/home rail): bind the accent at the **item/card level** so several
    category pairs coexist in one viewport and the palette self-sorts into an at-a-glance
    **taxonomy legend**.
  - **Filtered page** (single category in scope): a **page-scope override collapses to a single
    theme**. [S08 · provisional]

---

## 5. Posture C — thin semantic (rich apps / dashboards)

For rich, stateful *application* UI (dashboards, admin consoles, deep component trees that
re-theme). A full primitive ramp sits underneath, but the *only* thing components ever touch is a
**small, closed role set** — the spine's two-tier rule taken to its minimal top layer: not
posture A's exhaustive Role×Prominence×Context matrix, but a deliberately tiny role set.
[S03,S05]

- **Role tokens ship in foreground/background pairs.** Surface pairs (background, card, popover),
  an action pair (primary + its foreground), quiet pairs (muted, accent + foregrounds), a status
  pair (destructive + ring), and chrome roles (border, input, ring). Every "on-X" foreground
  ships with its "X" background so contrast travels with the token. [S03,S04,S05]
- **Theme by value-mode on one name.** Light and dark are twins sharing identical role names;
  only the resolved value changes per mode. Adding a theme = adding a **value column**, never a
  component variant or a `dark-`-prefixed palette. (Contrast posture A, where dark mode means
  re-selecting ramp steps per element.) [S03,S05]
- **Adopt, don't author, the primitive tier.** In the app register the craft budget moves off
  ramp-authoring onto semantic selection + mode mapping — adopt a utility palette wholesale and
  never expose it to UI. [S05 · provisional]
- **Channel-split colors: store base colors as bare channels, apply alpha at use-site,** so one
  token yields solid fills, borders, *and* translucent rings/overlays — no new token per opacity.
  [S03,S05]
- **State-as-enum wired to tokens, ring-as-shadow.** Interactive atoms carry
  Default/Focus/Invalid/Disabled as variant axes; focus pulls the ring token, invalid pulls
  destructive, disabled pulls muted; focus/validation render as a **spread box-shadow** in the
  ring color so focus never changes the box model (no 1px reflow). [S03 · provisional]
- **Own-the-atom contract.** Atoms are source you paste and bind to your tokens, not a versioned
  black-box dependency. Portability is the *naming contract* (primary, foreground, ring, radius) —
  any project honoring the names gets consistent, re-skinnable components with no upgrade lock-in.
  [S05 · provisional]

### Scaling the thin layer — by sub-namespace, not by widening the flat list
When the role set must grow, add **bounded, closed sub-families**, each rethemeable
independently — never a longer flat list: [S05 · provisional]
- a fixed categorical **chart set** (`chart-1..N`) for data-viz series;
- a mirrored **app-shell / sidebar sub-theme** (its own foreground/primary/accent/border/ring)
  so chrome rethemes independently of content.

### Extended status axis
Promote the **full status quartet — info / success / warning / destructive(error)** — into the
semantic role set as first-class tokens (not a lone `destructive`), each a direct primitive
selection. [S05 · provisional]

### Alpha as an orthogonal token shape
- **Alpha-ramp family:** step ONE base color through fixed **opacity** levels
  (lighter/light/main/dark/darker) — orthogonal to the lightness ramp. Use for overlays, scrims,
  hovers, and disabled states, where a translucent wash over an arbitrary background beats a
  solid lightness step. [S05 · provisional]
- **Translucent-border convention:** in a mode-switched system, define border/divider roles as
  **foreground-at-low-alpha**, not an opaque neutral step. One alpha-on-ink border reads
  correctly over any surface shade in either mode — no per-surface opaque border value needed.
  [S05 · provisional]

---

## 6. Posture D — brand-dominant (brand-led storefronts)

One saturated **brand hue is the primary surface**, deployed as large full-bleed color
**blocks**, not a thin ribbon of trim. Choose this register when a single strong brand
identity — not a product taxonomy, not neutral app chrome — is the organizing idea. [S06 ·
provisional]

- **Tiny palette, by design:** brand-hue + near-black (photographic/product panels) + paper-white
  (content) + **ONE** high-contrast accent chosen for action. Adding more chroma collapses the
  hierarchy that makes the single accent read as "action." [S06 · provisional]
- **Color-blocking is the section rhythm — the color-field boundary IS the section boundary.** In
  this posture color method and page-composition method FUSE; alternating fields do the
  dividing/whitespace work. [S06 · provisional]
- **Dual-ground foreground PAIRS are first-class peers.** Author ground-aware semantic pairs
  (text-on-light / text-on-brand, accent-on-light / accent-on-brand) up front. The
  on-brand/on-dark column is a **peer** of the on-light column, not a `-on-solid` edge suffix,
  because inverse fields cover roughly half the page. [S06 · provisional]
- **Accent chosen for chromatic distance from the brand hue.** When the field is itself an
  intense hue, the action color must be near-complementary / high-contrast to *escape* the field.
  The selection rule shifts from "the lone saturated thing" (neutral ground) to "separation from
  the brand hue." [S06 · provisional]

The spine and "color is a scarce signal" hold unchanged here — only the *spending* of hue
changes (dominant structure vs. trim).

---

## 7. Postures compose as TIERS, not a forced single choice

The four postures are **composable tiers**, selected by register — not a mutually-exclusive menu.
The register decides how many tiers you expose. [S05 · provisional]

- **Taxonomy storefront →** category-color (B): base + per-category tint as wayfinding.
- **Expressive / formal library →** author a tonal-ramp (A) primitive layer.
- **Rich app / dashboard / admin →** STACK thin-semantic (C) **on top of** a ramp (A) primitive
  library. [S05 · provisional]
- **Brand-led storefront →** brand-dominant (D) over the same primitive→semantic spine.

**The app-register stack, concretely:**
1. **Primitive tier (bottom):** a full set of uniform hue-family ramps. Author it, *or* adopt a
   utility palette wholesale. Never exposed to UI.
2. **Semantic tier (top):** a small closed role set in fg/bg pairs that SELECTS from primitives.
   UI binds ONLY this tier.
3. **Tier encoded in the name:** primitives carry the library prefix; semantics are bare roles
   (so the two can never be confused). [S05 · provisional]

This is the reframe of the method-pluralism rule: color posture was first read as an either/or
*choice* and is now understood as *tiers* an app can stack. The discipline is the same — choose
the tier(s) deliberately and state why. [S05 · provisional]

---

## 8. Cross-cutting refinements (apply across postures)

### Accessibility verification relocates but never disappears
Contrast verification is a **property of the value**, so *where* it is recorded tracks the
posture — but it is always present:
- **Posture A** records measured contrast + an AA/AAA/fail verdict **on every primitive step**
  (the palette is a lookup table). [S01,S04]
- **Postures C / D** push contrast into the **foreground/background pairing**: every "on-X"
  foreground ships with its "X" background (and in D the on-brand pair is a first-class peer), so
  contrast travels bundled with the token rather than per-step. [S03,S04,S05,S06]

The rule is invariant — contrast is always verified somewhere in the system; only its *home*
moves (per-step vs. per-pair). It never silently drops out.

### Mode = a value column (load-bearing, not a new palette)
Light and dark are two **value columns over one identical role vocabulary.** Values swap; names
never do. Adding a mode is adding a column, never forking the token set or prefixing a
`dark-` palette. [S03,S05]

### Register-tuned chroma, quarantined to one swappable layer
Match palette chroma to the brand register (muted for premium/clinical, high-chroma for playful)
**without touching the neutral ramp, type tokens, or chrome discipline.** Loudness lives entirely
in the one swappable category/accent layer, so the same architecture serves a calm *or* a loud
client by re-chroma-ing that layer alone. [S08 · provisional]

---

## Premium craft signals (what makes color read as *authored*, not generated)

The rules above build a *correct* system. These are the moves that make it read as *expensive*.
Reach for them deliberately; each is drawn from real premium work, with its source and tier.

- **Restraint reads as expensive; a rainbow reads as cheap.** A near-monochrome field with **one**
  small, deliberate accent is the single most reliable "this was designed" signal — confident, not
  timid; expensive, not busy. More than one "look-at-me" color per view dilutes all of them.
  [S02,S06 · 🟡] This is the color face of the one-bold-move discipline.
- **Color is a scarce signal — spend hue only where it carries meaning.** Status, a signed delta, the
  single active control, a wayfinding category. Decorative color scattered "to add interest" is the
  loudest generated tell. When in doubt, spend less. [S01,S03,S06 · 🟢]
- **Pick the accent for chromatic DISTANCE from the dominant ground, not just "the one saturated
  thing."** On a bold brand-hue field a same-family button vanishes; the action color must escape the
  field by near-complementary separation. On a neutral ground the accent still wants real distance
  from the neutrals' slight hue bias. [S06 · 🟠]
- **Author dual-ground foreground PAIRS up front**, not as an afterthought `-on-solid` suffix: every
  `text`/`accent`/`border` ships a light-ground value and a dark/brand-ground value from day one.
  Legibility then travels with the token across any surface. [S03,S06 · 🟡]
- **Register-tune the neutrals — don't default to pure black/white.** A warm near-charcoal primary
  text on a warm cream reads softer and more crafted than `#000` on `#fff`; a cool near-black suits a
  clinical brand. A pure mid-grey reads as unconsidered; bias the neutral slightly toward the brand
  hue so it reads as *chosen*. [S04 · 🟠]
- **Make per-step contrast a usable lookup, not decoration.** When you publish a ramp, every step
  carries its measured ratio + AA/AAA verdict so a designer picks a text color by reading the table,
  not guessing. The accessibility lives on the value. [S01,S07 · 🟡]
- **Let the ramp anchor float to the tone that *is* the color**, and name it there — a pale tint
  anchors light, a near-black neutral anchors dark. Forcing every ramp to a symmetric mid-500 is a
  generator default. [S01,S07 · 🟡]
- **Channel-split color so one token yields solid + translucent** (a focus ring and its invalid
  variant are the same hue at different alpha). Frozen hex can't spawn a ring without a new token.
  [S03,S05 · 🟡]
- **Give each hue family an editorial header** — a one-line note on its psychological role and
  intended use — so the palette communicates intent, not just values, and misuse (an alert-red used
  decoratively) is self-evidently wrong. [S01 · 🟠]
- **Commerce micro-detail:** sale price in the accent with the original struck-through is a small,
  expected, premium-reading signal — the kind of detail whose absence reads as unfinished. [S04 · 🟠]
