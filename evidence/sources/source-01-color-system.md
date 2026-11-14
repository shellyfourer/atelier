# Color system — primitive ramp architecture + semantic alias mapping

_Confidence: high_

**Portable vs discard:** Portable: the two-tier primitive/semantic split, Family->Ramp->Step naming, a fixed light-dense step scale, floating per-ramp anchors named after the anchor, per-step contrast+verdict, and the Role x Prominence x Status x Context semantic matrix. Discard: the specific hue inventory, ramp nicknames, exact hex values, the exact family/ramp count, and font/brand specifics — all source-specific.

## Method principles

- **Split color into two hard-separated tiers: a PRIMITIVE tier (named hues with numeric steps, pure values, zero intent) and a SEMANTIC tier (role-named aliases that only ever point AT primitives, never at raw hex). UI and components consume semantic tokens exclusively; primitives are the private palette.**
  - *Why:* Decoupling value from meaning lets you re-theme, swap a brand hue, or fix a contrast failure by re-pointing aliases without touching a single component. It is the single highest-leverage structural decision in a color system.

- **Organize primitives as Family -> Ramp -> Step, a three-level namespace (e.g. collection a hue family contains multiple distinct ramps (a warm variant, a muted variant, a tinted variant); each ramp holds the stepped tokens). Allow MULTIPLE ramps per hue family rather than one ramp per hue.**
  - *Why:* A family groups perceptually-adjacent ramps so designers browse by intuition, while separate ramps within a family give real chromatic range (a warm red vs a pink-red vs a brick-red) instead of forcing every red UI need through one compromise ramp.

- **Use a fixed, shared step scale across every ramp with denser sampling at the light end. Here: 25, 50, 100, 200...900, 950 — twelve steps, two extra ultra-light steps (25,50) below 100 and one ultra-dark (950) above 900.**
  - *Why:* A uniform scale makes ramps interchangeable (swap hue, keep step) and makes tokens predictable. Extra light steps exist because tints get used heavily for backgrounds/surfaces/hovers where small luminance differences matter most; the human eye discriminates more finely in highlights than shadows, so the scale is denser where it is used and perceived.

- **Anchor each ramp at whatever step is its most usable/representative tone, and NAME the ramp after that anchor (e.g. '<WarmAccent> - 500', '<PaleTint> - 100', '<Neutral> - 950'). The anchor is NOT forced to 500 for every ramp.**
  - *Why:* A pale yellow and a near-black neutral do not have their 'character' at the same lightness. Letting the anchor float to the step that actually defines the color keeps naming honest and tells a consumer which step to reach for first, rather than imposing a false 500-centric symmetry.

- **Document a measured WCAG contrast ratio AND a pass/fail accessibility badge on EVERY step of EVERY ramp, not just the anchor — against a fixed reference (here each step's ratio vs white, monotonic from ~1.07 at the lightest to ~19 at the darkest).**
  - *Why:* Accessibility is a property of the value, so it belongs on the primitive where it is objective and reusable. Per-step contrast turns the palette into a lookup table: a designer picking a text color can instantly see which steps clear AA/AAA on a given background, before any semantic decision is made.

- **Name semantic tokens as Role x Prominence/Status x Context, each as its own namespace segment: role = the element being painted (Text, Foreground/Layers, Icons, Surface...), prominence = Primary/Secondary/Tertiary, status = Success/Warning/Error, context = a suffix like '-on-solid' for tokens meant to sit on a filled color.**
  - *Why:* This lets a component ask for exactly the color its situation needs (text-primary vs text-primary-on-solid) and guarantees legibility in that situation by design. The multi-axis name is self-documenting and makes missing combinations obvious when auditing coverage.

- **Give each hue section an editorial header: a human title plus a short paragraph on the color's psychological role and intended use (energy/urgency for red; neutral foundation for gray), separate from the mechanical swatch grid.**
  - *Why:* A palette is also a communication tool. Documenting intent at the family level guides correct selection and prevents misuse (reaching for an alert-red as a decorative accent), which no amount of hex values can convey.

- **Treat color as one instance of a uniform foundation pattern applied to ALL token domains — typography, spacing, padding, sizing, radius, gaps follow the identical primitive->semantic, scaled-step structure (e.g. spacing-4/8, size-24, tag-radius aliasing a radius primitive).**
  - *Why:* One consistent mental model across every foundation means a designer or engineer who learns the color system already knows the spacing and type systems. Uniform architecture is what makes a system feel like a system rather than a pile of tokens.


## Anti-slop rules learned here

- Never let a component or screen reference a raw primitive (accent-500) or a literal hex — always go through a semantic alias. Primitives bound directly into UI is the #1 tell of an immature system.

- Do not force every ramp to anchor at 500. A one-size 50->900 symmetric ramp with the 'main' color always in the middle is a generator default, not a designed palette.

- Do not generate ramps as mathematically even lightness steps (equal L* deltas). Perceptual spacing is uneven on purpose — denser in the lights — so a linear interpolation betrays auto-generation.

- Never ship swatches without per-step contrast data and an explicit AA/AAA/fail verdict. Dumping hex chips with no accessibility annotation is decorative, not functional.

- Avoid one ramp per hue. A single 'red' ramp cannot cover warm, muted, and tinted variants of one hue; collapsing a family into one ramp is an under-built shortcut.

- Do not invent semantic tokens ad hoc per screen. They must come from a fixed Role x Prominence x Status x Context matrix so coverage is auditable and names are predictable.

- Never name semantic tokens after their value (e.g. 'blue-button-color'). Name them after role/intent ('text-primary', 'icon-error-on-solid') so the value can change without the name lying.

- Do not treat color as special-cased. If spacing/type/radius use a different naming grammar than color, the system is inconsistent — all foundations should share the primitive->semantic scaled pattern.
