# atelier — design-system construction methodology

> Synthesized by studying mature design systems for *method*. Portable principles only; no source-specific values, fonts, or layouts. This is how atelier builds a system from scratch for a new brand.

# atelier — Design-System Construction Methodology

A portable, bottom-up method for building a design system from scratch for any brand. These are the *rules of construction*, not any one brand's values. Work the layers in order — each rests on the one below it. Every layer shares one spine: **primitives carry value, semantics carry meaning, components bind meaning to a part, and nothing consumes a raw value directly.**

---

## Standing policy (decided — applies to every project)

These two calls are resolved at the skill level, not per project:

1. **Every design makes exactly one bold move.** The method *mandates* a single, deliberate
   departure from safe defaults per project — one place the system takes a real aesthetic
   risk (a type move, a layout break, an unexpected color decision, a density choice). Not
   zero (that reads as templated/safe). Not many (that reads as noise). **One**, chosen
   intentionally and made to feel inevitable. This is atelier's core anti-slop guarantee:
   a system with no point of view is slop no matter how clean its tokens are. *Where* to
   spend the boldness stays a per-project human call (see `_DECISIONS-NEEDED.md`), but
   *that* there is one is non-negotiable.

2. **Defaults, then per-project tuning.** Atelier ships with proven default constants (base
   unit, step scale, tracking, line-height ratios, ramp lengths, elevation offsets) so every
   project starts from a sane, consistent foundation — then *tunes* them against the specific
   brand's specimens, with human sign-off on the feel. Never ship raw defaults unexamined
   (that's generic); never start from a blank numeric slate every time (that's slow and
   inconsistent). Defaults are the floor, not the answer.

---

## 0. The spine (applies to every layer)

1. **Two hard tiers everywhere.** A *primitive* tier holds raw values with zero intent. A *semantic* tier holds role-named aliases that only ever point *at* primitives. Components consume semantics exclusively.
2. **One mental model across all domains.** Color, type, spacing, padding, sizing, radius, and effects all use the same primitive→semantic→component-scoped shape and the same naming grammar. Learn one foundation, you know them all.
3. **Name by intent at the semantic tier, by value at the primitive tier.** Words where a value is a reusable *decision* (`spacing-small`, `text-primary`); literal values where it's a raw *ingredient* (`spacing-4`, hue step `500`). Never mix the two conventions inside one tier.
4. **Document to teach, not to dump.** Every foundation ships as explain → show → apply: a plain-language definition, a live specimen of every level, and a per-level "where to use this" note, all on one shared column grid.
5. **Method pluralism — there is no single correct system.** Each layer below describes *more
   than one legitimate construction method*, and atelier **chooses the method per project**, not
   by dogma. (Learned by contrasting three real systems: a large formal ramp-based library, a
   lean category-color commerce project, and a thin-semantic shadcn/Tailwind dashboard — all
   excellent, built differently.) Match the method to the product. For color specifically there
   are now **three** methods: **(A) tonal ramp** (expressive/formal libraries), **(B)
   category-color** (taxonomy-driven commerce), **(C) thin semantic variable layer** (rich apps
   / dashboards, theme-by-mode). The failure is picking a method reflexively; the discipline is
   choosing it deliberately and stating *why* in the brief. (See the token-method decision in
   `_DECISIONS-NEEDED.md`.)
6. **Live components over style boards.** When a documented style sheet and the actual built
   components disagree, the components are the truer current state; the board is documentation
   that may lag. Read both, trust the build.

---

## 1. Color

**First, choose the color method (per spine rule 5):**
- **(A) Tonal-ramp system** — for expressive/formal libraries with a wide chromatic range. Full
  stepped ramps per hue, per-step contrast. Detailed below.
- **(B) Category-color system** — for taxonomy-driven commerce (a shop whose products fall into
  natural categories). Each category gets a **base + a light/tint pairing** used for
  surfaces/backgrounds, kept separate from a small **functional set** (primary, success, error,
  hover). Color becomes wayfinding — users learn categories by hue. Flat, lean, no deep ramps.
- **(C) Thin semantic variable layer** — for rich apps / dashboards that need theming. A small,
  closed set of role tokens in foreground/background pairs (`background/foreground`, `primary/
  -foreground`, `muted`, `accent`, `destructive`, `border`, `ring`…), theme-switched by **mode
  on the same names** (light/dark are value columns, not new palettes). See the Source 03
  additions at the end of this doc for the full method.
