# GENERATE.md — the atelier generation playbook

> The end-to-end, runnable procedure for taking a brief to a **complete, non-generic design**:
> brand book + design system + Figma pages across all three breakpoints. One ordered loop that
> **both a human developer and the Claude `atelier` skill** execute the same way.
>
> This playbook *orchestrates* the method; it does not restate it. At every decision point it
> names the exact file to open. Read `SKILL.md` for the operating contract and the teacher/template
> rule before you start, and keep `method/anti-slop.md` open the whole time.

---

## How to read this document

- The procedure is a **numbered loop, Steps 0 → 6**. Work it top to bottom; do not skip ahead.
- **The dependency stack is non-negotiable** (`SKILL.md` → "The dependency stack"): anti-slop
  rules → tokens (color → type → space/grid) → components → pages → (motion, later). Never
  generate a layer before the one beneath it is solid. A page built before its token system
  regresses to generic.
- Each step lists: **inputs → the file(s) to open → the decision(s) to record → the output**.
- Every recorded decision lands in the **project brief record** (one living doc per project). The
  brief record is the single source of truth downstream; if a choice isn't written there with its
  *why*, it didn't happen.
- **Confidence discipline.** `evidence/VALIDATION.md` marks every principle 🟢 load-bearing /
  🟡 corroborated / 🟠 provisional. Lean on load-bearing principles freely. When you invoke a
  provisional one, **flag it as provisional in the brief record** so the human reviewer knows it's
  a bet, not a proven law. Never silently promote a provisional principle to a hard rule.
- **Anonymization is mandatory.** No source project's palette, hex, fonts, copy, screens, or
  client identity ever enters an output. Sources are teachers, not templates (`SKILL.md`). Carry
  *method*; discard *specifics*.

---

## Step 0 — INTAKE the brief

**Goal:** capture enough signal to *name the register* in Step 1. A vague brief caps output
quality more than any other factor (see Honest limits). Do not proceed to Step 1 until the
register-critical answers exist — if the client is thin on an answer, propose a default and mark
it an assumption to confirm.

**Open:** nothing yet — this is elicitation. (Keep `method/00-decide.md` in mind; its register
vocabulary tells you which answers matter most.)

**Ask the client/user — the concrete question list:**

1. **Industry & what the product *is*.** What does it sell or do? Who uses it, and in what
   mindset? (This is the raw material for the register.)
2. **Register / direction in their words.** Which adjectives? (clinical, editorial, luxury,
   playful, technical/B2B, warm-retail, utilitarian…). Ask for 3–5 and for one they explicitly
   *reject*.
3. **Product archetype.** Is this a **storefront**, a **dashboard/app**, a **marketing/brand
   site**, a **formal library**, or a mix? (Gates whole method layers in Step 1.)
4. **Brand inputs that already exist.** Any locked colors, a logo, chosen fonts, a tagline,
   existing brand guidelines? For each: is it **fixed** (must honor) or **provisional** (may
   replace)? Get the actual assets if they exist.
5. **Reference sites — liked AND disliked.** 2–4 of each, with one sentence on *why* for each.
   The disliked set is as diagnostic as the liked set (it reveals the anti-slop boundary).
6. **Chroma & tone cues.** Should color feel muted/premium or loud/playful? Light-ground or a
   bold brand-colored ground? Any hard color constraints (accessibility, regulatory, cultural)?
7. **Target breakpoints.** Confirm desktop / tablet / mobile widths (default to the three-tier
   model; capture exact viewport anchors if the client has them).
8. **Deliverables wanted.** Brand book? Full design system/tokens? Which **page types**
   (home, PLP, PDP, cart, checkout, about, pricing, auth, dashboard, blog, legal…)? Figma file?
   Build-ready specs for a downstream stack (WordPress / Shopify / React)?
9. **Hard constraints.** Locked brand elements, accessibility target (AA/AAA), required
   languages/locales, regulatory gates (age/consent), performance limits, existing design-system
   or component-library they must stay compatible with, timeline.
10. **Content reality.** Real copy and imagery, or placeholder? Catalog size / taxonomy depth
    (drives whether category-color is even viable)? Data-dense surfaces (tables, dashboards)?

**Record (brief record §Intake):** the answers above, each brand input tagged fixed/provisional,
and an explicit **deliverables + page-types list**. Note every assumption you filled in for the
client to confirm.

**Output:** a populated Intake section — enough to run the decision engine.

---

## Step 1 — DECIDE (run `method/00-decide.md`)

