# atelier — anti-slop ruleset

> Concrete things to NEVER do. Each is a tell of generic / auto-generated design. Check every output against this before shipping.

## atelier — Anti-Slop Ruleset

Concrete things to never do. Deduped across all layers.

### Rule 0 — the one that overrides all others

**A design with no point of view is slop, no matter how clean its tokens are.** Every project
must make exactly one deliberate bold move (see Standing Policy in `method/00-decide.md`). Zero bold
moves = templated and safe = slop. If you cannot name the one bold move in a finished design,
it is not finished.

### Architecture (all layers)
- **Never let a component or screen reference a raw primitive or literal value** (a hue step, a hex, a bare px). Always go through a semantic alias. Primitives bound directly into UI is the #1 tell of an immature system.
- **Never name a semantic token after its value** (`blue-button-color`). Name by role/intent (`text-primary`, `icon-error-on-solid`) so the value can change without the name lying.
- **Never invent tokens ad hoc per screen.** They must come from a fixed matrix so coverage is auditable and names predictable.
- **Never use one naming grammar everywhere.** Reserve abstract/t-shirt names for the semantic tier and literal values for primitives; don't mix conventions within a tier, and don't special-case one domain so it diverges from the others.
- **Never ship a foundation as a bare value dump.** Use explain-show-apply cards (definition + per-level live demo + usage note) so a token is adoptable from the doc alone.

### Color
- Don't force every ramp to anchor at a mid-step. A symmetric one-size ramp with the "main" color always in the middle is a generator default.
- Don't generate ramps as equal-lightness steps. Perceptual spacing is uneven on purpose — denser in the lights; linear interpolation betrays auto-generation.
- Never ship swatches without per-step contrast data and an explicit AA/AAA/fail verdict.
- Avoid one ramp per hue — a single "red" can't cover brick, rose, and torch; collapsing a family into one ramp is under-built.

### Typography
- Never define a style as a lone font-size. If it doesn't pin line-height, letter-spacing, weight, and paragraph-spacing, it's incomplete and will drift.
- Don't build a single flat linear ramp (h1…h6 / one 12→96 list). That collapses intent and magnitude into one axis.
- Don't hand-pick letter-spacing per step with arbitrary numbers; if tracking isn't a consistent function of size it can't extend cleanly.
- Don't use a constant line-height multiplier across the whole scale — display and body need opposite leading ratios.
- Don't leave line-heights as arbitrary decimals off a rhythm grid.
- Don't bake weight into the size step ("heading = always bold"); weight is an independent axis.
- Don't hardcode one font family everywhere; omitting the display/body split forecloses the likeliest future change.
- Don't ship size-only styles with no responsive behavior; one fixed px forces per-breakpoint overrides downstream.

### Space / Radius / Elevation
- Don't ship a single global border-radius. Radius scales with element size via per-component, size-keyed tokens.
- Don't fake elevation with one flat drop shadow. Real depth is two stacked layers (ambient + contact) scaling together across an ordered ramp.
- Don't invent shadows per-component or inline. Every surface maps to a named level tied to a component-role roster.
- Don't collapse spacing, padding, and fixed sizing into one token set — keep separate role-named axes even on a shared number line.
- Don't number-index primitives (`space-1`); name by literal value.
- Don't force every effect onto one ramp length — match resolution to the effect (fine for blur, few for inner shadow, categorical for focus rings).
- Don't skip explicit `*-none` tokens; "intentionally square/flush" is a deliberate choice.
- Don't hardcode effect colors into each shadow — centralize tint as a tiny set of alpha-only tokens.

### Components
- Don't build one monolithic Button/Input/Card with a sprawling variant matrix. Split into named siblings scoped to one job each.
- Don't fork a component per interaction state (`Button Hover` as its own component). States are variant axes of one set.
- Don't leave the base primitive anonymous or buried, or copy-paste it into each composite.
- Don't bake density/scale into every component as a variant when a parallel compact library expresses it once at the library level.
- Don't dump components into a flat namespace. Use path taxonomy, category prefixes, and functional pages.
- Don't ship components without a one-line usage description.
- Don't conflate an atom with its labeled molecule — keep the bare field separate from the field group.
- Don't wrap single-state elements in a variant set for symmetry.