- All three obey the spine: a semantic tier names roles; nothing in UI binds a raw value.

The rest of this section details method (A); methods (B) and (C) are detailed in their sections.

**Primitive ramps.** Organize as **Family → Ramp → Step**, three namespace levels. A family groups perceptually-adjacent ramps; allow **multiple ramps per hue family** (a warm variant, a muted variant, a tinted variant) rather than forcing one compromise ramp per hue.

- Use **one fixed step scale across every ramp**, denser at the light end (extra ultra-light steps below the mid, one ultra-dark above). Uniform steps make ramps interchangeable — swap the hue, keep the step.
- **Do not space steps by equal lightness deltas.** Perceptual spacing is intentionally uneven: finer in the highlights, where tints get used most and the eye discriminates best.
- **Anchor each ramp at its most representative tone and name the ramp after that anchor.** A pale tint and a near-black neutral do not carry their character at the same lightness; don't force a mid-step anchor on every ramp.
- **Record measured contrast + an explicit AA/AAA/fail verdict on *every step*** against a fixed reference, not just the anchor. Accessibility is a property of the value, so it lives on the primitive, turning the palette into a lookup table.

**Semantic aliases.** Name on a matrix of **Role × Prominence/Status × Context**:
- *Role* = the thing being painted (text, surface, icon, border).
- *Prominence* = primary / secondary / tertiary.
- *Status* = success / warning / error.
- *Context* = a suffix like `-on-solid` for tokens meant to sit on a filled color.

Deriving tokens from a fixed matrix makes coverage auditable and missing combinations obvious. Give each hue family an **editorial header** — a human title and a short note on its psychological role and intended use — separate from the swatch grid.

---

## 2. Typography

**First, choose the typeface strategy (per spine rule 5):**
- **(A) Single-family, size-stepped** — one typeface carries all roles via the size/weight
  matrix below. Cohesive, systematic; default for UI-heavy products.
- **(B) Role-assigned multi-typeface** — assign *distinct faces to distinct functions* (display
  vs body vs UI/links/buttons), each role carrying its own named size + weight. More
  personality; legitimate and strong **only if disciplined** — one face per function, never
  mixed ad hoc. Good for editorial/brand-forward work.
- Either way, each style is still a composite token (below) and roles still come from a matrix.

Model each style as a **composite token**, never a bare font-size. Every step bundles: font-family, named weight/style, size, line-height, letter-spacing, paragraph-spacing, (and indent). Consumers reference one name; correct typesetting travels with it.

**Structure as a matrix, plus an orthogonal weight axis:**
- **Role families** on one axis (~5: a display/attention tier, headline, title/subhead, body/reading, label/UI-caption).
- **T-shirt size steps** on the other (XS…XL, extend as needed).
- **Weight as a third, independent axis** — emit one named style per (step × weight) cell; offer the full weight ladder only where it's used (display/headline) and restrict body/label to a few weights to prevent bloat.

**Encode the optical laws as functions, not hand-tuned per-step numbers:**
- **Letter-spacing ≈ a fixed fraction of size** — strongly negative on large display, trending toward zero/positive as size shrinks.
- **Line-height inversely proportional to size** — tight for display (~1.05–1.1×), loose for body (~1.3–1.45×) — and **snapped to a small rhythm grid** (multiples of 2/4) rather than arbitrary decimals.
- **Overlap adjacent families' size ranges deliberately** so the same optical size can carry a different personality by role (a body-adjacent title vs. a small headline at the same px).

**Provision two family slots from day one** — one display, one body — as tokens even if they currently resolve to the same face; the display/body split is the most common future change. **Store per-breakpoint values** (desktop/tablet/mobile) for size, line-height, tracking on each step so one name resizes fluidly; align the breakpoint delta to roughly one size notch. Name hierarchically (`Typography/<Family>/<Step>/<step>-<property>`; composite as `<Family>/<Step>/<Weight>`) and keep atomic sub-tokens independently addressable for edge cases.

---

## 3. Space, Sizing, Radius, Elevation