**Goal:** choose *how this project is built* and record each choice with its *why*. This is the
craft step; the rest is execution. atelier is not one system applied everywhere — it is a set of
legitimate construction methods, and the discipline is choosing the right ones **deliberately**
and stating why (reflexive choice is the failure mode).

**Open:** `method/00-decide.md` (the chooser) alongside `method/anti-slop.md` (Rule 0).

Run the decision checklist end to end. Each line below produces a recorded answer.

1. **Name the register** (`00-decide.md` → Step 0). Base register + modifiers (chroma, tracking,
   density), from the Step-0 vocabulary: expressive/formal library · taxonomy commerce · rich
   app/dashboard · brand-dominant storefront · marketing/brand site. Most briefs are a base
   *plus modifiers* ("clinical B2B taxonomy commerce"). The register drives everything below.

2. **Gate the product archetype** (`00-decide.md` → Step 4). Decide storefront / dashboard /
   marketing / app so the **conditional method layers** switch in or out: storefront anatomy,
   page-skeleton library, application shell & state-as-design. Don't pay for layers the register
   doesn't need. (Responsive-component discipline is **always on** — never gated.)

3. **Run the lead color diagnostic** (`00-decide.md` → Step 1; detail in `method/01-color.md`).
   Ask **"what does color DO on this page?"** and pick the posture(s):
   - Expressive range across a wide system → **(A) tonal ramp**
   - Wayfinding, users learn taxonomy by hue → **(B) category-color** `{accent, tint}` kits
   - Theming neutral app chrome by mode → **(C) thin-semantic** role set
   - Carrying the whole brand as surface → **(D) brand-dominant** field
   Then decide **whether postures STACK as tiers** and how many you expose. The clearest case: a
   rich app stacks **(C) thin-semantic on top of an (A) ramp primitive library**. Record the
   posture(s) *and* the tier count. Confirm the two cross-cutting rules: **color is a scarce
   signal** (ration hue to carry information) and **accessibility lives on the value** (per-step
   contrast, or relocated to the fg/bg pairing — never dropped).

4. **Pick the type strategy** (`00-decide.md` → Step 2; detail in `method/02-typography.md`).
   **(A) single-family size-stepped** (default for UI-heavy) vs **(B) role-assigned multi-face**
   (editorial/brand-forward, disciplined — one face per function). A third face must have a *job*
   (e.g. mono for status/metadata), capped at ~3 faces. Set the **letter-spacing register knob**:
   default tracking 0 for neutral/clinical/technical/B2B; negative-on-display only for
   editorial/luxury — and justify it.

5. **Scope density** (`00-decide.md` → Step 3). Is there a genuinely data-dense surface (tables,
   dashboards, dense cards)? If yes, the data-density method and often a parallel compact library
   come into scope, and where the density line falls is recorded. If no, don't build for it.

6. **Pick the default constants to tune** (`00-decide.md` → Step 5, policy 2:
   *defaults, then per-project tuning*). atelier ships proven defaults (base unit, step scale,
   tracking, line-height ratios, ramp lengths, elevation offsets). List which constants this
   brand's specimens will push on, and schedule the **tuning pass with human sign-off**. Never
   ship raw defaults unexamined; never start from a blank numeric slate.

7. **CHOOSE THE ONE BOLD MOVE** (`00-decide.md` → Step 5, policy 1 — standing policy; `anti-slop.md`
   Rule 0). Every design makes **exactly one** deliberate departure from safe defaults — one place
   it takes a real aesthetic risk (a type move, a layout break, an unexpected color decision, a
   density signature). **Not zero** (templated) and **not many** (noise). Name it now, in one
   sentence, and say *where* it is spent and why it won't fight the funnel. In registers where the
   usual levers are absent (a dense dashboard has no hero scale or decorative color), spend it
   elsewhere: a signature data-viz treatment, a distinctive nav behavior, a disciplined unexpected
   accent. **This sentence is load-bearing** — Step 6 checks that it is nameable in the finished
   design.

**Record (brief record §Decisions):** every checklist line from `00-decide.md` with its answer and
its *why*, plus the one-bold-move sentence. Tag any provisional-tier principle you're relying on.

**Output:** a completed decision record. The downstream chapters now have their inputs.

---

## Step 2 — BUILD THE DESIGN SYSTEM (bottom-up)

**Goal:** mint the token system and components so that **everything binds to tokens, never raw
values**. Build in strict order; the layer order is the dependency stack.