### Page composition
- Don't stack two tall, dense sections consecutively; insert a short calm band between heavy ones.
- Don't give every section the same height or content weight — uniform bands signal a template.
- Don't repeat the same 50/50 split orientation twice in a row; flip sides each time.
- Don't let text run the full container width in reading-heavy sections; cap prose and headers to a readable measure.
- Don't break the grid by widening/going full-bleed for text — the intentional break is a narrowing to a centered column.
- Don't overload the hero with copy, multiple CTAs, and feature lists; keep it a light stage and move proof to the band below.
- Don't invent ad-hoc spacing or widths per section; resolve every value to the shared ramp.
- Don't cluster all social proof into one block; thread it through the whole scroll.
- Don't order sections arbitrarily; sequence as a decision narrative with the primary action reachable throughout.
- Don't mix multiple type families or leave headline tracking loose at large sizes.
- Don't drop a section in without a recognizable header grammar.


---

## Additions from Source 03 (dashboard / data-density / shadcn)

- Token method (thin semantic layer): never reference a ramp step (a '600', a '-foreground-900') directly in a component — a numeric scale step inside a component means the semantic layer was bypassed; bind to a role token.
- Never create parallel light/dark component variants or a 'dark-'-prefixed palette — dark is a value mode on the same semantic names; a second component or palette name is the ramp-era tell.
- Never ship a foreground without its paired background (or vice versa) — orphan 'on-color' tokens break the contrast-travels-with-the-token guarantee.
- Never store colors as frozen hex when you need tints/rings — keep channels so alpha variants (rings, overlays, disabled) derive from one token instead of spawning new ones.
- Never invent a new semantic token per component in the thin-layer method — the role set is small and closed; a new role must be a new MEANING, not a new appearance (resist 'card-button-border' sprawl).
- Never implement focus/invalid as a layout border that changes box size — use a ring (shadow-spread) token so focus never reflows the element.
- Never treat a component library as a black-box dependency themed via overrides — own the atom source and theme through the token names (the contract is the names).
- Data density: never signal importance with large type in a dense view — if you reach for 24px+ inside a table or KPI strip, switch to weight + muted-color contrast on the existing 12/14px scale.
- Never hardcode cell padding or badge insets as arbitrary px — pull from the micro-spacing ramp so density stays on-grid.
- Never left-align numeric columns or use proportional figures — right-align with tabular figures so columns compare vertically.
- Never build the data table as one hardcoded block — toolbar, body, and footer (selection count + pagination) are separate, independently toggle-able regions, with checkbox/sort slots pre-reserved so turning them on causes no reflow.
- Never scatter saturated color for decoration in a data view — reserve hue strictly for status badges, signed trend deltas, and the single active/current control.
- Never float dense cards with soft/blurred drop shadows — use a 1px ring shadow + small radius for flat elevation that reads at high card counts.
- Never give every chart its own full card — inline sparklines/mini-bars/donuts into stat cards by default; reserve full chart cards for charts that are themselves the subject.
- Never separate dense rows with empty margin you don't have — use hairline dividers, zebra striping, and card borders as the density-era substitute for whitespace.
- Never let a KPI/stat card have two competing focal points — exactly one dominant big value; label, timeframe, delta chip, and micro-chart are all subordinate.
- Never redesign cards per breakpoint — keep per-card density constant and reflow by collapsing the column count and the nav rail.
- App shell: never build one sidebar component per role or per display mode — build ONE rail parameterized by (role, display-mode, active-page); roles subtract/reorder from a shared definition, modes change density/placement.
- Never let the menu and the access control disagree — a link visible to a role must open to a permitted (not 'access denied') state; both derive from the same permission matrix.
- Never ship a blank or spinner-only empty/loading state — every widget kind needs a typed empty state (icon + title + support line) and a loading skeleton matching its final layout; show a CTA only when the current role can perform the action.
- Never re-render the shell on navigation — nav rail, header frame, and user footer persist; only the content slot swaps (collapsing the rail is a state change, not a route change).
- Never hardcode shell metrics — rail width, header height, content padding, and radii come from named structural tokens so theming, density modes, and responsive collapse stay consistent.
- Never treat count/notification badges as decoration — a nav badge must reflect real per-destination state and clear when the user addresses it.
- Never flatten navigation into one long list — group into labeled semantic sections with a stable slot order so role-based hiding and future features have predictable insertion points.