**One base unit; three parallel axes.** Generate every dimension as an integer multiple of a single small base. Keep **spacing** (gaps between siblings), **padding** (inset within a container), and **size** (fixed element dimensions) as **separate role-named axes** even though they share one number line — so "all internal padding" and "all inter-element spacing" can be reasoned about, and diverge later, independently. **Name primitives by literal value** (`spacing-4`, `padding-20`), not an index — self-documenting, collision-free, insertable without renumbering.

**Three tiers:** value-named primitives → t-shirt semantic aliases (`spacing-small/large/2x-large`) → **component-scoped tokens** that bind one part to a primitive and isolate its quirks (`button-radius`, `input-field-width`). Always include explicit **`*-none`** tokens so "intentionally square/flush" is a deliberate choice.

**Radius scales with element size.** Reject a single global radius. Tiny chips get a hair of radius, buttons a little more, large blocks often zero. **Key the radius token's name to the component's size** so radius tracks element scale by rule.

**Elevation as a composite, role-mapped ramp (1…N):**
- Each level stacks **two shadows** — a soft ambient layer (large blur/spread, low alpha) plus a tight contact layer (small blur, higher alpha). One flat drop shadow is the tell of a fake.
- Both pull tint from a **tiny set of alpha-only color tokens**, so the whole system re-tints (or dark-mode-inverts) from two values.
- **Geometry scales monotonically** — y-offset, blur, spread grow together as level rises, keeping the ramp perceptually ordered.
- **Bind each level to a documented component/state roster** (resting cards, buttons, menus, dropdowns, modals) so z-depth is a system-wide contract, not an eyeball.

**Each effect gets its own scale shape.** Match ramp resolution to expressive need: fine-grained for blur, few steps for inner shadow, **categorical semantic variants** (not sizes) for focus rings. Don't force one ramp length onto effects that don't want it.

---

## 4. Components

- **Name explicit base atoms** and tag them (`Cell (Base)`). Higher structures *instance* the base; one edit propagates. Never copy-paste a primitive into each composite.
- **Encode the composition ladder in the name.** Atom keeps the bare noun (`Field`); its molecule appends a role word (`Field group`) bundling the atom with its satellites (label, helper, affordances). Altitude is readable from the name; the group is the intended unit of reuse.
- **Prefer a family of specialized siblings over one mega-component.** A button "need" is a family — generic action, icon-only, filter, floating-action, selectable — each scoped to one job with small, orthogonal axes (size × state), not one set with an exploding matrix.
- **Variant sets only where a real axis exists.** Interactive controls and multi-kind cells get sets; a static card or a lone glyph stays a plain component. Don't wrap single-state elements in a set for symmetry.
- **States and kinds are variant axes, never forked copies.** One set holds default/hover/disabled/error so every state shares geometry and tokens and the full inventory is inspectable in one place.
- **Hoist density/scale to the library level.** Ship parallel libraries (full + compact) with *identical* component names rather than adding a density variant to every component — swap the subscribed library to rescale a whole project losslessly.
- **Strict path taxonomy + functional pages.** `design_system/<library>/components/<Name>`, with category prefixes for catalog-like items; group editor pages by UI function with a stable marker.
- **One-line usage description on every component** — what it is and when to use it — so the library is a self-describing API.

---

## 5. Page composition

- **Band chassis.** Build pages from a fixed vocabulary of full-width horizontal sections, each owning one uniform outer margin and one top inner-padding; let **content set height**, not a fixed slot. Shared chassis is the biggest driver of "composed, not templated."
- **Oscillate density.** Never stack two tall, heavy sections back-to-back. Alternate a tall high-information band with a short calm one (trust strip, one-line quote, link row) to give the scroll a pulse and the eye recovery points.
- **Hero as a stage, not a container.** Full-viewport but visually light (one image/moment, minimal copy); hand proof immediately to a thin credibility strip right below. Separate *impression* from *justification*.
- **Two nested width systems.** A wide container for grids/media; a deliberately **narrower measure** for reading-dominant content. **The intentional grid-break is a *narrowing*** to a centered column for editorial/quote/capture moments — never a widening of text to full-bleed. Cap prose and section headers to a readable measure even inside full-width bands.
- **Flip the 50/50 split.** Use image+content splits as a repeatable unit and **alternate sides** on each consecutive use, guiding the eye diagonally down the page.
- **One token ramp drives everything.** Every gap, padding, and width resolves to the shared scale; variety lives in composition and content, not ad-hoc pixels. That constraint is what reads as one authoring hand.
- **Thread proof throughout.** Ratings, badges, before/after, pull-quotes recur at multiple depths (in cards, a reviews band, standalone quotes) rather than clustering in one testimonial block.
- **Order sections as a decision narrative.** Sequence by the user's journey — desire → justify → handle objections → next step — and keep the primary action reachable across the arc (e.g. a persistent commitment bar on long transactional pages). Section order is an argument, not a stack.
- **Consistent section-opening grammar.** A reusable header unit (optional badge + heading + support line, held to the narrow measure) opens most bands so every new topic has a predictable entry point while its interior varies freely.



