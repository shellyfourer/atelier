# Space, sizing, radius, elevation, and the grid/layout system

> One number line governs the whole frame: the gaps between things, the insets inside things, the
> fixed dimensions of things, the roundness of their corners, the depth they float at, and the
> columns the page is built on. All of it resolves to a single cadence, exposed through the
> two-tier spine (value-named primitives → semantic aliases → component-scoped tokens). Nothing in
> this layer invents a bespoke number. This chapter states the load-bearing invariants first, then
> the posture choices (where more than one legitimate method exists), then the refinements.

---

## 1. The spacing cadence (load-bearing)

**One base unit; three parallel axes.** Generate every dimension as an integer multiple of a
single small base, then keep three role-named axes running in parallel even though they share one
number line [S01,S04]:

- **spacing** — gaps *between* sibling elements,
- **padding** — inset *within* a container,
- **size** — fixed element dimensions.

Hold them apart so "all internal padding" and "all inter-element spacing" can each be reasoned
about — and later diverge — independently. Collapsing them into one axis forecloses that move.

**Name primitives by literal value**, not by index (`spacing-4`, `padding-20`) [S01,S04] — self-
documenting, collision-free, and insertable without renumbering the scale.

**Three tiers, per the spine:** value-named primitives → **t-shirt semantic aliases**
(`spacing-small / large / 2x-large`) → **component-scoped tokens** that bind one part to a
primitive and quarantine its quirks (`button-radius`, `input-field-width`). Always mint explicit
**`*-none` tokens** so "intentionally square / flush / zero-gap" is a deliberate, named choice
rather than an absent value.

**Semantic gap tokens are first-class** — the gap language (small/large/…) is exposed as its own
alias set so layout code reaches for a role, never a raw multiple [S01,S04].

---

## 2. Sizing

Sizing is the third axis of the same cadence (above): fixed element dimensions resolve to the same
base-unit multiples as spacing and padding, surfaced as value-named primitives and, where a part
owns a dimension, as a **component-scoped token** (`input-field-width`) that isolates that part's
quirk from the shared scale. The discipline is identical to spacing — the only difference is what
the number governs (an element's own extent, not the space around or inside it).

---

## 3. Radius

Radius draws from the same number line and is tokenized, never ad-hoc — but there are **two
legitimate postures**, and the choice is a product decision, not a default.

**Posture A — size-keyed radius (expressive component families).** Reject a single global radius.
Tiny chips get a hair of radius, buttons a little more, large blocks often zero. **Key the radius
token's name to the component's size** so radius tracks element scale by rule rather than by
eyeball. A useful default distribution: **pill radius reserved for small interactive atoms**
(buttons, tags, avatars) and a **larger fixed radius for cards and panels** [S02,S04].

**Posture B — single radius knob (flat, uniform app idiom).** A single base-radius token derives
every corner; named steps resolve *from* it [S03 · provisional]. One knob re-rounds the whole
system at once. This suits a flat, tiling, uniform app register where corners want to move in
lockstep.

**Choosing between them:** the size-keyed ramp suits an expressive component family where radius is
part of the voice; the single-knob form suits a flat app idiom where uniformity is the voice. Both
obey the spine; both ship a `radius-none`. Pick by product register and state why in the brief.

---

## 4. Elevation

Elevation is a tokenized, role-mapped ramp (never one-off shadows) [S01,S04]. As with radius, the
**shape** of that ramp is a posture choice keyed to register.

**Shared invariants (both postures):**
- **Elevation is a named/tokenized effect style**, never an inline ad-hoc shadow — a documented
  ramp (1…N), each level bound to a roster [S01,S04].
- **Geometry scales monotonically.** As the level rises, y-offset, blur, and spread grow together,
  keeping the ramp perceptually ordered.
- **Bind each level to a documented component/state roster** (resting cards, buttons, menus,
  dropdowns, modals) so z-depth is a system-wide contract, not an eyeball judgement call per use.
- **Tint pulls from a tiny set of alpha-only color tokens**, so the whole system re-tints — or
  dark-mode-inverts — from two or three values rather than per-shadow edits.

**Posture A — two-layer ambient + contact (expressive / marketing surfaces).** Each level stacks
**two shadows**: a soft ambient layer (large blur/spread, low alpha) plus a tight contact layer
(small blur, higher alpha) [S01 · provisional]. One flat drop shadow is the tell of a fake; the
paired layers are what read as real depth.

**Posture B — flat 1px-ring (dense, tiling, flat UI).** Cards and popovers separate via a crisp,
low-alpha **ring** (a 1px border/box-shadow) plus a small radius, not a soft blurred drop
[S03 · provisional]. In data-dense and app-chrome contexts the ring tiles cleanly and keeps
surfaces flush; the blurred stacked ramp would muddy a grid of adjacent cards.

**Choosing between them:** the two-layer ramp for expressive surfaces that want to lift off the
page; the 1px-ring for dense, tiling, flat UI where separation must be *drawn* crisply rather than
cast softly. This is a method-pluralism tension, not a contradiction — both are valid, selected by
register.

**Each effect gets its own scale shape.** Match ramp resolution to expressive need: fine-grained
for blur, few steps for inner shadow, and **categorical semantic variants (not sizes) for focus
rings** [S01,S04]. Don't force one ramp length onto an effect that doesn't want it.

---

## 5. The grid & layout system (tokenized, breakpoint-first)

A layout grid is a token system like any other foundation — not an ad-hoc per-page decision. It
obeys the same spine (primitives → semantic aliases) and **inherits the global spacing cadence**,
so page layout and component spacing stay harmonically aligned [S01,S04,S07].

**Breakpoint is the top grid axis.** Namespace grid tokens per device tier
(`grid/<breakpoint>/…`). Each breakpoint owns a *complete, independent* grid definition — the grid
is resolved by tier, never interpolated between tiers, so each layout frame stays authoritative
[S07 · provisional].

**The frame is three paired sizing tokens per breakpoint:** a device/viewport width, a
container/content max-width, and a margin — with **margin = (device − container) / 2**. The content
column is *derived* from that relationship, not hand-placed [S07 · provisional].

**Column count is a per-breakpoint set, not one global number.** Each tier enumerates several valid
column counts (most on desktop, fewest on mobile), and **each count carries its own gutter** —
denser and sparser grids within a single breakpoint carry different gutters [S07 · provisional].
Gutter is therefore tokenized per **(breakpoint × column-count)**.

**Gutters and margins draw from the shared spacing scale** — the same base-unit steps as
everything else — surfaced as semantic aliases. The grid never invents its own numbers
[S01,S04,S07].

**Three distinct responsive padding families, kept independent:** device margin ≠ container inset ≠
section spacing. Keep them as separate token groups so each is its own responsive knob; all three
shrink from generous (desktop) to tight (mobile), but on their own schedules [S04,S07].

**Container max-width is capped and breakpoint-scoped.** Large screens center a fixed content
column; small screens go **edge-to-edge** — margin collapses toward zero and padding does the
insetting [S07 · provisional].

---

## 6. The throughline

Every gap, inset, dimension, corner, shadow offset, gutter, and margin in the system resolves to
one base-unit cadence, exposed through value-named primitives and role-named semantic aliases, with
component-scoped tokens quarantining the exceptions. Where more than one method is legitimate —
radius (size-keyed vs single-knob), elevation (two-layer vs 1px-ring) — the posture is chosen per
project by register and stated in the brief, never defaulted into. That single shared cadence,
applied with deliberate posture choices rather than ad-hoc numbers, is what makes a layout read as
one authoring hand.
