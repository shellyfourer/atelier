# Source 03 — method notes (dashboard / shadcn+Tailwind)

> Anonymized. A data-dense product dashboard built on a shadcn/ui + Tailwind atom system. Teacher, not template: method only, no client palette/fonts/copy/screens. Its value is being a *third* construction method distinct from Source 01 (formal ramp library) and Source 02 (lean category-color commerce) — plus the data-density and app-shell dimensions neither prior source covered.

# Source 03 — method notes (third source)

_Confidence: high (direct study of a token layer, an atom library with variant matrices,
light/dark twin frames, a data-table + stat-card system, and an app shell with a role matrix)._

A copy-paste atom system built on a **semantic-CSS-variable** token method (shadcn/Tailwind
lineage) for a **data-dense, multi-role dashboard application**. Studied as a *teacher*: its
value is that it inverts nearly every lever the first two sources taught. Sources 01 and 02 were
both **page systems** — marketing/commerce surfaces that make *one thing dominate* with large
type, generous whitespace, hero scale jumps, and decorative color. Source 03 is an **application
system**: hundreds of data points per screen, hierarchy by weight not size, whitespace replaced
by hairlines, color demoted to a scarce signal, and chrome that persists across navigation. No
specifics copied — method only.

**Portable vs discard.** Portable = the thin-semantic-layer token method (a third, co-equal
option under method pluralism); the data-density method (micro-spacing ramp, weight-over-size
hierarchy, slot-based tables, typed cells, stat-card grammar, flat ring elevation,
borders-as-whitespace, color-as-signal); and the app-shell/state method (persistent shell +
content slot, one role-and-mode-parameterized nav rail, permission-matrix-as-source-of-truth,
typed empty/loading/error states, tokenized structural metrics). Discard = the specific
near-black/near-white values, the font family, the base radius number, the exact spacing rungs,
the role names, the view IDs, and all domain/product vocabulary. Learn *that* a translucent ring
token exists; forget its exact color.

## What makes this source a useful contrast to Sources 01 & 02

| Dimension | Sources 01 & 02 (page systems) | Source 03 (app system) | Lesson for atelier |
|---|---|---|---|
| Token method | Ramp/category primitives, exposed to components (pick a 500, a category base) | **Thin semantic layer is the *only* component-facing interface**; the ramp lives underneath, never referenced in a component | A third legitimate token method. Components speak only in roles (primary/foreground/muted/ring). |
| Dark mode | Re-select different ramp steps per element | **Same semantic name, different value per mode** — light/dark as twins | Theme by value-mode, not by forking components or naming a second palette. |
| Spacing | Coarse 8/16/24 marketing ramp, whitespace = large gaps | **Micro-spacing ramp (sub-rungs: 2/6/10)**; whitespace replaced by hairlines + striping + card edges | Density is a spacing problem first; add sub-rungs and *draw* separation you can't afford to leave empty. |
| Hierarchy | Size jumps (32–48px) signal importance | **Weight + muted-vs-foreground color** on a tiny 12/14px scale | At density, scale is unaffordable; two space-free levers remain. |
| Color | Brand decoration, category wayfinding | **Scarce semantic signal** — hue only on status, trend deltas, the single active control | When hundreds of points share a screen, decorative color is noise. |
| Elevation | Two-layer ambient+contact shadow ramp | **Flat 1px ring** (zero-offset, 1px spread, low-alpha) | Soft shadows stack badly across tiling cards; flat ring reads correctly at high card counts. |
| Structure | Page = independent full-page layouts, repainted per route | **Persistent shell + swappable content slot**; one app re-skins per role | Applications need continuity and role adaptation; pages don't. |

## Method principles learned here

### A. The thin-semantic-layer token method (a third token option)

- **Two tiers, but the semantic layer is *thin and closed* and the only thing components
  touch.** A primitive ramp (full numeric color scales, spacing scale, type scale) sits
  *underneath* a small set of role tokens; components bind only to roles and never to a ramp
  step. *Why:* separating "what a color is" from "what it means" lets you re-skin by editing one
  small map. (This is the spine's two-tier rule, but far thinner at the top than Source 01's rich
  semantic matrix — a deliberately minimal role set, not an exhaustive Role×Prominence×Context
  grid.)
- **Role tokens come in foreground/background pairs.** Every "on-X" foreground ships with its "X"
  background (surface pairs, an action pair, quiet pairs, a status pair, chrome roles:
  border/input/ring). *Why:* contrast travels *with* the token, so legibility is guaranteed under
  any theme and the token set reads as intent, self-documenting.
- **Theme by value-mode on one name.** Light and dark are twin frames sharing identical role
  names; only each token's resolved value changes between modes. *Why:* one component definition
  serves every theme — adding a theme is adding a value column, not a component variant. This is
  the single biggest divergence from a ramp system's per-element dark mode.