---

# Additions from Source 03 (dashboard / shadcn+Tailwind)

> New layers/choices this source justifies: a third token method (thin semantic variable layer), a data-density method, and an app-shell/state method. Integrated under the existing spine + method-pluralism rules.

The following are genuinely NEW sections to append to `methodology.md`. They do not restate the existing two-tier spine, the tonal-ramp/category-color color methods, the single/multi-typeface split, the stacked-shadow elevation ramp, or the band-chassis page composition — they extend method pluralism into a third token method and add two new domains (data density, app shell) that the prior page-oriented sources never covered.

---

## 1b. Color — third method: the thin semantic-variable layer (apps/dashboards)

Add a third option to the color-method choice (spine rule 5), alongside (A) tonal-ramp and (B) category-color:

- **(C) Thin-semantic-variable system** — for rich, stateful *application* UI (dashboards, admin
  consoles, deep component trees that re-theme). A full primitive ramp sits underneath, but the
  *only* thing components ever touch is a **small, closed set of role tokens**. This is the spine's
  two-tier rule taken to its minimal top layer: not Source 01's exhaustive Role×Prominence×Context
  matrix, but a deliberately tiny role set.

Rules specific to method (C):
- **Role tokens in foreground/background pairs.** Surface pairs (background, card, popover), an
  action pair (primary + its foreground), quiet pairs (muted, accent + foregrounds), a status pair
  (destructive + ring), and chrome roles (border, input, ring). Every "on-X" foreground ships with
  its "X" background so contrast travels with the token.
- **Theme by value-mode on one name.** Light and dark are twins sharing identical role names; only
  the resolved value changes per mode. Adding a theme = adding a value column, never a component
  variant or a `dark-`-prefixed palette. (Contrast method (A), where dark mode means re-selecting
  ramp steps per element.)
- **Channel-split colors.** Store base colors as bare channels and apply alpha at use-site, so one
  token yields solid fills, borders, *and* translucent rings/overlays — no new token per opacity.
- **One radius knob.** A single base-radius token derives every corner (named steps resolve from
  it). This is a method-pluralism alternative to Section 3's size-keyed per-component radius: the
  one-knob form suits a flat, uniform app idiom; the size-keyed ramp suits an expressive component
  family. Choose by product.
- **State-as-enum wired to tokens, ring-as-shadow.** Interactive atoms carry
  Default/Focus/Invalid/Disabled as variant axes; focus pulls the ring token, invalid pulls
  destructive, disabled pulls muted; focus/validation render as a **spread box-shadow** in the ring
  color so focus never changes the box model (no 1px reflow).
- **Own-the-atom contract.** Atoms are source you paste and bind to your tokens, not a versioned
  black-box dependency. Portability is the *naming contract* (primary, foreground, ring, radius) —
  any project honoring the names gets consistent, re-skinnable components with no upgrade lock-in.

---

## 6. Data density (dashboards, tables, data-dense surfaces)

A new domain the prior page-oriented sources did not cover. Density **inverts** the marketing-page
levers: you cannot push things apart with whitespace or signal importance with scale, so hierarchy
and separation must be *drawn*.

- **Micro-spacing ramp.** Extend the base spacing scale with fine sub-rungs (e.g. 2/6/10 between
  the usual rungs) so cell padding, badge insets, and icon gaps tune tightly while staying on-grid.
  Density is achieved by selecting smaller rungs — never by hardcoding arbitrary gaps.
- **Hierarchy by weight + color, not size.** On a tiny type scale (xs/sm), stack a bold near-black
  primary over a muted secondary inside one cell (name over email, value over label). Font-weight
  and foreground-vs-muted color are the two space-free levers that replace the 32–48px scale jumps
  of a hero.
