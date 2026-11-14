# Taste & judgment calls awaiting the human

> Collaborative curation (your choice). These are NOT auto-decided. Resolve, then fold into the relevant method/ chapter + method/anti-slop.md.

- [ ] Hue inventory and palette intent: which hue families exist, how many ramps per family, and the editorial psychological role written for each — this is brand-voice and must be curated, not generated.
- [ ] Anchor-step selection per ramp: which step best 'represents' each color is a perceptual/taste judgment that should be eyeballed and confirmed by a human, not auto-picked.
- [ ] Neutral temperature: whether neutrals carry a slight hue bias toward the accent (and which direction) is a deliberate feel decision.
- [ ] Typeface selection and the display-vs-body pairing: the actual faces, their personalities, and whether display and body should visibly differ are core identity calls for the human.
- [ ] Role-family labels and how many tiers: the naming/wording of type roles and the exact count of families reflect the brand's content vocabulary.
- [x] **RESOLVED (policy):** The concrete numeric constants → **Defaults + per-project tuning.** Atelier ships proven default constants and tunes them per brand with human sign-off. See the Standing policy in method/00-decide.md. *(Per-project: the actual tuned numbers are still set each engagement.)*
- [ ] Component roster and family boundaries: which specialized siblings a given control (button, input, card) should split into depends on the product's actual needs — decide with the team.
- [ ] Elevation level → component/state mapping: the z-ordering contract (which surface sits at which depth) is a product-architecture decision.
- [ ] Density strategy: whether the project needs a parallel compact library at all, and where the density line falls, is a scope/UX call.
- [ ] Page section sequence and the funnel arc: the specific section order, where narrowing grid-breaks land, and what proof recurs where are per-page editorial/conversion judgments the human should own.
- [x] **RESOLVED (policy):** Signature boldness → **Always exactly one bold move per project.** Mandated by the method as atelier's core anti-slop guarantee. See the Standing policy in method/00-decide.md. *(Per-project: WHERE to spend the one bold move stays a human call each engagement.)*


## New taste/scope calls surfaced by Source 03 (dashboard / shadcn)

- [ ] Token method per project: with a third option now on the table (thin semantic-variable layer), the color-method choice is tonal-ramp vs category-color vs thin-semantic — decide per engagement by product type (rich app → thin-semantic; taxonomy shop → category; expressive formal library → ramp), and state why in the brief.
- [ ] Dark-mode strategy: whether the project ships a dark theme at all, and if so whether via value-mode twins on one semantic name (thin-semantic method) or via per-element ramp-step reselection (ramp method) — a taste + scope call tied to the token method chosen.
- [ ] Radius strategy: one global radius knob (flat/uniform app idiom) vs size-keyed per-component radius (expressive component family). The two are mutually exclusive; pick by product character.
- [ ] Elevation strategy: flat 1px-ring (dense, tiling, flat UI) vs two-layer ambient+contact shadow ramp (expressive/marketing surfaces). Choose by product; don't mix idioms within one system.
- [ ] Density tiers: does the product need a data-dense surface at all, and if so where the density line falls (does it warrant the micro-spacing sub-rungs and a parallel compact register) — a UX/scope call.
- [ ] Component-model stance: own-the-atom copy-paste source (naming-contract portability, no upgrade lock-in) vs a versioned shared component package — an engineering/governance decision with design consequences.
- [ ] Role model: whether the product is multi-role, the actual role set and view inventory, and the contents of the permission matrix (who sees/can-do what) — a product-architecture decision that must be authored as one artifact before menus or guards are built.
- [ ] Empty/loading/error copy and CTA policy: the wording per widget-kind empty state and the rule for when a role-gated CTA appears — brand-voice plus permission policy the human should own.
- [ ] Nav structure: the labeled section grouping, slot order, which items carry count badges, and which display modes the rail must support — an IA decision per app.
- [ ] Where the one bold move lives in a dashboard: at density the usual boldness levers (hero scale, decorative color) are unavailable, so the single deliberate bold move must be spent elsewhere (e.g. a signature data-viz treatment, a distinctive nav-rail behavior, an unexpected but disciplined accent) — a per-project taste call under the standing one-bold-move policy.


## New taste/scope calls surfaced by Source 04 (storefront)

- [ ] Storefront anatomy (new Section 8) and the page-skeleton library (new Section 9) are a *conditional* method layer — they apply only when the product IS a transactional commerce storefront. Confirm atelier's decision brief gains a 'product archetype' gate (storefront / dashboard / marketing-site / app) that selects whether Sections 8–9 are in scope, parallel to the existing color/token-method choice.
- [ ] The responsive-component discipline (new Section 5a) is proposed as UNIVERSAL (applies to every component in every project, not just storefronts), since 'author 3 breakpoints from their own frames' was already a standing rule and this only specifies how. Confirm it should be promoted to the always-on spine rather than gated as storefront-only.
- [ ] Where to spend the mandated single bold move on a storefront is still a per-project human call, but storefronts have strong conventional pulls (hero, mega-menu, PDP gallery). Decide whether atelier recommends spending boldness on a NON-conversion surface (editorial/brand-story bands, the journal rail) so the bold move never fights the funnel.
- [ ] The buybox sub-skeleton order is given as a fixed canonical sequence (identify→trust→price→configure→commit→reassure→detail). Confirm this is a hard default that requires an explicit documented reason to depart from, versus a soft recommendation.
- [ ] Representative device-width anchors (~wide/medium/narrow) are kept deliberately non-numeric in the method. Confirm atelier should NOT pin literal breakpoint px in the portable methodology (keeping them a per-project tuning value), consistent with the 'defaults-then-tuning' standing policy.