**The spine (invariant, every layer — `method/00-decide.md` "the spine"):** primitives carry raw
value with zero intent → semantics carry role-named meaning → components bind to semantics only →
**nothing in the UI ever consumes a raw value directly.** Name by *value* at the primitive tier,
by *intent* at the semantic tier; never mix conventions within a tier. Encode the tier in the name
(library prefix for primitives, bare role for semantics) so a primitive can't be grabbed by
accident.

**Policy (apply throughout — `00-decide.md` Step 5.2):** start from shipped **default constants**,
then run the **per-project tuning pass against the brand's specimens with human sign-off**.
Defaults are the floor, not the answer.

Build in this order:

**2a. Color** — open `method/01-color.md`.
- Lay the **two-tier spine** first (§1). Then instantiate the posture(s) chosen in Step 1:
  - **(A) tonal ramp:** Family → Ramp → Step; one fixed step scale, denser in the lights;
    anchor each ramp at its most representative tone (never force a mid-step anchor); semantic
    aliases on a Role × Prominence/Status × Context matrix; **measured contrast + AA/AAA/fail
    verdict on every step**.
  - **(B) category-color:** mint each category as a paired `{accent, tint}` kit; keep it separate
    from a small functional set; make accent a **scope function** (chrome = brand constant,
    content region = category variable, else brand-primary fallback — write the fallback down).
  - **(C) thin-semantic:** small closed role set in **fg/bg pairs**; theme by **value-mode on one
    name** (adding dark = a value column, never a `dark-` palette or a second component);
    channel-split colors so alpha variants derive from one token; ring-as-shadow for focus.
  - **(D) brand-dominant:** tiny palette (brand hue + near-black + paper-white + ONE accent chosen
    for **chromatic distance** from the brand hue); author **dual-ground foreground pairs** as
    first-class peers; color-field boundary *is* the section boundary.
- If postures **stack** (e.g. C-on-A), author the primitive tier at the bottom (author it or adopt
  a utility palette), expose only the semantic tier to UI.
- Honor the anti-slop color rules: no equal-lightness steps, no symmetric mid-anchored ramp, never
  ship swatches without contrast verdicts, no single-ramp-per-hue.

**2b. Typography** — open `method/02-typography.md`.
- Every style is a **composite token** (family + weight + size + line-height + letter-spacing +
  paragraph-spacing bundled under one name); keep atomic sub-tokens independently addressable.
- Roles from a **role × size matrix with an independent weight axis**; provision **two family slots
  (display + body) from day one** even if they resolve to one face. Apply the type strategy and the
  letter-spacing register knob from Step 1.
- Line-height **inverse to size** (tight display ~1.05–1.1, loose body ~1.3–1.45), snapped to a
  rhythm grid; **1.0 for single-line centered roles** (buttons/nav/chips), ~1.5 for flowing body.
- Responsiveness = **per-breakpoint composite swap**, ~one size notch per tier — never fluid-scale
  one property.

**2c. Space / grid** — open `method/03-space-grid.md`.
- **One base unit; three parallel role-named axes** (spacing / padding / size), primitives named by
  literal value, three tiers (value primitives → t-shirt aliases → component-scoped tokens), always
  mint explicit `*-none` tokens.
- **Radius** posture: size-keyed ramp (expressive) vs single-knob (flat app). **Elevation** posture:
  two-layer ambient+contact (expressive) vs flat 1px-ring (dense/flat). Pick by register; both ship
  a `-none` and pull tint from a tiny alpha-only token set.
- **Grid** = a token system, **breakpoint is the top axis**; each tier a complete independent grid;
  frame = three paired tokens per breakpoint (device width, container max-width, margin, with
  `margin = (device − container)/2`); column count a per-tier set, each count with its own gutter;
  gutters/margins draw from the shared spacing scale; three independent padding families (device
  margin ≠ container inset ≠ section spacing); container capped+centered on desktop, edge-to-edge
  (margin→0) on mobile.

**2d. Components** — open `method/04-components.md`.
- **Atom → molecule → organism**; name explicit base atoms and **instance, never copy**; states &
  kinds are **variant axes, never forked copies**; variant sets only where a real axis exists;
  one-line usage note per component; strict path taxonomy, function-grouped.
- **Family over mega-component** — split the moment two axes stop being orthogonal; inversely,
  **collapse N looks to one themed atom** (externalize the per-look delta to a single
  data/category token binding). Hoist density/scale to a **parallel compact library**, not a
  per-component variant.
- Pull in the **conditional** disciplines only if Step 1 gated them in: responsive-component
  discipline (always on), data-density method, application shell & state-as-design.

**Record (brief record §System):** the posture instantiations, the tuned constants with sign-off,
and the component inventory. Note which tokens/components lean on provisional principles.

