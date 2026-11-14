# atelier — validation ledger

> How strongly is each principle validated? A principle confirmed by many independent sources
> is **load-bearing**; one seen once is **provisional**. This ledger makes the strength of the
> system auditable, and it is updated every time a source is analyzed. The goal is maximum
> independent confirmation — confirmation is a first-class output, not repetition.

**Corpus v1: 8 Figma sources analyzed** (7 full/delta + 1 re-run after a read-block). Spanning
formal token library, commerce configurator, shadcn dashboard, warm storefront, app-leaning
store, brand-dominant storefront, a reproducibility twin, and a high-chroma catalog. The spine,
method-pluralism, 4 color postures, composite type tokens, atom→organism, and the four
composition laws are now **load-bearing** (3–5 independent sources each). A void source (invalid
key) is **confirmation-neutral** — it never moved a tier (see `evidence/PROCESS-NOTES.md`).

## Confidence tiers

| Tier | Meaning | Rule of thumb |
|---|---|---|
| **🟢 Load-bearing** | Independently confirmed by 3+ sources | Trust it; build on it. |
| **🟡 Corroborated** | Confirmed by 2 sources | Solid; watch for edge cases. |
| **🟠 Provisional** | Seen in 1 source | Keep; flag as unconfirmed until a second source validates. |

## Source legend

| ID | Register / kind | Method character |
|---|---|---|
| S01 | Large formal token library | Tonal-ramp, exhaustive, formal |
| S02 | Lean commerce configurator | Category-color, multi-typeface, pragmatic |
| S03 | Product dashboard (shadcn/Tailwind) | Thin-semantic tokens, data-density, app-shell |
| S04 | Shopify storefront (warm retail) | Tonal-ramp (warm), responsive-component, storefront anatomy |
| S05 | App-leaning store (shadcn admin register) | Thin-semantic stacked on ramp; alpha-ramp tokens; greybox method |
| S06 | Brand-dominant storefront | 4th color posture (brand hue as surface); color-blocking composition; rich page skeletons |
| S07 | Formal twin of S01 (delta/validation) | Reproduces S01's method; adds the tokenized grid/layout system |
| S08 | Playful games/party retail (high-chroma catalog) | Category-color enriched ({accent,tint} pairs, scope-theming); four-track page anatomy |

_(Corpus v1 complete: 8 sources analyzed. Live-site / WordPress sources are future additions.)_

> **S07 is a reproducibility check:** an independent twin of S01 that confirms S01's spine,
> composite type tokens, Family→Ramp→Step, and component library are reproducible — strong
> evidence the method is real, not one file's artifact. Its CONFIRMS bump S01-only rows below.

### Revisions log
Principles that a later source downgraded, upgraded, or reframed (not just confirmed):
- **Letter-spacing on display** — *reframed* by S05 from a law ("strongly negative on large display")
  to a **register knob**: default 0 for neutral/technical brands; negative only for editorial/luxury.
- **Color methods (A/B/C)** — *reframed* by S05 from a mutually-exclusive **choice** to composable
  **tiers**: an app register stacks thin-semantic (C) on top of a ramp primitive library (A).

---

## Principle validation

### Spine (cross-layer)
| Principle | Sources | Tier |
|---|---|---|
| Two hard tiers: primitive (value) → semantic (intent); components bind to semantic only | S01, S03, S04, S05, S06 | 🟢 Load-bearing |
| Method pluralism — color posture is register-selected (4 postures now evidenced) | S01⟂S02⟂S03⟂S06 | 🟢 Load-bearing |
| Color is a scarce signal — ration saturated hue (holds on neutral AND high-chroma grounds) | S02, S06 | 🟡 Corroborated |
| One mental model / naming grammar across all token domains | S01, S04 | 🟡 Corroborated |
| Name by intent at semantic tier, by value at primitive tier | S01, S03, S04 | 🟢 Load-bearing |
| Document to teach (explain → show → apply) | S01, S04 | 🟡 Corroborated |
| Method pluralism — no single correct system (choose per project) | S01⟂S02⟂S03 (by contrast) | 🟢 Load-bearing |

