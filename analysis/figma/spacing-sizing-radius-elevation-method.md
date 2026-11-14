# Spacing / Sizing / Radius / Elevation METHOD — the dimensional + effect token architecture of a mature multi-tier design system.

_Confidence: high_

**Portable vs discard:** Portable: the three-tier token architecture (value-named 4-based primitives → t-shirt semantic aliases → size-keyed component-scoped tokens), separate spacing/padding/size axes, size-proportional per-component radius, two-layer role-mapped elevation ramp, and per-effect scale shapes with explain-show-apply docs. Discard as source-specific: the exact numbers (base 4, the 01–05 shadow offsets, the 7/3/3 ramp lengths), the component roster, and all palette/font/copy values."

## Method principles

- **Build on ONE small base unit (4) and generate every spacing/padding/size step as an integer multiple of it (0,4,8,12,16,20,24,32,48...). Name each primitive token by its literal pixel value, not an index: spacing-4, padding-20, size-24.**
  - *Why:* A single rhythmic unit makes any two dimensions visually commensurate, and value-named tokens are self-documenting and collision-free — a reader knows exactly what padding-20 is without a lookup table, and the scale can gain a step without renumbering.

- **Split dimension primitives into SEPARATE parallel axes by role — spacing (gaps between siblings), padding (inset within a container), and size (fixed element dimensions) each get their own namespace (Foundations/Spacing, Foundations/Padding, Foundations/Size) even though they share the same 4-based number line.**
  - *Why:* Role-separated primitives let the same numeric value carry different intent, so tooling and humans can reason about 'all internal padding' vs 'all inter-element spacing' independently, and the two axes can later diverge without a migration.

- **Layer tokens in three tiers: (1) raw primitives (Foundations/*, value-named), (2) semantic aliases that assign meaning via a t-shirt scale (Gaps/Spacing/ds-spacing-small|large|2x-large → 12/24/48) pointing AT primitives, (3) component-scoped tokens (Components/Radius/Custom/Buttons/button-36-radius, Components/Size/.../input-field-width) that bind a specific part to a primitive.**
  - *Why:* The indirection lets layout code consume intent ('small gap') while the raw value stays swappable in one place, and component-scoped tokens isolate a component's quirks so retuning one widget never leaks into the global scale.

- **Name semantic gap tokens on a t-shirt scale (small/large/2x-large) but keep primitives value-named — use words only where a value is a reusable DECISION, numbers where it is a raw ingredient.**
  - *Why:* Abstract names at the semantic layer survive value changes (small can become 16 without a rename); literal names at the primitive layer stay unambiguous. Mixing the two conventions by tier, not by whim, keeps each layer internally consistent.

- **Scope radius per component rather than shipping a single global radius ramp: tiny chips/tags get ~2, buttons ~4, large content blocks get 0, with radius-none as an explicit primitive. Tie the component radius token's NAME to the component's size (button-36-radius) so radius tracks element scale.**
  - *Why:* Corner radius reads correctly only relative to element size — a fixed global 'md radius' looks heavy on a chip and timid on a modal. Size-keyed per-component radius encodes the proportion rule directly into the token, and an explicit radius-none makes 'intentionally square' a deliberate token choice rather than an absent value.

- **Model elevation as a discrete 1..N ramp (01–05) of COMPOSITE shadow styles, where each level stacks two drop shadows — a soft ambient layer (larger blur+spread, ~10% black) plus a tight key/contact layer (small blur, ~20% black) — and both pull their color from a tiny set of alpha-only tokens (elevation-primary-10, -20).**
  - *Why:* Two-layer shadows read as real physical depth (ambient occlusion + contact shadow) instead of a flat grey halo; centralizing only the two alpha colors means the whole elevation system can be re-tinted or dark-mode-inverted from two values, while the per-level geometry stays fixed.

- **Scale elevation geometry monotonically with level: y-offset, blur, and spread all grow together as the level rises (01: y1/blur3/spread1 → 05: y8/blur12/spread6), so higher levels sit visibly farther off the surface.**
  - *Why:* Coupling all three shadow parameters to a single 'height' dimension keeps the ramp perceptually linear and prevents the mismatched-shadow look where a big blur has too little offset — depth stays legible and ordered.

- **Bind each elevation LEVEL to a documented roster of components/states (01=resting cards & switches, 02=buttons & snackbars, 03=menus, 04=raised/dropdown, 05=modals & drawers), not to arbitrary aesthetic choice.**
  - *Why:* Mapping levels to UI roles turns elevation into a z-ordering contract: every surface type has one correct depth, so the whole app's layering stays consistent and a new screen inherits the right shadow by picking its component role, not by eyeballing.

- **Treat every depth/soft-focus effect as its own tokenized family on its own scale: backdrop blur on a 7-step t-shirt ramp (2XS..2XL), inner/'3D' shadow on a 3-step ramp (S/M/L), focus rings as 3 SEMANTIC variants (primary/neutral/error) rather than sizes. Pick ramp length and naming per family's expressive need.**
  - *Why:* Different effects need different resolution — blur wants fine granularity for subtle-to-dramatic glass, inner shadow needs only a few, and focus state is categorical (meaning) not scalar (size). Letting each family choose its own scale shape avoids forcing a one-size ramp onto effects that don't want it.

- **Structure effect/foundation DOCUMENTATION as self-similar spec cards: each effect gets a title + plain-language definition + a labeled live demonstration of every level + a per-level 'where to use this' note, laid out on the same column grid as the rest of the system.**
  - *Why:* A consistent explain-show-apply card template makes the system teachable and self-enforcing — a designer or dev can adopt a token correctly from the doc alone, and the uniform structure signals that effects are first-class tokens, not ad-hoc styling.


## Anti-slop rules learned here

- Don't ship a single global border-radius (one 'rounded' value everywhere). Radius must scale with element size — tiny tags ~2px, buttons ~4px, big blocks 0 — ideally via per-component, size-keyed radius tokens.

- Don't fake elevation with one flat drop shadow (0 2px 4px rgba(0,0,0,.1)). Real depth is TWO stacked layers: a soft ambient shadow plus a tight contact shadow, and the pair scales together across an ordered 1..N ramp.

- Don't invent shadows per-component or inline. Every surface must map to a named elevation LEVEL that is itself tied to a component-role roster (resting card vs menu vs modal), so z-depth stays a system-wide contract.

- Don't collapse spacing, padding, and fixed sizing into one token set. Keep them as separate role-named axes even when they share the same number line.

- Don't number-index primitive tokens (space-1, space-2) — name them by literal value (spacing-4, padding-20) so they're self-documenting and insertable without renumbering.

- Don't use t-shirt names everywhere OR numbers everywhere. Reserve abstract names (small/large/2xl) for the SEMANTIC alias layer and literal values for primitives; don't mix the conventions within one tier.

- Don't force every effect onto the same scale length. Match ramp resolution to the effect: many steps for blur, a few for inner shadow, categorical variants for focus rings.

- Don't skip radius-none / spacing-none as explicit tokens. 'Intentionally square' and 'intentionally flush' should be deliberate token choices, not missing values.

- Don't hardcode effect colors into each shadow. Centralize shadow tint as a tiny set of alpha-only color tokens so the whole elevation system re-themes from a couple of values.

- Don't document foundations as a bare value dump. Use explain-show-apply cards (definition + live per-level demo + usage mapping) so tokens are adoptable from the doc alone.