- **One radius knob derives the whole system.** A single base-radius token feeds every corner;
  named steps resolve from it. *Why:* sharp-vs-soft becomes one global dial. (Note the
  method-pluralism tension with Source 01's size-keyed per-component radius: both valid — the one
  knob suits a flat, uniform-radius app idiom, the size-keyed ramp suits an expressive component
  family; choose by product.)
- **Channel-split colors so one token yields solid + translucent uses.** Store color as bare
  channels; apply alpha at use-site, so a focus ring and its invalid variant are the same color
  at reduced opacity. *Why:* a frozen hex can't spawn a translucent ring — channel-splitting means
  one token covers fills, borders, *and* rings without new tokens.
- **State is a variant enum wired to tokens, and the ring is a box-shadow, not a border.** The
  atom carries Default/Focus/Invalid/Disabled (× Size × fill axis); focus pulls the ring token,
  invalid pulls destructive, disabled pulls muted — and focus/validation render as a spread
  box-shadow in the ring color. *Why:* every state re-themes automatically and the state surface
  is enumerable/testable; shadow-spread rings keep the box model stable on focus (no 1px reflow).
- **Own the atom; the contract is the names.** Atoms ship as source you paste and bind to your
  tokens, not as a versioned black-box dependency. *Why:* portability is the naming contract
  (primary, foreground, ring, radius), so any project honoring the names gets consistent,
  re-skinnable components with no upgrade lock-in.

### B. The data-density method (the inverse of a marketing hero)

- **Micro-spacing ramp.** Add sub-rungs (2/6/10 alongside the usual rungs) so cell padding, badge
  insets, and icon gaps tune tightly without leaving the grid. Density is achieved by selecting
  smaller rungs, never by hardcoding arbitrary gaps.
- **Hierarchy by weight + color, not size.** Stack a bold near-black primary over a muted
  secondary inside one cell (name over email, value over label) on a tiny type scale. Font-weight
  and foreground-vs-muted are the two space-free levers that replace scale jumps.
- **The data table is a slot-based component, not a monolith.** Three independently toggle-able
  regions: an optional toolbar (filters/search/bulk actions), the table body (header + rows), and
  a footer (selection-count readout + pagination), plus an optional caption. The same table
  scales from a bare list to a full grid.
- **Cells are a typed library with fixed alignment rules.** Recurring archetypes — identity
  (avatar + two-line stack), numeric (tabular, right-aligned), status (semantic pill), media/brand
  (logo/thumbnail), action (ellipsis menu). Identity/text left, numbers right (tabular figures),
  actions right. *Why:* scanability in a dense grid depends on predictable typed cells and
  column alignment.
- **Reserve every interactive slot even when off.** A selection-checkbox column, a sort indicator
  on sortable headers, a selection-count readout, and pagination (Previous / numbered / Next with
  the current page as the *only* filled chip) all have pre-allocated space, so toggling state never
  reflows the grid.
- **Stat/KPI cards follow a fixed grammar: one dominant value, everything else subordinate.**
  Optional parts — icon, label, big value, signed+colored delta chip, timeframe, and an *inline*
  micro-visual (sparkline/mini-bar/donut/progress). The big value is always the single anchor.
- **Charts are cards with consistent chrome, and inline-micro-chart is the default.** Embed
  sparklines/area fills/mini-bars inside stat cards for glanceable trend; reserve a full chart
  card only when the plot itself is the subject. Keep axis furniture sparse and muted; let data
  ink dominate.
- **Whitespace is relational at density.** Hairline borders, zebra striping, and card edges do the
  job a 96px margin does on a landing page. The unit of breathing room shifts from the section gap
  to the row divider and cell padding.
- **Color is a scarce signal.** Near-monochrome neutral foundation; spend saturated hue only on
  status badges, signed trend deltas, and the single active/current control. Color always carries
  information so the eye can trust it.
- **Flat 1px-ring elevation.** Cards/popovers sit on the surface via a crisp low-alpha ring +
  small radius, not a soft blurred drop shadow. (Method-pluralism tension with Source 01's
  two-layer ambient+contact ramp: both valid; the ring idiom is correct *for dense, tiling, flat
  UI*, the stacked-shadow ramp for expressive marketing surfaces — choose by product.)

### C. The app-shell / state-as-design method (application, not page)

- **Model the product as a persistent shell + a swappable content slot.** The shell = three fixed
  regions (vertical nav rail, top header/toolbar, main content). The shell renders once and
  survives navigation; only the content slot re-renders. Decide up front which chrome is global
  (shell) vs local (content). *Why:* an app needs continuity — state (collapsed nav, active
  workspace, auth) persists and the frame never flashes. Naming the shell/slot boundary is what
  makes it an app, not a collection of pages.
- **One nav rail, parameterized by orthogonal display-mode and content axes.** Modes
  (expanded / collapsed-icon-only / compact / minimal / detached-floating / bordered /
  with-switcher / with-in-nav-search) are a *prop*, never a forked component. Collapsed keeps
  icons+badges and drops labels (tooltips carry the label), so layout must survive label removal.