---

## Additions from Source 04 (storefront / responsive)

- Responsive component: never ship one fluid layout and call it responsive — author an explicit variant per breakpoint (Desktop/Tablet/Mobile) as siblings in one component set, so each reflow is a deliberate decision, not a flexbox side effect.
- Never keep inline horizontal nav links on tablet/mobile 'because they fit' — collapse to a hamburger at the defined threshold and hold the bar height constant.
- Never shrink icon/touch targets to make a toolbar fit — shed lower-priority utility icons by priority (5→4→3) and keep the survivors at full hit-target size.
- Never author a menu/overlay open-state as a disconnected separate screen — co-locate it as a hidden child frame inside the same breakpoint variant so collapsed and open states never drift.
- Never merely wrap multi-column content when stacking — choose column count per breakpoint (N→N/2→1), widen each block to fill, and consciously choose stacking order (promote high-value items) rather than accepting raw source order.
- Never reflow every element uniformly — keep band-spanning rows (newsletter / section-header + input) full-width at every breakpoint while only the grid columns below them collapse.
- Storefront: never merge the primary category nav and the right-pinned utility cluster (locale/currency, search, offers, account, cart) into one undifferentiated menu — they are distinct component classes.
- Never ship a retail category menu as a plain link list — make it a two-pane merchandising surface with a descriptor category rail and a featured-product pane.
- Never hardcode product-card width in px — bind it to a block-size token so grids reflow by column count, not by resizing the card.
- Never render an empty cart as a dead end, and never omit the free-shipping/threshold progress line from the cart drawer — the empty state must cross-sell and offer a 'view all' path.
- Never build a thin link footer for a storefront — carry opening hours, address, contacts/social, a locale switcher, a legal row, and a payment-badge row.
- Never present newsletter signup as a bare form — lead with the discount incentive and include consent microcopy linking terms/privacy.
- Never scatter trust signals across the page — consolidate them into one icon+label strip below the nav or hero.
- On mobile, never leave an always-open desktop filter sidebar — collapse filters behind a Filter trigger with a sticky 'Show results' commit bar.
- Page skeletons: never model a page as one flat section list — split GLOBAL CHROME (promo/header/footer, authored once) from the per-template BODY stack, and prepend a breadcrumb only on deep/transactional pages.
- Never treat the slide-out mini-cart and the full cart PAGE as the same skeleton — the page adds a breadcrumb, an incentive bar, a two-column summary+reassurance panel, and a cross-sell rail.
- Never stack a homepage as pure product rails with no trust/story bands between them — alternate discovery bands with trust/story bands or it reads as a catalog dump.
- Never flatten the PDP buybox into 'title + price + button' — it is an ordered named sub-skeleton (rating+cert → title → spec chips → desc → price → variant swatches → option controls → ATC → payment badges → trust strip → accordions → mini cross-sell).
- Never give a long-form/editorial page (blog/about/legal) a full-width body or a buy-CTA ending — constrain it to a readable measure and close with lateral navigation (related/next).
- Never re-order sections per breakpoint — author section order at desktop, keep it breakpoint-invariant, and derive mobile by collapsing columns and drawer-izing filters.
- Never drop the PLP toolbar (live result count + sort) or a progressive load affordance — they are the irreducible core of a collection page, not decoration.


---

## Additions from Source 05 (thin-semantic / app register)

