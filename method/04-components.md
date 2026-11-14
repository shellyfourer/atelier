# Component architecture method

> How atelier builds the component layer: the tier of the system where meaning binds to a
> part. Portable construction rules only — no brand values, screens, or client specifics.
> Validation tags `[S0x,…]` cite the independent sources behind each principle (see
> `evidence/VALIDATION.md`); a principle seen in one source is marked `· provisional`.

Components are where the token spine (primitives → semantics) stops being a lookup table and
becomes something you can place. The invariants below are load-bearing across registers;
below them sit the organizing postures (how you cut a kit into pieces) and then the
domain-specific disciplines (responsive, data-density, app-shell) and refinements.

---

## 1. The invariants (true in every register)

These hold whether you are building a formal token library, a storefront, a dashboard, or a
greybox kit.

- **Atom → molecule → organism.** Decompose every part into three altitudes: the bare atom,
  the molecule that bundles an atom with its satellites, the organism that composes molecules
  into a section-scale unit. Build upward; never author a composite as a flat drawing.
  [S01,S03,S05]
- **Name explicit base atoms; instance, never copy.** Tag the primitive (`Cell (Base)`,
  `Field`) and have every higher structure *instance* that base, so one edit propagates. Never
  paste a primitive into each composite. The shared base atom is the single reused unit across
  all the composites that contain it. [S01,S03,S04,S05]
- **Encode the composition ladder in the name.** The atom keeps the bare noun (`Field`); its
  molecule appends a role word (`Field group`) and bundles the atom with its label, helper, and
  affordances. Altitude is readable from the name, and the molecule is the intended unit of
  reuse. [S05 · provisional]
- **States and kinds are variant axes, never forked copies.** One set holds
  default / hover / disabled / error (and kind, where kinds exist) so every state shares
  geometry and tokens and the whole inventory is inspectable in one place. Forking a copy per
  state is the failure this prevents. [S01,S03,S05]
- **Variant sets only where a real axis exists.** Interactive controls and multi-kind cells
  earn a set; a static card or a lone glyph stays a plain component. Do not wrap a single-state
  element in a set for symmetry. [S01 · provisional]
- **One-line usage note on every component** — what it is and when to use it — so the library
  reads as a self-describing API. [S01 · provisional]
- **Strict path taxonomy + function-grouped editor pages.**
  `design_system/<library>/components/<Name>`, with category prefixes for catalog-like items,
  and editor pages grouped by UI function with a stable marker. [S01,S05]

---

## 2. Function is the primary organizing spine

Sort the kit by **UI function** (actions / form elements / text inputs / cards), orthogonal to
any feature, screen, or product. Function-first organization — not feature- or screen-first —
is the structural reason one "teacher" kit stays reusable across unrelated products: nothing in
the component layer knows which app it serves. [S05 · provisional]

---

## 3. Family over mega-component — and where to split

The default posture for any component "need" that is really several jobs.

- **Prefer a family of specialized siblings over one mega-component.** A button need is a
  family — generic action, icon-only, filter, floating-action, selectable — each scoped to one
  job with small, orthogonal axes (size × state), not one set carrying an exploding matrix.
  [S01 · provisional]
- **Family-split and axis-orthogonality are one causal rule.** You split a component into
  job-scoped siblings *precisely so* each sibling's remaining axes stay small and orthogonal
  (size × state — never × shape × role). The test for "split vs. add a variant" is sharp:
  **split the moment two axes stop being orthogonal.** An icon-only button has no content-type
  axis; a filter button has no FAB-elevation axis — so they are siblings, not variants of one
  set. [S05 · provisional]

### Collapse N looks to one themed atom
The inverse discipline, and just as important: when a design shows N visually-distinct
cards or sections, do **not** author N components. Find the invariant skeleton and externalize
the only per-variant delta to a **single data/category token binding**. A five-look product
card is *one* structure whose variant axis is a category binding (accent for chips / rating /
price-add, the paired tint for the card background). Component count stays flat as categories
grow. This is family-splitting's complement: split on orthogonal *axes*, collapse on themeable
*looks*. [S08 · provisional]

### Hoist density/scale to the library level
Do not add a density variant to every component. Ship **parallel libraries** (full + compact)
with *identical* component names; swap the subscribed library to rescale a whole project
losslessly. Density is a library choice, not a per-component axis. [S01 · provisional]

---

## 4. Responsive-component discipline (one component across breakpoints)

The system mandates authoring three breakpoints from their own frames; this is the
component-level contract for how a *single* reusable component (header, footer, nav, composed
input) is modelled across them.