## New taste/scope calls surfaced by Source 05

- [ ] DECISION — Color method framing: adopt the 'composable TIERS, not a forced choice' framing. This revises spine rule 5 (which currently reads as 'pick ONE method'). Confirm you want the spine edited to say the register determines how many tiers you expose, with app = ramp-under-semantic stack. This is an ambiguity-resolution, not a contradiction, but it touches a numbered spine rule so it needs sign-off.
- [ ] DECISION — Adopt-don't-author the primitive tier: this legitimizes skipping bespoke, contrast-measured ramp authoring (currently the core craft of method A) when an off-the-shelf utility palette is used in an app register. Confirm atelier wants to sanction 'adopt a utility palette wholesale' as a first-class option, with the caveat that per-step contrast must still be verified at the semantic-selection tier.
- [ ] DECISION — Letter-spacing law downgrade: this source DISCONFIRMS 'strongly negative tracking on large display' as universal and reframes it as a register knob defaulting to 0. Confirm you want the type doc's tracking rule rewritten from a law to a register-tunable coefficient (editorial/luxury = negative; neutral/technical = 0).
- [ ] DECISION — Register taxonomy now has (at least) five construction methods: ramp library, category-color commerce, thin-semantic app, warm-retail storefront, and greybox/wireframe kit. Confirm you want the greybox kit added to the method-pluralism list as a peer register rather than a variant.
- [ ] NOTE (no decision needed): one of five layers (page-anatomy skeletons) was BLOCKED by a placeholder 'undefined' fileKey and contributed zero evidence. The skeleton catalogue is unchanged by this source. If you expected skeleton findings, the source must be re-run with a valid key.


## New taste/scope calls surfaced by Source 06

- [ ] Color-register taxonomy now has FOUR members (tonal-ramp, category-color, thin-semantic, brand-dominant). Confirm the atelier ledger should treat these as a closed enumerated set with an explicit selection heuristic (taxonomy? → category-color; neutral app chrome? → thin-semantic; single strong brand identity? → brand-dominant; role-tinted neutral UI? → tonal-ramp), or keep it open for a possible 5th.
- [ ] Decide the canonical name for the dual-ground foreground discipline (e.g. ground-aware semantic PAIRS: text-on-light / text-on-brand) and whether it is promoted to a universal semantic-tier requirement or kept register-scoped to brand-dominant/high-contrast registers only.
- [ ] Density oscillation now has a documented SECOND axis (surface-weight) beyond height. Confirm whether the portable rule becomes 'oscillate on all salient weight axes (height, surface-saturation, content-density)' generally, or stays flagged as expressive-register-only.
- [ ] Confirm that 'two altitudes of reuse' (atomic library + counted block collections) is adopted as a standing component-architecture requirement, and decide whether the 'Total Blocks: N' count contract is mandated for every block collection atelier ships.
- [ ] Decide whether the non-standard page families (quiz funnel, RMA state-frames, slide-outs-as-templates) are added to the default storefront skeleton catalogue as always-considered [optional] entries, or only surfaced when a brief implies them.


## New taste/scope calls surfaced by Source 08

- [ ] Category-token model: standardize on emitting every catalog category as a {accent, tint} pair kit at mint time? This changes the token schema library-wide (prior sources treated category color as a single accent). Confirm before it becomes the default.
- [ ] Scope-driven accent with brand fallback: adopt 'chrome = brand constant; content region = category variable; nothing-in-scope = brand primary' as the standing color-routing contract across all future catalog builds?
- [ ] Typeface budget: ratify the 'up to 3 purposeful faces partitioned by role-class (structure / reading / action)' rule as an allowed pattern — and set whether it is opt-in per brief or a recommended default when separation is wanted.
- [ ] Intentional anti-DRY tokens: confirm the token model should permit duplicate-value distinct-role tokens (name by intent, never collapse value-identical roles). This is a deliberate reversal of normal DRY instinct and should be explicitly sanctioned.
- [ ] Page-anatomy catalogue restructure: upgrade the catalogue from a flat page list to the FOUR-TRACK form (full pages / overlays / state variants / responsive rule). Confirm this becomes the canonical catalogue shape going forward.
- [ ] Composition primitive library: accept diagonal seam, stacked-deck fan, tilted divider planes, and interstitial reset band as named, reusable composition primitives — and decide whether the angled/rotated ones are register-gated (playful only) or allowed in restrained builds too.