- Do not treat the three color methods as a forced single choice when the register is an app/dashboard — layer a thin-semantic tier on top of a primitive ramp library; a UI that binds ramp steps directly is a missing semantic tier.
- Do not expose primitive ramp steps to UI or let a component bind family/step directly — UI reads only semantic role tokens. A raw ramp-step reference in a component is the tell.
- Do not let primitive and semantic tiers share a namespace — encode the tier in the token NAME (library prefix for primitives, bare role for semantics) so no one grabs a primitive by accident.
- Do not widen the thin semantic layer into a sprawling flat role list — when it must grow, add a bounded SUB-namespace (chart, sidebar/app-shell) with its own closed roles. A long ungrouped role list is slop.
- Do not model borders/overlays as opaque neutral steps in a mode-switched system — use foreground-at-low-alpha so one token survives every surface shade in both modes.
- Do not collapse status into a single destructive token when the app surfaces info/success/warning distinctly — promote the full status quartet into the role set.
- Do not author bespoke contrast-measured primitive ramps when an adopted utility palette suffices for an app register — but never ship the adopted palette as the UI contract; always interpose the semantic tier.
- Do not reflexively apply negative letter-spacing to large headings — tracking is a register knob; default to 0 for neutral/clinical/technical/B2B brands and only go negative for editorial/luxury.
- Do not give buttons, nav items, chips/pills, or inline run-in labels the body line-height — single-line centered roles get leading 1.0; only flowing paragraphs get ~1.5.
- Do not conflate 'has named text styles' with 'has type variables' — audit both substrates separately; variable-binding is not required for centralization.
- When adding a third typeface, give it a register/job (e.g. mono strictly for status/metadata/micro-text) — never add a third face as decoration or let it leak into headings/body.
- Do not add a variant axis a sibling doesn't need for cross-sibling symmetry — split into job-scoped siblings the moment two axes stop being orthogonal; each sibling exposes only its real axes.
- Do not read an intentionally greybox/monochrome kit as unfinished and rush to skin it — its neutrality is the method; preserve structure-decoupled-from-skin.
- Do not run two same-PURPOSE bands in a row on a homepage (two product rails, or two story bands) even if their visual weights oscillate — alternate discovery with trust/story.
- Do not re-order sections per breakpoint — hold band sequence invariant; reflow only by column-collapse (N→N/2→1) and drawer-izing filters with a sticky commit bar.
- Do not model a page as one flat section list — split global chrome (authored once) from the per-template body stack; prepend a breadcrumb on deep/transactional pages only.
- Do not end an editorial/long-form page with a buy-CTA or a dead-end — hold the narrow reading measure for the whole body and close on lateral navigation; reserve the cross-sell-rail closer for commerce pages.
- Do not overlay hero copy as a scrimmed text block over a busy image — compose headline + single CTA into the image's pre-planned negative space.
- Never proceed with a Figma analysis when the fileKey is missing or a literal placeholder ('undefined'/'null'/'{{...}}') — halt and report; do not guess a key, reuse an unrelated project's key, or synthesize plausible findings to fill the schema. An empty new_findings array is the correct honest output when the source can't be read.


---

## Additions from Source 06 (brand-dominant register)