- **One set, a `Breakpoint` variant = {Desktop, Tablet, Mobile}.** Model a responsive component
  as ONE set whose breakpoints are *sibling variants*, not three unrelated frames. Each variant
  is drawn at a fixed device-width anchor with a fixed inner container; **page padding steps
  DOWN** as width narrows, so blocks grow to fill the narrower container rather than the gutter
  shrinking. Identity and tokens are shared; only layout changes. Equivalently: model
  responsive sizing as one semantic role name resolving to breakpoint-specific values — never
  fork a component to change sizes. [S04,S05,S08]
- **Reflow is a priority-ordered set of authored decisions, never emergent flexbox.** In order:
  1. **Nav collapse threshold** — inline horizontal nav exists only at the widest breakpoint; at
     the first step down it is removed from the bar and replaced by a hamburger beside the logo,
     with **bar height held constant**.
  2. **Action icons shed by priority** — the utility cluster drops lower-priority icons as width
     shrinks (5→4→3), survivors unchanged in size and order; never shrink hit targets to fit.
  3. **Overlay state is co-located** — author the open menu as a hidden child frame *inside the
     same variant*; collapsed nav becomes a full-width accordion with a pinned action footer.
  4. **Multi-column blocks follow a column ladder** N → N/2 → 1, each block widening step-wise as
     columns drop, reading order preserved via predictable x/y.
  5. **Bands vs. grids** — band-spanning rows (newsletter, section-header + input) stay
     full-width at *every* breakpoint while only the columns below re-grid.
  6. **Bottom utility bar may stack AND reorder** — a legal/payment group may be promoted above
     the fine print when it stacks on mobile. [S04,S05,S08]
- **The throughline:** what changes per breakpoint is **column count, nav disclosure, icon
  priority, and stacking order** — each an explicit decision. **Hit-target sizing for
  interactive controls stays constant across all three.** [S04,S05,S08]
- **A breakpoint may own net-new organisms**, not just reflowed ones. Promote desktop-inline
  affordances (filter rail, mini-cart, gate, auth) into standalone mobile **overlay / sheet**
  surfaces that are themselves first-class library entries — a bottom-sheet or slide-up has no
  desktop analog and is authored as its own organism, not as a reflow of one. [S03,S08]

---

## 5. Data-density method (tables, dashboards, dense surfaces)

Density **inverts** the marketing-page levers: you cannot push things apart with whitespace or
signal importance with scale, so hierarchy and separation must be *drawn*. This is the
component discipline for cells, tables, and stat cards. [S03 · provisional]

- **Hierarchy by weight + color, not size.** On a tiny type scale (xs/sm), stack a bold
  near-black primary over a muted secondary inside one cell (name over email, value over label).
  Font-weight and foreground-vs-muted color are the two space-free levers that replace a hero's
  32–48px scale jumps.
- **Micro-spacing ramp.** Extend the base spacing scale with fine sub-rungs (2 / 6 / 10 between
  the usual rungs) so cell padding, badge insets, and icon gaps tune tightly while staying
  on-grid. Density is achieved by selecting smaller rungs — never by hardcoding arbitrary gaps.
- **Slot-based tables.** Model the table as three independently toggle-able regions — optional
  toolbar (filters / search / bulk actions), body (header + rows), footer (selection-count +
  pagination) — plus an optional caption, so the same primitive scales from a bare list to a
  full grid.
- **Typed cells with fixed alignment.** Treat cells as a small library: identity (avatar +
  two-line stack), numeric (tabular, right-aligned), status (semantic pill), media/brand, action
  (ellipsis menu). Text/identity left; numbers right with tabular figures; actions right.
- **Reserve interactive slots even when off.** Pre-allocate the selection-checkbox column, the
  sort indicator on sortable headers, the selection-count readout, and pagination, so toggling
  state never reflows the grid.
- **Stat-card grammar — one dominant value.** Optional parts (icon, label, signed+colored delta
  chip, timeframe, inline micro-visual) are all subordinate to the single big value anchor.
- **Charts-as-cards, inline-micro by default.** Embed sparklines / mini-bars inside stat cards
  for glanceable trend; reserve a full chart card only when the plot itself is the subject.
- **Whitespace is relational at density.** Hairline borders, zebra striping, and card edges do
  the separation job a large margin does on a landing page; the unit of breathing room shifts
  from the section gap to the row divider and cell padding.
- **Color is a scarce signal.** Near-monochrome foundation; spend saturated hue only on status
  badges, signed deltas, and the single active control — so color always carries information.