### Color
| Principle | Sources | Tier |
|---|---|---|
| Family → Ramp → Step naming hierarchy | S01, S04, S07 | 🟢 Load-bearing |
| One fixed step ladder shared across all ramps (e.g. 25…950) | S01, S04, S07 | 🟢 Load-bearing |
| Multiple named sibling ramps per family (not one ramp per hue) | S01, S04 | 🟡 Corroborated |
| Per-step measured WCAG contrast + pass/fail on every swatch | S01, S04 | 🟡 Corroborated |
| Semantic/alias layer resolves to ramp steps (no loose hexes) | S01, S03, S04, S05 | 🟢 Load-bearing |
| Anchor step varies per ramp, encoded in the name | S01, S04 | 🟡 Corroborated |
| Category-color method (taxonomy as palette) — one option, NOT a storefront default | S02, S08 (S06 contra-indicates as default) | 🟡 Corroborated |
| Category = paired {accent, tint} tokens (mini-ramp per category) | S08 | 🟠 Provisional |
| Category accent is scope-based theme channel (chrome=brand, content=category, else fallback) | S08 | 🟠 Provisional |
| Item-scope accent binding → mixed lists self-theme into a taxonomy legend | S08 | 🟠 Provisional |
| Register-tuned chroma quarantined to the category layer (ramp/type/chrome constant) | S08 | 🟠 Provisional |
| **Brand-dominant color posture (D): brand hue as primary full-bleed surface** | S06 | 🟠 Provisional |
| Color-blocking as composition lever (color-field boundary = section boundary) | S06 | 🟠 Provisional |
| Dual-ground foreground PAIRS as first-class peers (on-light / on-brand) | S06 | 🟠 Provisional |
| Accent chosen for chromatic distance FROM the brand hue (high-chroma register) | S06 | 🟠 Provisional |
| Thin-semantic token method (theme-by-mode on one name) | S03, S05 | 🟡 Corroborated |
| Foreground/background pairing (on-solid certified) | S03, S04, S05 | 🟢 Load-bearing |
| Warm register: drift dark end warm, surfaces from 25/50 steps | S04 | 🟠 Provisional |
| **Color methods are composable TIERS, not either/or (app = C-on-A)** | S05 | 🟠 Provisional |
| Tier encoded in token name (library prefix vs bare role) | S05 | 🟠 Provisional |
| Thin layer scales by bounded SUB-namespaces (chart, sidebar) not a flat list | S05 | 🟠 Provisional |
| Full status quartet (info/success/warning/destructive) as roles | S05 | 🟠 Provisional |
| Alpha-ramp token family (one base × opacity), orthogonal to lightness | S05 | 🟠 Provisional |
| Translucent border = foreground-at-low-alpha (survives any surface/mode) | S05 | 🟠 Provisional |
| Adopt-don't-author primitives in app register (craft → semantic tier) | S05 | 🟠 Provisional |

### Typography
| Principle | Sources | Tier |
|---|---|---|
| Composite type token (size+line-height+tracking+weight+spacing bundled) | S01, S03, S04, S05, S08 | 🟢 Load-bearing |
| Role × size matrix + independent weight axis | S01, S04, S05, S08 | 🟢 Load-bearing |
| Breakpoint-scoped type variant (swap whole composite, not fluid-scale one property) | S04, S05, S08 | 🟢 Load-bearing |
| Typeface as a 3rd semantic axis (≤3 faces partitioned structure/reading/action) | S02, S08 | 🟡 Corroborated |
| Line-height inverse to size (tight display, loose body) | S01, S04, S05 | 🟢 Load-bearing |
| Letter-spacing — register knob, NOT a fixed law (see Revisions log) | S01/S04 (law) → S05 (reframed) | 🟡 Corroborated (reframed) |
| Single-family vs role-assigned multi-typeface (method choice) | S01/S04 vs S02, S05 | 🟢 Load-bearing |
| Semantic-ordinal role naming (H1/H2, Title 1/2…) as valid second axis label | S05 | 🟠 Provisional |
| Line-height 1.0 for single-line centered roles (buttons/nav/chips) | S05 | 🟠 Provisional |