- Don't default every storefront to a neutral ground with a timid accent. When the brief has a strong single-brand identity, a bold brand hue can BE the dominant surface; reaching for white-page-plus-small-accent every time is a template tell.
- Don't force a per-category hue system onto a shop that has a strong master brand hue; multiple category hues fight a dominant brand hue and read as unresolved. One brand hue owning the field is a legitimate, often stronger, choice.
- When the dominant field is a saturated brand hue, never pick the CTA/action color from the same hue family; it disappears. The accent must be chromatically distant (near-complementary, high-contrast) so action escapes the field.
- Don't treat on-dark/on-brand foregrounds as an afterthought suffix when inverse fields cover large areas; author the ground-aware foreground pair up front or legibility breaks on half the page.
- Don't let a bold brand hue tempt you into many saturated colors; a brand-dominant register still rations hue to brand-hue + black + white + ONE accent.
- Don't treat density oscillation as height-only in an expressive register; a short band on a full-saturation surface is HEAVY. Alternate surface-weight as well, and never place two full-bleed saturated bands back-to-back.
- Don't let proof dissolve into a colorful page; bind it to the single reserved accent so 'saturated' reliably reads as 'credible/commit', and don't spend that accent on decoration.
- Don't read a full-bleed dark/saturated band as a WIDENING break; the editorial break is still a NARROWING to a readable measure that the inverted surface merely amplifies.
- Don't hand-build one sidebar per role or per plan tier; build ONE shell whose nav is driven by a role×tier permission matrix. N near-identical copies drift and leak access the moment requirements change.
- Don't leave role/entitlement coverage implicit; publish the explicit view×role(×tier) access matrix so every cell is decided and auditable (unlisted = undecided = a bug).
- Don't conflate the atomic component library with block collections; keep curated, counted contact-sheets of pre-composed sections as a separate higher-altitude layer, and don't let the 'Total Blocks: N' count go stale.
- Don't hard-embed content inside a container organism when the payload varies; expose named slots (shown as placeholders) and fill by instance-swap.
- Don't maintain documentation chips separately from the live UI primitive they describe; make the docs USE the real component so the spec can't drift from the token.
- Don't model post-action outcomes (return submitted, eligible vs closed, order placed) as one page with runtime conditionals; enumerate each terminal state as its own named frame.
- Don't treat Order Confirmation as 'checkout minus the form'; it is a separate receipt template with its own required slots including the loyalty/points-earned callout.
- Don't collapse a PDP to 'gallery + buybox + tabs'; the evidence narrative (science → proof → usage → social proof → FAQ → cross-sell) is the conversion engine, modeled as an ordered, individually-optional stack.
- Don't treat drawers/slide-outs as loose states; give each its own {header / body / pinned-action} skeleton so overlays get the same anatomy discipline as full pages.


---

## Additions from Source 07 (grid / layout)

- Never express the grid as one global column count / one gutter — resolve both from the active breakpoint tier.
- Never invent gutter/margin pixel values; bind them to the shared spacing-scale steps so the grid stays on the global rhythm.
- Never hardcode a content width — derive the container from `device-width − 2×margin` (or an explicit container-width token) so margins recompute per tier.
- Never reuse desktop gutters/padding on tablet or mobile; each tier carries its own smaller values — collapsing them flattens the responsive intent.
- Never conflate the three padding families (device margin ≠ container inset ≠ section spacing); keep them independent so each responds on its own.
- Never bake a nonzero margin into the column math on small breakpoints — margin legitimately goes to 0 (edge-to-edge) there.


---

## Additions from Source 08 (category-color / playful register)

- Mint each catalog category as a {accent, tint} PAIR of the same hue, never a lone accent — bind the tint to backing surfaces and the accent to interactive ones so a category reads as one family across loud and quiet surfaces.
- Make accent color a function of SCOPE: category-in-scope → that category's pair; nothing-in-scope ('All'/global sheet) → brand-primary fallback — and write the fallback down rather than leaving un-categorized surfaces to guesswork.
- Bind the accent token at the smallest meaningful unit (the card/item) so mixed lists self-theme into a visual taxonomy, and allow a page-scope override to collapse to one theme when filtered.
- Tune ONLY the category layer's chroma to the brand register (muted↔high-chroma); keep the neutral ramp, type tokens, and chrome discipline constant so a loud palette never destabilizes structure.
- Do not default every role to one family — assign typefaces by role-class (structure / reading / action) when the brief wants separation, but cap at ~3 purposeful faces, each owning a clear band.
- Do not style buttons and links as 'small bold headings' — give interactive roles their own named tokens with their own family + medium weight even where their size overlaps a heading step.
- Name type (and all) tokens by role/intent, not by resolved value; keep two roles separate even when their current font/size/weight are identical, so they can diverge later without a rename.
- When a design shows N visually-different cards/sections, do not author N components — find the shared skeleton and externalize the per-instance difference to a single category/data token binding.
- Model responsive sizing as one semantic role name resolving to breakpoint-specific VALUES; keep component references stable across breakpoints and never fork a component just to change its sizes.
- Separate sections with intentional seams (angled color-block edges, tilted divider planes, or a full-bleed reset band), not a default horizontal rule or identical margins everywhere.
- When a focal slot holds a set of peers, consider a fanned/stacked-deck cluster as one object instead of a flat mini-grid — keep rotations subtle and the content grid inside each card clean.
- Catalogue overlays/drawers/modals as a SEPARATE track from full-page skeletons, tagging each with the breakpoint(s) it appears on and the inline region it replaces — do not conflate an overlay with a page.
- Treat empty/zero/gate/multi-step states as first-class required skeletons with their own section stacks; never assume only the happy-path populated page needs a template.
- Collapse structurally-identical sibling frames (per-category PLPs, per-product PDP skins) into ONE parametrized skeleton with a named variable slot; never list each near-duplicate as its own page type.
- Model checkout as a stepped flow family sharing one persistent order-summary slot (desktop rail / mobile accordion), not as a single checkout page.
- When enumerating a large multi-frame Figma file, drill page→child-frame IDs before screenshotting — never read a 30000px canvas as one unreadable thumbnail; re-request tall frames at their natural height and split the PNG before reading.