- **Flat 1px-ring elevation.** Cards/popovers separate via a crisp low-alpha ring + small
  radius, not a soft blurred drop shadow (method-pluralism tension with the two-layer
  ambient+contact ramp — ring for dense flat UI, stacked ramp for expressive surfaces).

---

## 6. Application shell & state-as-design (multi-role apps)

Where page composition repaints independent full pages per route, an application is a
**persistent frame plus swappable content**, and its states and roles are first-class design
surfaces. [S03,S06]

- **Shell + content slot.** The shell is three fixed regions (vertical nav rail, top
  header/toolbar, main content). It renders once and survives navigation; only the content slot
  re-renders. Decide up front which chrome is global (shell) vs. local (content). Collapsing the
  rail is a *state change*, not a route change or a component swap. [S03 · provisional]
- **One parameterized nav rail — never a forked component per mode.** Build a single rail with
  orthogonal display-mode axes (expanded / collapsed-icon-only / compact / minimal /
  detached-floating / with-switcher / with-in-nav-search) and content axes. Collapsed keeps
  icons + badges and drops labels (tooltips carry the label), so the layout must survive label
  removal. [S03 · provisional]
- **Grouped nav with count badges.** Labeled semantic sections with a stable slot order (not a
  flat list), each item with an optional trailing count badge — so the nav doubles as a status
  surface and future items have predictable insertion points. [S03 · provisional]
- **Parameterize the shell by ROLE from an explicit view × role access matrix.** A single matrix
  (rows = view IDs, columns = roles, cells = allow/deny, plus a global row for everyone) drives
  menus, route guards, and empty/denied states — all *derived*, never hand-curated per role. One
  permission-driven shell re-skins itself per role; this is the component-architecture analog of
  the token coverage matrix, not N hand-built sidebars. [S03,S06]
- **Treat plan/subscription TIER as a second, orthogonal content axis** on the same shell
  (role × tier), with the upsell/tier affordance as a first-class, consistently-placed
  component. [S06 · provisional]
- **First-class empty / loading / error states — typed, one per widget kind**
  (passive-data / actionable-first-run / empty-table / generic-widget). All share a skeleton
  (icon → title → support line → optional CTA), but copy and CTA-presence depend on whether the
  *current role* can act. Loading = the same grid filled with placeholder skeletons so layout is
  identical before and after data arrives (no content shift). Budget these as their own section
  stacks, not as edge cases bolted onto the happy path. [S03,S06]
- **State-as-enum wired to tokens.** Interactive atoms carry Default / Focus / Invalid /
  Disabled as variant axes: focus pulls the ring token, invalid pulls destructive, disabled
  pulls muted; focus/validation render as a spread box-shadow in the ring color so focus never
  changes the box model (no 1px reflow). [S03 · provisional]
- **Tokenize structural metrics, not just color.** Rail width, header height, content padding,
  and radii are named tokens so collapse/expand and responsive breakpoints compute from one
  source and the shell stays aligned with the content grid. [S03 · provisional]
- **Persistent shell + reflowing card grid.** Reflow by collapsing column count (4 → 2 → 1) and
  the rail (rail → drawer) per breakpoint; **per-card density stays constant** — never redesign
  cards per breakpoint. [S03 · provisional]

---

## 7. Two altitudes of reuse + composition refinements

- **Maintain two altitudes of reuse.** Keep both the **atomic component library** AND **named,
  counted block collections** — contact sheets of pre-composed whole sections (e.g. "Data
  Tables — 8"). The explicit count is a coverage checklist and a maintenance contract; never
  dump finished blocks into the primitives namespace. [S06 · provisional]
- **Compose containers from named slots filled by instance-swap.** Placeholders mark fill
  points so one frame hosts many payloads without a variant explosion — the structural
  complement to the sibling-family rule (split on axes, slot on payload). [S06 · provisional]
- **Let reused primitives serve double duty** — both documentation chip and live UI primitive —
  so docs can't drift from the token; the system eats its own dog food. [S06 · provisional]

---

## 8. The greybox / wireframe kit (a legitimate construction method)

A deliberately un-styled, monochrome component library whose entire value is **structure** —
slot layout, variant inventory, naming — with tokens intentionally neutral for downstream
re-skinning. Low aesthetic commitment is the *method*, not an unfinished system: it ships the
architecture decoupled from any look, so one structural library can parent several styled
systems. Keep the three surfaces separated: a token/foundation sheet, a true-component library
of reusable symbols, and composed layout sections/page skeletons. [S05 · provisional]