**Output:** a complete token set + component library, everything bound to tokens.

---

## Step 3 — ASSEMBLE PAGES (from `method/page-skeletons.md`)

**Goal:** instantiate the page types the brief needs as ordered section stacks, bound to the
system from Step 2.

**Open:** `method/page-skeletons.md` and `method/05-composition.md`.

1. **Pick the page types** the brief's deliverables list calls for (Step 0 §8). Only build what's
   asked; each has a canonical stack in `page-skeletons.md` (Home, PLP, PDP + buybox micro-skeleton,
   Cart, Checkout, About, Contact, Blog index/article, Account/Dashboard, Pricing, Auth, Legal, plus
   overlays, confirmation, empty-states, quiz/RMA where the register adds them).

2. **Author GLOBAL CHROME once** (header/nav + utility cluster + footer, promo bar optional) and
   model each page as `CHROME + BODY STACK` — never a flat section list. Prepend a **breadcrumb**
   as the first in-body element on deep/transactional pages; the homepage gets none.

3. **Instantiate each section stack** in order, tagging sections [required]/[recommended]/[optional]
   per the skeleton. Honor the composition **invariants** (`05-composition.md`): density oscillation
   (two axes — height *and* surface-weight in high-chroma registers), grid-break-as-narrowing,
   threaded proof, section-opening grammar. Order sections as a **decision narrative**
   (desire → justify → objections → next step); on homepages apply convince/convert
   **purpose-alternation**.

4. **Apply the container contract** (`page-skeletons.md` → page-shell container + `03-space-grid.md`
   §5): desktop wide capped centered column, tablet mid-width, mobile edge-to-edge (margin→0,
   padding insets). Container width = `device-width − 2×margin`; section rhythm / container inset /
   device margin are three independent responsive knobs.

5. **Keep section order breakpoint-invariant.** Author the desktop frame as canonical; derive
   tablet/mobile **only** by collapsing columns (N → N/2 → 1) and drawer-izing filters/sidebars
   behind a trigger with a sticky commit bar. **Never re-order per breakpoint** — that silently
   forks the funnel. (A breakpoint may still *own* net-new overlay organisms — bottom-sheet,
   slide-up filter — authored as their own entries.)

6. Close each page in its correct register: editorial/long-form pages hold the narrow measure and
   close on **lateral navigation** (related/next); commerce pages close on a **cross-sell rail**.
   Mixing closers is the register error.

**Record (brief record §Pages):** the page list, each page's instantiated stack with section tags,
and any skeleton deviations with reasons.

**Output:** page definitions as ordered, token-bound section stacks, ready to build.

---

## Step 4 — BRAND BOOK

**Goal:** produce the human-facing articulation of the system — adoptable from the doc alone.

**Open:** `method/01-color.md`, `method/02-typography.md` (for the usage rules), `SKILL.md`
("What atelier produces" — logo honesty).

1. **Color system** — document the posture(s) and the two-tier spine: primitive ramps / role set,
   semantic aliases, mode columns where they exist, and the contrast verdicts. Use **explain →
   show → apply** cards (definition + live per-token specimen + "where to use this" note) —
   never a bare value dump.

2. **Type system** — the composite styles on their role × size × weight matrix, the display/body
   split, the letter-spacing register decision, line-height logic, and responsive composite-swap
   behavior. Same explain-show-apply treatment.

3. **Usage rules** — clearspace, do/don't, scarce-signal color rule, the reserved accent's job,
   the one-bold-move stated as an identity principle so it's protected downstream.

4. **Logo = DIRECTION, not final artwork** (honest framing per `SKILL.md`):
   - A written **direction** (what the mark should feel like and why, tied to the register).
   - **Candidate marks** — several explorations, not one.
   - **Usage rules** — clearspace, min sizes, color-on-ground pairs, misuse don'ts.
   - An **explicit honest note** in the deliverable: a client-ready final logotype needs human
     iteration; this is a strong starting direction, not a finished mark. State this plainly — do
     not oversell.

**Record (brief record §Brand book):** links to the assembled brand-book artifact and the logo
direction note.

**Output:** a brand book (color + type + usage + logo direction/candidates/usage).

---

## Step 5 — BUILD IN FIGMA (all 3 breakpoints)

**Goal:** realize the system and pages in Figma, **bottom-up**, bound to Figma variables — never
hardcoded values. This mirrors the dependency stack: variables → components → pages.