---

## Visual / aesthetic anti-slop  `[S09]`

> **Everything above polices how the system is *built*. This section polices how the output
> *looks*.** A design can pass every architecture/color/type/space/component/composition rule
> above and still read as machine-made, because the tells below live in appearance, not method.
> This gap shipped real slop on a first build (arrows on links, dot-joined meta, an all-caps
> eyebrow over every heading) that the method-only ruleset passed clean. Run this as a **distinct
> pass** from the method checks.
>
> **These are not bans — they are a diagnostic scan plus a purpose test.** One pattern that
> serves a stated purpose is fine. Slop is many of them stacked with no reason. For each one you
> use, you must be able to write the one-line reason it serves (hierarchy, identity, readability).
> If the only reason is "it looks modern" / "it looks AI-safe," cut it or rework it.

### The two questions that gate the whole section

1. **The swap test.** If you swapped out the logo and brand name, would this still feel like a
   specific brand with its own character — or could it belong to any product? If *any product*,
   it's too generic; the identity isn't doing any work.
2. **The void test.** Removing slop does not create good design; it leaves a void the model
   refills with its most generic output. After cutting tells, confirm the page is *alive and
   specific* (a real palette, a face chosen for a reason, one repeated identity motif, one
   deliberate accent) — not merely *clean*. A sterile, flat-white, thin-grey-border, no-identity
   result is its own slop (the over-filtered default).

### Visual / color tells

- Don't reach for the generated-palette defaults: blue→purple / blue→cyan / purple→pink
  gradients, full-page colored glow, neon accents, pastel blocks, radial orbs, purple-and-black
  "tech" schemes. A gradient that separates one level of hierarchy is craft; the same gradient as
  page wallpaper is slop.
- Don't stack trend effects (glassmorphism + mesh gradient + glow + grid + mono + pill-everything)
  — each needs its own purpose, and three at once with none stated is the tell.
- Don't blur (backdrop-filter) the navbar, cards, modal, and sidebar all at once — glassmorphism
  is a 1–2-element accent, not the character of the UI.
- Don't put a soft drop shadow / a glow on every element so the whole page floats — elevation is
  a selective hierarchy marker; most surfaces sit flat.
- Don't spend one accent color on buttons AND icons AND badges AND links AND rules AND backgrounds
  — ration it (one deliberate accent at the key moment; the brand/anti-slop color rule above).
- Don't wallpaper the background with a grid / dot / blueprint / graph-paper pattern for "texture"
  with no identity reason.
- Don't default to dark mode because it "looks tech" — theme follows brand/product/users, not vibe.
- Don't use grey skeleton bars as the hero/product shot. Show the real thing or an honest
  placeholder, never a disguised one.

### Layout / section tells

- Don't ship the template stack on autopilot: Hero → subtitle → 2 CTAs → screenshot → feature
  grid → testimonials → FAQ → CTA → footer. Section order follows the *product's* narrative, not
  the generated default (this is the composition "decision narrative" law, restated as a tell).
- Don't make every section the same composition — centered title + subtitle + identical card grid,
  repeated down the page. Uniform section rhythm, and "the only variation is the background flips
  every other section," both read as template. (Pairs with density/surface oscillation above.)
