# Typography system — scale architecture and composite type-token method

_Confidence: high_

**Portable vs discard:** "Portable: the composite-token recipe (role families × T-shirt steps × orthogonal weight axis; each step bundling size+line-height+letter-spacing+paragraph-spacing bound as sub-tokens), the proportional laws (tracking ≈ fixed % of size, line-height ratio tight-for-display/loose-for-body, line-heights snapped to a grid), the dual display/body family slots, per-breakpoint resolution, and the hierarchical naming + documented specimen. Discard as source-specific: the actual typeface name, the exact px/weight numbers, and the role-label wording — regenerate those per project."

## Method principles

- **Model each type style as a COMPOSITE token (a 'Font(...)' object), not a font-size. Every step bundles seven bound sub-values: font-family, named weight/style, size, line-height, letter-spacing, paragraph-spacing, and paragraph-indent. Consumers reference one style; the bundle travels with it.**
  - *Why:* A style is a semantic unit, not a number. Bundling size+rhythm+tracking guarantees that anyone who picks 'Title M' gets correct vertical rhythm and tracking automatically, so correct typesetting is the path of least resistance and drift between size and line-height becomes impossible.

- **Structure the scale as a 2D matrix: FAMILIES (semantic roles) on one axis, SIZE STEPS on the other. Use ~5 role families (a display/attention tier, a headline tier, a title/subhead tier, a body/reading tier, a label/UI-caption tier) each subdivided into a fixed T-shirt step ladder (XL, L, M, S, XS, sometimes XXL).**
  - *Why:* Roles map to intent ('what is this text for') while steps map to magnitude ('how big within that role'). Designers pick by meaning first, size second, which keeps usage consistent and makes the system legible without a spec sheet.

- **Overlap the families' size ranges deliberately so adjacent tiers share px values but differ in treatment. The top of a lower tier numerically overlaps the bottom of the tier above it (e.g. a 24px body-adjacent title and a 24px small-headline can coexist).**
  - *Why:* The differentiator between tiers is not just size but line-height ratio, tracking, weight intent, and paragraph behavior. Overlap lets the same optical size carry different typographic personalities depending on role, which is impossible with a single linear ramp.

- **Make letter-spacing a PROPORTIONAL FUNCTION of size, not a hand-tuned per-step value. Large display sizes get strongly negative tracking that shrinks (toward zero or positive) as size decreases; small UI text gets near-zero tracking. In this system tracking is almost exactly a fixed fraction of size (large tiers ~ -5% of size, body/label ~ -1% of size).**
  - *Why:* Optical tracking need scales with size: big type looks loose and needs tightening; small type needs its default or slightly open spacing for legibility. Encoding tracking as a ratio of size makes the whole ramp self-consistent and trivially extensible to new steps.

- **Scale line-height INVERSELY proportional to size: display tiers run tight (line-height ≈ 1.05–1.1× size), body tiers run loose (≈ 1.3–1.45× size), labels tightest-to-moderate. Quantize line-heights to a small rhythm grid (multiples of 2/4px) rather than arbitrary decimals.**
  - *Why:* Headlines are short and want density; running text needs open leading for readability. Snapping line-heights to a baseline grid keeps multi-column layouts and vertical rhythm aligned across every style.

- **Treat WEIGHT as an orthogonal third axis, not baked into the step. Generate each display/heading step across a full named weight ladder (Light 300 → Regular 400 → Medium 500 → SemiBold 600 → Bold 700 → ExtraBold 800), emitting one named style per (step × weight) cell; reading tiers expose far fewer weights.**
  - *Why:* Separating weight from size lets the same size express different emphasis without multiplying the size scale. Offering the full ladder only where it's used (display/headline) and restricting body/label weights prevents combinatorial bloat while covering real needs.

- **Provision TWO font-family slots — one for display/attention type, one for body/reading type — as tokens, even if they currently resolve to the same typeface. Display tiers bind the display family; body/label tiers bind the body family.**
  - *Why:* The display/body split is the single most common evolution of a type system. Wiring it as two tokens from day one means swapping in a distinct display face later is a one-token change, not a refactor of every style.

- **Make the scale RESPONSIVE by storing per-breakpoint values (desktop/tablet/mobile) for size, line-height, and tracking on each step, so a single named style fluidly resizes. The step down the breakpoints roughly equals the step down one size notch (mobile of step N ≈ desktop of step N-1).**
  - *Why:* One semantic name ('Display XL') that resolves differently per viewport keeps components breakpoint-agnostic and preserves hierarchy across devices without authoring separate mobile styles. Aligning the breakpoint delta to the scale ratio keeps proportions intact.

- **Name tokens by a strict hierarchical path: Typography / <Family> / <Step> / <step>-<property>, with the composite style named <Family>/<Step>/<Weight (nnn)>. Keep atomic sub-tokens (size, line-height, etc.) addressable independently of the composite.**
  - *Why:* Predictable namespacing makes tokens self-documenting and machine-navigable, and exposing atoms lets edge cases reference a raw value (e.g. one-off line-height) without detaching from the system.

- **Pair every family with a plain-language USAGE definition (what it's for, how sparingly to use it) and render the full specimen matrix — every step × weight, with its measurements and a live preview — as the design-system documentation surface.**
  - *Why:* A scale is only adopted correctly if intent is documented next to the specimen. Showing measurements + previews together turns the token file into its own spec, eliminating ambiguity about which style to reach for.


## Anti-slop rules learned here

- Never define a type style as a lone font-size. A style that doesn't also pin line-height, letter-spacing, weight, and paragraph-spacing is incomplete and will drift.

- Don't build a single flat linear size ramp (h1..h6 / one 12→96 list). Lacking the role×size matrix collapses intent and magnitude into one axis and produces generic hierarchy.

- Don't hand-pick letter-spacing per step with arbitrary numbers. If tracking isn't a consistent function of size, the ramp looks inconsistent and can't be extended cleanly.

- Don't use a constant line-height multiplier across the whole scale. Display and body need opposite leading ratios; one ratio for all is a dead giveaway of an unconsidered system.

- Don't bake weight into the size step (e.g. only ever 'Heading = Bold'). Weight must be an independent axis so emphasis varies without duplicating sizes.

- Don't hardcode a single font family everywhere. Omitting the display-vs-body family split forecloses the most likely future change.

- Don't ship size-only styles with no responsive behavior. One fixed px per style forces per-breakpoint overrides in every component downstream.

- Don't leave line-heights as arbitrary decimals off any rhythm grid; unsnapped leading breaks vertical alignment.

- Don't ship the scale without usage guidance and a specimen matrix — an unlabeled token dump gets misused.
