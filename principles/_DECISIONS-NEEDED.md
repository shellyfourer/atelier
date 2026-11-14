# Taste & judgment calls awaiting the human

> Collaborative curation (your choice). These are NOT auto-decided. Resolve, then fold into methodology.md / anti-slop.md.

- [ ] Hue inventory and palette intent: which hue families exist, how many ramps per family, and the editorial psychological role written for each — this is brand-voice and must be curated, not generated.
- [ ] Anchor-step selection per ramp: which step best 'represents' each color is a perceptual/taste judgment that should be eyeballed and confirmed by a human, not auto-picked.
- [ ] Neutral temperature: whether neutrals carry a slight hue bias toward the accent (and which direction) is a deliberate feel decision.
- [ ] Typeface selection and the display-vs-body pairing: the actual faces, their personalities, and whether display and body should visibly differ are core identity calls for the human.
- [ ] Role-family labels and how many tiers: the naming/wording of type roles and the exact count of families reflect the brand's content vocabulary.
- [x] **RESOLVED (policy):** The concrete numeric constants → **Defaults + per-project tuning.** Atelier ships proven default constants and tunes them per brand with human sign-off. See "Standing policy" in methodology.md. *(Per-project: the actual tuned numbers are still set each engagement.)*
- [ ] Component roster and family boundaries: which specialized siblings a given control (button, input, card) should split into depends on the product's actual needs — decide with the team.
- [ ] Elevation level → component/state mapping: the z-ordering contract (which surface sits at which depth) is a product-architecture decision.
- [ ] Density strategy: whether the project needs a parallel compact library at all, and where the density line falls, is a scope/UX call.
- [ ] Page section sequence and the funnel arc: the specific section order, where narrowing grid-breaks land, and what proof recurs where are per-page editorial/conversion judgments the human should own.
- [x] **RESOLVED (policy):** Signature boldness → **Always exactly one bold move per project.** Mandated by the method as atelier's core anti-slop guarantee. See "Standing policy" in methodology.md. *(Per-project: WHERE to spend the one bold move stays a human call each engagement.)*


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