- **Slot-based tables.** Model the data table as three independently toggle-able regions — an
  optional toolbar (filters/search/bulk actions), the body (header + rows), and a footer
  (selection-count readout + pagination) — plus an optional caption. The same primitive scales
  from a bare list to a full grid.
- **Typed cells with fixed alignment.** Treat cells as a small library: identity (avatar +
  two-line stack), numeric (tabular, right-aligned), status (semantic pill), media/brand, action
  (ellipsis menu). Identity/text left; numbers right with tabular figures; actions right.
- **Reserve interactive slots even when off.** Pre-allocate the selection-checkbox column, the
  sort indicator on sortable headers, the selection-count readout, and pagination (current page is
  the *only* filled chip) so toggling state never reflows the grid.
- **Stat-card grammar — one dominant value.** Optional parts: icon, label, big value (the single
  anchor), a signed+colored delta chip, timeframe, and an inline micro-visual
  (sparkline/mini-bar/donut/progress). Everything but the big value is subordinate.
- **Charts-as-cards, inline-micro-chart by default.** Embed sparklines/mini-bars inside stat cards
  for glanceable trend; reserve a full chart card only when the plot itself is the subject. Keep
  axis furniture sparse and muted; let data ink dominate.
- **Whitespace is relational at density.** Hairline borders, zebra striping, and card edges do the
  separation job a large margin does on a landing page. The unit of breathing room shifts from the
  section gap to the row divider and cell padding.
- **Color is a scarce signal.** Near-monochrome neutral foundation; spend saturated hue only on
  status badges, signed deltas, and the single active/current control — so color always carries
  information.
- **Flat 1px-ring elevation.** Cards/popovers separate via a crisp low-alpha ring + small radius,
  not a soft blurred drop shadow. (Method-pluralism tension with Section 3's two-layer
  ambient+contact ramp: both valid — the ring for dense, tiling, flat UI; the stacked ramp for
  expressive marketing surfaces.)

---

## 7. Application shell & state-as-design (multi-role apps)

A second new domain. Where Section 5 composes *pages* (independent full-page layouts repainted per
route), an application is a **persistent frame plus swappable content**, and its states and roles
are design surfaces in their own right.

- **Shell + content slot.** The shell is three fixed regions (vertical nav rail, top
  header/toolbar, main content). It renders once and survives navigation; only the content slot
  re-renders. Decide up front which chrome is global (shell) vs local (content). Collapsing the
  rail is a *state change*, not a route change or a component swap.
- **One parameterized nav rail.** Build a single rail with orthogonal display-mode
  (expanded / collapsed-icon-only / compact / minimal / detached-floating / with-switcher /
  with-in-nav-search) and content axes — never a forked component per mode. Collapsed keeps
  icons+badges and drops labels (tooltips carry the label), so layout must survive label removal.
- **Grouped nav with count badges.** Labeled semantic sections with a stable slot order (not a
  flat list), each item with an optional trailing count badge so the nav doubles as a status
  surface and role-hiding/future features have predictable insertion points.
- **Permission-matrix as source of truth.** A single explicit matrix (rows = view IDs,
  columns = roles, cells = allowed/denied, plus a global row for everyone) drives menus, route
  guards, and empty/denied states — all *derived*, never hand-curated per role. One app re-skins
  itself per role; this is the application analogue of the commerce world's separate
  guest/customer/admin experiences.
- **Typed empty/loading/error states.** First-class archetypes, one per widget kind
  (passive-data / actionable-first-run / empty-table / generic-widget). All share a skeleton
  (icon → title → support line → optional CTA) but copy and CTA-presence depend on whether the
  *current role* can act. Loading = the same grid filled with placeholder skeletons so layout is
  identical before and after data arrives (no content shift).
- **Tokenize structural metrics, not just color.** Rail width, header height, content padding, and
  radii are named tokens so collapse/expand and responsive breakpoints compute from one source and
  the shell stays aligned with the content grid.
- **Persistent shell + reflowing card grid.** Top KPI band → primary chart row → multi-column
  data/list/table cards. Reflow by collapsing column count (4→2→1) and the rail (rail→drawer) per
  breakpoint; per-card density stays constant — never redesign cards per breakpoint.


---

# Additions from Source 04 (Shopify storefront)

> New: responsive-component discipline + storefront anatomy. (Color/type/space/composition were independently re-confirmed — see VALIDATION.md.)

