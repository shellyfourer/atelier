# atelier — validation ledger

> How strongly is each principle validated? A principle confirmed by many independent sources
> is **load-bearing**; one seen once is **provisional**. This ledger makes the strength of the
> system auditable, and it is updated every time a source is analyzed. The goal is maximum
> independent confirmation — confirmation is a first-class output, not repetition.

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

_(Sources A/B/C/06 pending analysis — ledger will grow as each lands.)_

---

## Principle validation

### Spine (cross-layer)
| Principle | Sources | Tier |
|---|---|---|
| Two hard tiers: primitive (value) → semantic (intent); components bind to semantic only | S01, S03, S04 | 🟢 Load-bearing |
| One mental model / naming grammar across all token domains | S01, S04 | 🟡 Corroborated |
| Name by intent at semantic tier, by value at primitive tier | S01, S03, S04 | 🟢 Load-bearing |
| Document to teach (explain → show → apply) | S01, S04 | 🟡 Corroborated |
| Method pluralism — no single correct system (choose per project) | S01⟂S02⟂S03 (by contrast) | 🟢 Load-bearing |

### Color
| Principle | Sources | Tier |
|---|---|---|
| Family → Ramp → Step naming hierarchy | S01, S04 | 🟡 Corroborated |
| One fixed step ladder shared across all ramps (e.g. 25…950) | S01, S04 | 🟡 Corroborated |
| Multiple named sibling ramps per family (not one ramp per hue) | S01, S04 | 🟡 Corroborated |
| Per-step measured WCAG contrast + pass/fail on every swatch | S01, S04 | 🟡 Corroborated |
| Semantic/alias layer resolves to ramp steps (no loose hexes) | S01, S03, S04 | 🟢 Load-bearing |
| Anchor step varies per ramp, encoded in the name | S01, S04 | 🟡 Corroborated |
| Category-color method (taxonomy as palette) | S02 | 🟠 Provisional |
| Thin-semantic token method (theme-by-mode on one name) | S03 | 🟠 Provisional |
| Foreground/background pairing (on-solid certified) | S03, S04 | 🟡 Corroborated |
| Warm register: drift dark end warm, surfaces from 25/50 steps | S04 | 🟠 Provisional |

### Typography
| Principle | Sources | Tier |
|---|---|---|
| Composite type token (size+line-height+tracking+weight+spacing bundled) | S01, S03, S04 | 🟢 Load-bearing |
| Role × size matrix + independent weight axis | S01, S04 | 🟡 Corroborated |
| Optical laws as functions (tracking ∝ size; line-height inverse) | S01, S04 | 🟡 Corroborated |
| Single-family vs role-assigned multi-typeface (method choice) | S01/S04 vs S02 | 🟡 Corroborated |

### Space / Radius / Elevation
| Principle | Sources | Tier |
|---|---|---|
| 4-based spacing scale; separate semantic gap tokens | S01, S04 | 🟡 Corroborated |
| Pill radius reserved for buttons/tags/avatars; larger radius for cards | S02, S04 | 🟡 Corroborated |
| Named/tokenized effect styles over ad-hoc shadows | S01, S04 | 🟡 Corroborated |
| Single global radius knob (flat app idiom) | S03 | 🟠 Provisional |
| Two-layer (ambient + contact) shadow ramp | S01 | 🟠 Provisional |

### Components
| Principle | Sources | Tier |
|---|---|---|
| Atom → molecule → organism decomposition | S01, S03 | 🟡 Corroborated |
| States as variant axes, not separate components | S01, S03 | 🟡 Corroborated |
| Shared base atom reused across composites | S01, S03, S04 | 🟢 Load-bearing |
| Responsive-component discipline (authored per breakpoint) | S04 | 🟠 Provisional |
| State-as-enum wired to tokens (focus→ring, invalid→destructive) | S03 | 🟠 Provisional |

### Page composition
| Principle | Sources | Tier |
|---|---|---|
| Density oscillation (alternate tall/dense with short/calm bands) | S01, S04 | 🟡 Corroborated |
| Grid-break-as-narrowing (break grid by narrowing, not widening) | S01, S04 | 🟡 Corroborated |
| Threaded social proof (distribute, don't clump) | S01, S04 | 🟡 Corroborated |
| Repeating section-header grammar | S01, S04 | 🟡 Corroborated |
| Data-density composition (weight-not-size, tabular figures) | S03 | 🟠 Provisional |

---

## How to update this ledger

When a source is analyzed, for each of its CONFIRMS add the source ID to the matching row and
bump the tier if the count crosses a threshold. For each NEW finding, add a new 🟠 Provisional
row. Never silently drop a provisional — it stays until a second source either confirms it
(→ 🟡) or a source contradicts it (note the conflict explicitly).