### Space / Radius / Elevation
| Principle | Sources | Tier |
|---|---|---|
| 4-based spacing scale; separate semantic gap tokens | S01, S04 | 🟡 Corroborated |
| Pill radius reserved for buttons/tags/avatars; larger radius for cards | S02, S04 | 🟡 Corroborated |
| Named/tokenized effect styles over ad-hoc shadows | S01, S04 | 🟡 Corroborated |
| Single global radius knob (flat app idiom) | S03 | 🟠 Provisional |
| Two-layer (ambient + contact) shadow ramp | S01 | 🟠 Provisional |

### Grid & layout
| Principle | Sources | Tier |
|---|---|---|
| Grid is a token system; breakpoint is the top axis (each tier a full independent grid) | S07 | 🟠 Provisional |
| Container derived: margin = (device − container)/2; content column not hand-placed | S07 | 🟠 Provisional |
| Gutter tokenized per (breakpoint × column-count); column count is a per-tier set | S07 | 🟠 Provisional |
| Gutters/margins draw from the shared spacing scale (grid inherits global rhythm) | S01/S04 (spacing) + S07 (grid) | 🟡 Corroborated |
| Three independent padding families (device margin / container inset / section spacing) | S04 (section/container) + S07 | 🟡 Corroborated |
| Container capped + centered on desktop; edge-to-edge (margin→0) on mobile | S07 | 🟠 Provisional |

### Components
| Principle | Sources | Tier |
|---|---|---|
| Atom → molecule → organism decomposition | S01, S03, S05 | 🟢 Load-bearing |
| States as variant axes, not separate components | S01, S03, S05 | 🟢 Load-bearing |
| Shared base atom reused across composites | S01, S03, S04, S05 | 🟢 Load-bearing |
| Function is the PRIMARY organizing spine of a component kit | S05 | 🟠 Provisional |
| Family-split the moment two axes stop being orthogonal | S05 | 🟠 Provisional |
| Responsive-component discipline (authored per breakpoint) | S04, S05, S08 | 🟢 Load-bearing |
| Breakpoints may own net-new organisms (bottom-sheet, slide-up) — not pure reflow | S03, S08 | 🟡 Corroborated |
| State-as-enum wired to tokens (focus→ring, invalid→destructive) | S03 | 🟠 Provisional |
| Greybox/wireframe kit — architecture decoupled from skin (5th method) | S05 | 🟠 Provisional |

### Page composition
| Principle | Sources | Tier |
|---|---|---|
| Density oscillation (alternate tall/dense with short/calm bands) | S01, S04, S05, S06 | 🟢 Load-bearing |
| Grid-break-as-narrowing (break grid by narrowing, not widening) | S01, S04, S05, S06 | 🟢 Load-bearing |
| Threaded social proof (distribute; rides the reserved accent in colorful registers) | S01, S04, S05, S06 | 🟢 Load-bearing |
| Repeating section-header grammar (standardized Section-Header organism) | S01, S04, S05, S06 | 🟢 Load-bearing |
| Surface-weight as a 2nd density axis (never stack two saturated full-bleed bands) | S06 | 🟠 Provisional |
| Parameterized app-shell from a view×role access matrix (not N sidebars) | S06 | 🟠 Provisional |
| Two altitudes of reuse: atomic library + named COUNTED block collections | S06 | 🟠 Provisional |
| Named SLOTS filled by instance-swap (avoid container variant explosion) | S06 | 🟠 Provisional |
| Decision-ordered section sequence; hero-as-stage; flip-the-split | S01, S04, S05 | 🟢 Load-bearing |
| Data-density composition (weight-not-size, tabular figures) | S03 | 🟠 Provisional |
| Convince/convert PURPOSE alternation (distinct from density oscillation) | S05 | 🟠 Provisional |
| Section order is breakpoint-invariant (reflow by column-collapse only) | S05 | 🟠 Provisional |
| Hero copy composed into image negative space (not scrimmed overlay) | S05 | 🟠 Provisional |

---

## How to update this ledger

When a source is analyzed, for each of its CONFIRMS add the source ID to the matching row and
bump the tier if the count crosses a threshold. For each NEW finding, add a new 🟠 Provisional
row. Never silently drop a provisional — it stays until a second source either confirms it
(→ 🟡) or a source contradicts it (note the conflict explicitly).