---

# Additions from Source 04 (warm-retail commerce storefront)

> New method this source justifies: a **responsive-component discipline** (how one component is
> authored across breakpoints), **storefront anatomy** (the component classes an operating shop
> carries), and a **page-skeleton library** (chrome/body split + per-type section stacks).
> Integrated under the existing spine + method-pluralism rules. This source also independently
> re-confirms the two-tier token spine, the two-family type ramp, the 4-based spacing/radius scale,
> the warm-retail color/type register, the named-effect elevation rule, and the band-chassis page
> method — none of which are re-stated here.

---

## 5a. Responsive-component discipline (how ONE component spans breakpoints)

Section 5 composes bands and the method already mandates "author three breakpoints from their own
frames." This adds the missing *component-level* contract: how a single reusable component (header,
footer, nav, composed input) is modelled across those frames.

- **One component set, a `Breakpoint` variant property = {Desktop, Tablet, Mobile}.** Model a
  responsive component as ONE set whose breakpoints are *sibling variants*, not three unrelated
  frames. Each variant is explicitly drawn at a fixed device-width anchor (wide / medium / narrow)
  with a fixed inner container; page padding **steps DOWN** as width narrows, so blocks grow to fill
  the narrower container rather than the gutter shrinking. Identity and tokens are shared; only
  layout changes.
- **Reflow is a priority-ordered set of authored decisions, never emergent flexbox.** In order:
  (1) **Nav collapse threshold** — inline horizontal nav links exist only at the widest breakpoint;
  at the first step down they are removed from the bar entirely and replaced by a hamburger beside
  the logo, with the **bar height held constant**. (2) **Action icons shed by priority** — the
  utility cluster drops lower-priority icons as width shrinks (e.g. 5→4→3), keeping the highest-value
  actions at every breakpoint, survivors unchanged in size and order; never shrink hit targets to
  fit. (3) **Overlay state is co-located** — author the open menu as a hidden child frame *inside the
  same variant*; collapsed nav becomes a full-width accordion (chevron per section) with a pinned
  action footer, and any rich grid re-tiles to fewer columns. (4) **Multi-column blocks follow a
  column ladder** N → N/2 → 1, each block widening step-wise as columns drop while reading order is
  preserved via predictable x/y. (5) **Bands vs grids** — keep band-spanning rows (newsletter /
  section-header + input) full-width at *every* breakpoint while only the columns below re-grid; a
  composed field+button goes from compact fixed-width to a full-width field with the button pinned
  inline. (6) **Bottom utility bar may stack AND reorder** — a right-aligned legal/payment group may
  be promoted *above* the fine print when it stacks on mobile.
- **The throughline:** what changes per breakpoint is **column count, nav disclosure, icon priority,
  and stacking order** — each an explicit decision. Hit-target sizing for interactive controls stays
  constant across all three.

---

## 8. Storefront anatomy (component classes for an operating commerce shop)