- Don't render feature cards as N identical boxes (same size, icon, padding, height) when the
  content has a hierarchy; vary to reflect it, and not every point needs to be a card.
- Don't reach for the default "app-like" bento mosaic, a fake terminal window as the hero visual,
  or "How It Works" as exactly 3 round-icon numbered steps — unless the content genuinely is a
  3-step sequence (numbered markers are only honest when order carries real information).
- Don't bolt on the stock trust/pricing/footer furniture by reflex: a "Trusted By" logo bar
  directly under the hero, a "Most Popular" highlighted middle tier, exactly 3 pricing columns,
  a 4-column Product/Company/Resources/Legal footer — each must match the real content or go.

### Decoration / typographic tells

- Don't append an arrow (`→` / `↗`) to link and button text as a default identity. Not every CTA
  needs an arrow; if one earns it, say why. *(This shipped in the first Kristina build as
  `Read article →`.)*
- Don't park a tracked-out ALL-CAPS eyebrow / pill label above every heading, especially when it
  just restates what the heading already says. An eyebrow is a scarce wayfinding device — spend it
  on a few sections, not all of them. *(First Kristina build put one over every band.)*
- Don't join meta with middle dots as a reflex (`Author · 8 min read · Date`, `A · B · C`); it's
  a template-chrome signature. Use it only where it genuinely reads best. *(Shipped in Kristina.)*
- Don't build labels as `WORD — fragment` with a spaced em dash, or reach for monospace for small
  data labels, or large-monospace headings / extreme-tracked uppercase "AI typography."
- Don't accent a single word in a headline (one word italic / colored / bold for pop) — set the
  line whole; let the whole type treatment carry it.
- Don't use generic AI glyphs (sparkle, star, magic wand, lightning, diamond, cube, robot, orb)
  as feature icons, and don't pick an icon set for its recognizable library look rather than
  relevance. If no icon is genuinely relevant, use none.
- Don't put a colored left-stripe on cards/rows as decoration, or ship AI capsule badges
  ("AI Powered" / "Beta" / "New" as pill + thin border + glow + dot + uppercase) without a real
  status to show.
- Don't choose a typeface because it's the safe default (Inter / Geist / Space Grotesk for sans,
  the usual monos) — choose for brand character and write the reason. A popular face is still fine
  *with* a reason.

### Copy tells (design-adjacent — the words are design material)

- Don't use the em dash (`—`) as a reflex connective in UI copy — it's a strong AI tell; a comma,
  period, colon, or parentheses usually reads more human. (A brand voice the owner supplies that
  uses it is direction, not agent copy — honor it; flag, don't silently strip.)
- Don't ship generic CTAs ("Get Started," "Learn More," "Try Now," "Explore," "Discover") — name
  the actual action ("Start reading," "Book a session").
- Don't use AI marketing buzzwords (AI-powered, seamless, revolutionary, next-generation,
  cutting-edge, unlock, elevate, empower, game-changing). Say the specific real benefit instead.
- Don't invent what you can't verify: no fabricated statistics, testimonials, logos, names, job
  titles, or trust/compliance claims (SOC 2, "300% faster"). No real data → show no number.
  Empty beats fabricated. (This also guards against a reviews/trust strip stuffed with invented
  proof — if the proof isn't real, the section shouldn't exist.)

### Liveliness (what to add after the cuts — the void test, operational)

Set and hold three dials for the whole design, derived from the brand book / register:

- **ENERGY** — how hard the design says hello (calm/public-service → balanced/SaaS → bold/agency).
- **RHYTHM** — how much sections vary from each other (uniform → consistent-with-breaks → mixed).
- **MOTION** — how much non-interaction motion, and why (hover-only → scroll-reveal → choreography).

Then hit them with levers, not decoration: **one focal point per screen**; **hierarchical
contrast** on purpose (size/weight/color), not randomly; **whitespace as structure**, not
leftover; **one deliberate accent** (zero = sterile, everywhere = slop); **one identity motif** —
a pattern, gesture, or typographic voice that is specific and repeated so the design belongs to
*this* brand. (atelier's "one bold move" / signature move is this motif; this just makes the rest
of the page carry its weight too.)