**Prerequisite — load the skill first.** Before any `use_figma` write call, **load the `figma-use`
skill** (mandatory; skipping it causes hard-to-debug failures). For creating a new file, load
`figma-create-new-file` first; for pushing composed pages from the system, `figma-generate-design`
/ `figma-generate-library` give the WHAT-and-in-what-order. Open a file **session** (`create_session`
with the fileKey) before file tools. If the fileKey is missing or a literal placeholder
(`undefined`/`null`/`{{…}}`), **halt and report** — never guess or reuse an unrelated key
(`anti-slop.md` S05).

Build order (do not invert):

1. **Tokens / variables first.** Create the Figma variables for color (primitive collection +
   semantic collection, with mode columns where posture C/D needs them), type composites, the
   spacing/radius/elevation scale, and the per-breakpoint grid frame. Primitives carry the library
   prefix; semantics are bare roles. This is the substrate every later node binds to.

2. **Components next, with variants + states.** Build atoms → molecules → organisms as variant sets
   (states/kinds as axes), each **bound to the semantic variables** — never a raw value. Author
   responsive components as **one set with a `Breakpoint` variant {Desktop, Tablet, Mobile}**;
   co-locate overlay/open states as hidden child frames inside the same variant.

3. **Assemble pages, section by section, across desktop / tablet / mobile.** Instantiate the Step-3
   stacks using the real components; apply the container contract per breakpoint; keep section order
   breakpoint-invariant (reflow by column-collapse + drawer-izing only). Every frame reads only from
   variables and component instances.

**Record (brief record §Figma):** file key, variable collections created, component list, and the
page frames built per breakpoint.

**Output:** a Figma file — variables, components, and assembled pages at all three breakpoints,
fully bound to tokens.

---

## Step 6 — VERIFY

**Goal:** confirm the output is traceable and non-generic before delivery. If it fails here, it is
not finished.

**Open:** `method/anti-slop.md` (run it as a checklist) and `evidence/VALIDATION.md`.

1. **Run the full anti-slop ruleset** against every layer (architecture, color, type,
   space/radius/elevation, components, page composition — plus the register-specific additions for
   dashboard / storefront / thin-semantic / brand-dominant / grid / category-color as they apply).
   Fix any hit **at the cheapest layer it lives on**, then re-check.

2. **Name the ONE bold move in the finished design** (`anti-slop.md` Rule 0 — overrides all).
   Point to where it is, in the actual frames, in one sentence. **If you cannot name it, the design
   is not finished** — a design with no point of view is slop no matter how clean its tokens are.

3. **Traceability audit.** Every frame traces to **tokens** (no raw hex/px/font in any component or
   page — all through semantic aliases) **and** to a **validated principle**. Spot-check that no UI
   node binds a primitive directly. For every principle the design leans on, confirm its tier in
   `evidence/VALIDATION.md`; provisional-tier bets are allowed but must be **flagged for the human
   reviewer**, not presented as settled law.

4. **Breakpoint parity.** All three breakpoints exist, derive from the canonical desktop order by
   column-collapse/drawer-izing only (no re-sequencing), and share identity + tokens.

5. **Present candidates and iterate.** Deliver as a strong first draft for human review (see Honest
   limits) — not as a zero-edit final.

**Record (brief record §Verification):** the anti-slop pass result, the named bold move, the
traceability verdict, and the list of provisional principles flagged.

**Output:** a verified, traceable, point-of-view design package ready for human iteration.

---

## Honest limits (state these; do not oversell)

- **Logo = direction, not final.** The logo deliverable is a direction + candidate marks + usage
  rules. It is the weakest link in AI generation. A client-ready final logotype needs human
  iteration — say so plainly in the deliverable.
- **"One-shot" = strong first draft, not zero-edit.** atelier produces a coherent, on-brand,
  traceable *first draft*. Promising a zero-edit full design is how you ship confident slop.
  Present candidates; expect a human iteration pass.
- **Motion / interaction is a later phase.** This playbook produces the static system and frames.
  Motion, interaction, and live logic layer onto an existing component system afterward; they are
  not part of this loop.
- **Output quality is capped by how well the brief/register was named.** The single biggest lever
  is Step 0 → Step 1. A vague brief and a mis-named register produce a competent-but-generic result
  no amount of downstream polish rescues. If the register can't be named with conviction, go back
  to intake before building pixels.
- **Provisional principles are bets.** Much of the richest method (category `{accent,tint}` kits,
  brand-dominant posture, app-shell matrix, composition refinements) is currently single-sourced in
  `evidence/VALIDATION.md`. Use them — they are the interesting moves — but flag them as provisional
  to the reviewer rather than presenting them as proven law.
```