A new domain. Source 02 taught *palette as wayfinding* for a shop; this is the *compositional
anatomy* of an operating storefront's chrome and templates — the parts a dashboard, configurator, or
formal library simply do not have. (Only build this layer when the product *is* a transactional
storefront; it's method-pluralism, not a universal requirement.)

- **Header splits into category NAV + a right-pinned UTILITY CLUSTER, modeled as different component
  classes.** The cluster holds, in order, locale/currency → search → offers/promo (often badged) →
  account → cart. Keeping them a distinct class keeps the center nav clean and global affordances
  reachable from every page.
- **The category mega-menu is a two-pane merchandising surface,** not a link list: a descriptor
  category rail beside a featured-product pane. Navigation doubles as product discovery.
- **The product card is a fixed slot stack** (image+optional badge → optional microcopy → swatch row
  → title → price with sale emphasized + struck original) whose **width is bound to a block-size
  token**, so one card serves grids, carousels, cross-sell rails, and mega-menu panes and reflows by
  column count, never by resizing the card. This is the shared atom across home, PLP, PDP cross-sell,
  and cart.
- **The cart has two distinct forms.** A slide-out **drawer** (item count + line items + a
  free-shipping/threshold **progress** indicator; its empty state cross-sells rather than dead-ends)
  and a full cart **page** (a different skeleton — see §9). The threshold-progress line is a
  storefront upsell primitive; never omit it from the drawer.
- **The footer is a physical-retail store-info taxonomy:** parallel columns [shop categories | store
  links | opening hours | contacts+social] + a locale switcher + a legal row + a **payment-badge
  row**. Hours, address, and payment marks signal a legitimate operating business — a different
  contract from a thin link footer.
- **Newsletter capture is a discount-capture block,** not a bare form: a value-led headline naming
  the incentive, one field + submit, and a consent line linking terms/privacy.
- **Trust signals ride one dedicated full-width strip** of icon+label pairs below the nav or hero —
  the scannable node of the page-wide "threaded proof" (Section 5), consolidated rather than
  scattered.
- **Promotions are a layered system of reusable, tokenized primitives:** top banner, moving marquee,
  timed popups (bonus / discount-code), an offers/bundle surface, and a slide-out offers panel — so
  merchandising swaps copy and timing without touching layout.

---

## 9. Page-skeleton library (chrome/body split + per-type section stacks)

The layer *above* Section 5 (which gives the band grammar) and §8 (which gives the component
classes): **which sections, in what order, on which page type.** Store it so one system spans ~10
page types without redundancy.

- **Model every page as `GLOBAL CHROME + BODY STACK`.** Chrome = {promo bar [opt], header/nav [req],
  footer [req]}, authored **once** and template-invariant; each template defines only its body stack.
  Deep/transactional pages prepend a breadcrumb as the first in-body element; the homepage does not.
- **Author section order at desktop and treat it as breakpoint-invariant.** Derive mobile by
  **column-collapse + drawer-izing filters**, never by re-ordering sections. (§5a governs how each
  component inside a section reflows.)
- **Each page type has a named, tagged body stack** (required / recommended / optional):
  - **HOME** — alternate product-discovery bands with trust/story bands: hero+CTA [req] → trust/USP
    ticker [rec] → tab-filterable product rail [req] → lookbook rail [opt] → value-props split [rec]
    → reviews wall [rec] → featured rail [rec] → UGC/shoppable rail [opt] → brand/journal rail [opt]
    → press strip [opt] → newsletter [rec].
  - **PLP/COLLECTION** — breadcrumb [rec] → collection header [req] → subcategory tiles [opt] →
    {filter sidebar [rec] + toolbar(count+sort) [req] + product grid [req] + pagination/load-more
    [rec]} → cross-sell rail [opt]. The **toolbar (count+sort) and the grid are the irreducible
    core**; filters degrade to a mobile drawer with a sticky "Show results" commit bar.
  - **PDP** — breadcrumb [rec] → {gallery [req] | BUYBOX} → rating summary (histogram + media) [rec]
    → review list [rec] → content split [opt] → FAQ accordion [opt] → benefits split [opt] → related
    rail [rec].
  - **CART PAGE** (distinct from the drawer) — breadcrumb → header + incentive bar (free-ship
    progress / urgency) [rec] → {line items + in-cart cross-sell | order-summary(breakdown, total,
    note, checkout CTA, payment badges) + reassurance(privacy/SSL/guarantee)} → cross-sell rail. The
    summary panel is sticky-eligible and bundles total + CTA + payment proof together.
  - **BLOG POST** — breadcrumb → hero image → title+meta → rich body at a constrained measure → tags+
    share → prev/next pager → related posts.
  - **ABOUT/STORY** — hero image → alternating image|text splits → benefits split.
  - **AUTH** — breadcrumb → {form(heading, fields, security line, submit, alt-link) | brand image}.
  - **ACCOUNT DASHBOARD** — breadcrumb → heading+sign-out → stacked editable info blocks (contact,
    address).
  - **LEGAL** — breadcrumb → title → long-form rich text at a constrained measure.
- **Promote the BUYBOX to a named sub-skeleton** with its own strict order, reusable across physical/
  digital/gift-card products: rating+cert badges → title → spec chips → description → price(+discount)
  → variant swatches → option controls(dropdown/segmented/qty) → ATC [req] → payment badges → micro
  trust strip → detail accordions → mini cross-sell. Don't re-derive it per product type.
- **Universal closers.** A cross-sell rail closes nearly every commerce page. Editorial pages (blog/
  about/legal) **constrain the body to a readable measure and end in lateral navigation (related/
  next), never a buy-CTA** — a distinct skeleton family from commerce pages.