- **Group nav into labeled semantic sections with a stable slot order; items carry count
  badges.** Flat nav doesn't scale past ~5 items; grouping gives a mental map and stable insertion
  points for role-based hiding and future features. Badges make the nav a status surface.
- **Drive per-role UI from a single explicit permission matrix; the sidebar is a pure projection
  of it.** Rows = view IDs, columns = roles, cells = allowed/denied, plus a global row for
  everyone. Menus, route guards, and empty/denied states all *derive* from the matrix — never
  hand-curate each role's menu. *Why:* ad-hoc role adaptation drifts (a visible link a role can't
  open, a guard that disagrees with the menu). One matrix keeps visibility, guards, and states
  consistent by construction and auditable in one artifact. This is the biggest new concept vs. a
  commerce system (which splits guest/customer/admin across separate experiences rather than one
  app that re-skins per role).
- **Empty/loading/error are first-class typed archetypes, one per widget kind.** Distinct empties
  — passive-data (no action), actionable first-run (+ primary CTA), empty-table, generic-widget —
  share a skeleton (icon → title → support line → optional CTA) but copy and CTA-presence depend
  on whether *this role* can act. Loading = the same card grid filled with placeholder skeletons
  so layout is identical before and after data. *Why:* in a data app the empty/error state is the
  *first* thing many users see; typing them per widget kind makes degradation predictable and
  prevents dangling CTAs for roles that can't create.
- **Tokenize structural metrics, not just color.** Rail width, header height, content padding, and
  radii are named tokens. *Why:* collapse/expand and responsive breakpoints compute from one
  source, keeping shell and content grid aligned as dozens of screens accrete.
- **Lay the screen out as persistent shell + reflowing card grid.** Top KPI band → primary chart
  row → multi-column data/list/table cards. Reflow by collapsing column count (4→2→1) and the rail
  (rail→drawer) per breakpoint; per-card density stays constant — never redesign cards per
  breakpoint.

## Anti-slop rules learned / reinforced here

**Token method (the thin semantic layer):**
- Don't reference a ramp step (a "600", a "-foreground-900") directly in a component — bind to a
  role token. A numeric scale step in a component means the semantic layer was bypassed.
- Don't create parallel light/dark component variants or a `dark-` prefixed palette. Dark is a
  value mode on the same names; a second component or palette name is the ramp-era tell.
- Don't ship a foreground without its paired background (or vice versa). Orphan "on-color" tokens
  break the contrast guarantee.
- Don't store colors as frozen hex when you need tints/rings — keep channels so alpha variants
  (rings, overlays, disabled) derive from one token.
- Don't invent a new semantic token per component. The set is small and closed; a new role must be
  a new *meaning*, not a new appearance. Resist `card-button-border` sprawl.
- Don't implement focus/invalid as a layout border that changes box size — use a ring
  (shadow-spread) token so focus never reflows.
- Don't treat the component library as a black-box dependency themed via overrides; own the atom
  source and theme through the token names.

**Data density:**
- Never signal importance with large type in a dense view — reach for weight + muted-color on the
  existing 12/14px scale instead of a 24px+ font.
- Never hardcode cell padding/badge insets as arbitrary px; pull from the micro-spacing ramp.
- Never left-align numeric columns or use proportional figures — right-align, tabular.
- Never build the table as one hardcoded block — toolbar/body/footer are separate, toggle-able
  regions with checkbox/sort slots pre-reserved so turning them on causes no reflow.
- Never scatter saturated color for decoration — reserve hue for status, signed deltas, and the
  single active control.
- Never float dense cards with soft/blurred drop shadows — use a 1px ring + small radius.
- Never give every chart its own full card — inline micro-charts by default; full chart cards only
  when the plot is the subject.
- Never separate dense rows with empty margin you don't have — use hairlines, striping, card edges.
- Never let a KPI card have two competing focal points — exactly one dominant value.
- Never redesign cards per breakpoint — keep density constant; reflow column count and the rail.

**App shell / state:**
- Don't build one sidebar per role or per display mode — one rail parameterized by
  (role, display-mode, active-page); roles subtract/reorder from a shared definition, modes change
  density/placement.
- Don't let the menu and access control disagree — a link visible to a role must open to a
  permitted state; both derive from the same matrix.
- Don't ship a blank or spinner-only empty/loading state — every widget kind needs a typed empty
  (icon + title + support line) and a loading skeleton matching its final layout; show a CTA only
  when the current role can perform the action.
- Don't re-render the shell on navigation — nav rail, header, and user footer persist; only the
  content slot swaps. Collapsing the rail is a state change, not a route change.
- Don't hardcode shell metrics — rail width, header height, content padding, radii are named
  tokens.
- Don't treat count/notification badges as decoration — they must reflect real per-destination
  state and clear when addressed.
- Don't flatten navigation into one long list — group into labeled sections with a stable slot
  order.
