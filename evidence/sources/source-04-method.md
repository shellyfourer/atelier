# Source 04 — method notes (Shopify storefront, warm-retail register)

> Anonymized. A full Shopify storefront in a warm/soft retail register. Teacher, not template.
> Its biggest value is (a) a SECOND independent confirmation of the ramp + composite-type
> architecture, and (b) genuinely new method: responsive-component discipline, storefront
> anatomy, and the page-skeleton library.

# Source 04 — method notes (warm-retail commerce storefront)

> Anonymized. A commerce storefront in a warm retail / craft register, built on a theme-driven
> stack, studied for *method* only — no client palette, fonts, copy, niche, or screens retained.
> Teacher, not template. Its value is three disciplines the prior three sources under-covered:
> (1) a formal **responsive-component method** (how a *single* component is authored across
> breakpoints); (2) **storefront anatomy** — the component classes specific to an operating shop;
> and (3) a **page-skeleton library** — the per-page-type section stacks and the chrome-vs-body
> split that lets one system span ~10 page types without redundancy.

# Source 04 — method notes (fourth source)

_Confidence: high (direct study of three authored breakpoint frames per template across ~10 page
types; a header/nav component set with an open-state overlay; a two-pane mega-menu; a faceted
collection page; a full PDP buybox; a cart drawer and a full cart page; a store-info footer; a
trust strip; editorial/auth/account templates; and a family of promo primitives)._

A warm-retail/craft storefront, studied as a *teacher*. Most of its token architecture, type
pairing, spacing scale, warm register, and page-rhythm **re-confirm** Sources 01–03 (see "What this
source confirms" below) and are not re-stated in the methodology. Its genuinely new contribution is
in three places the prior sources left thin:

- **Responsive-component discipline** — the prior sources all assert "author three breakpoints from
  their own frames," but never specified *how one component is modelled across them*: what
  collapses, what stays fixed, in what priority order. Source 04 makes this an explicit, portable
  method.
- **Storefront anatomy** — the component classes (utility cluster, two-pane mega-menu, faceted
  collection, PDP buybox stack, cart drawer, store-info footer, trust strip, promo primitives) an
  *operating retail shop* carries, that a dashboard / configurator / formal library does not.
- **Page-skeleton library** — a `GLOBAL CHROME + per-template BODY STACK` model, with a named,
  tagged (required/recommended/optional) section stack for each page type and a named buybox
  *sub*-skeleton. This is the "which sections, in what order, on which page" layer that sits
  *above* Section 5's band-chassis grammar.

**Portable vs discard.** Portable = the three methods below (the component-level reflow contract;
the storefront component classes and their internal order; the chrome/body page-skeleton split and
its per-type body stacks). Discard = the warm palette values, the specific faces, the niche, the
exact device widths (~1512/1024/440 are representative, not sacred), and all copy. Learn *that* a
utility cluster is a distinct component class, *what order* a buybox stacks, and *which* sections a
PLP must carry; forget the brand's cart glyph.

## What this source confirms (compactly — NOT re-added to the methodology)

Re-confirmed, strengthening confidence but adding no new rule:

- **Multi-tier token architecture** (raw ramp → semantic role → component token; author/consume at
  semantic+component, never raw hex/px). Confirms the spine.
- **Two-family type pairing** driven by a role×size ramp of composite tokens (display/headline for
  marketing headers + a workhorse grotesk for body/UI). Confirms Section 2.
- **Warm-retail color & type register** — multiple curated named ramps per family, a warm-drifted
  dark end, muted brand backgrounds sourced from the lightest ramp steps, an inverse optical-tracking
  ramp, hierarchy by family+size+color-step rather than heavy weights, a softened warm near-charcoal
  primary text instead of pure black. **Already captured** from the earlier warm-retail color/type
  study — Source 04 is a second independent confirmation, not new.
- **Fixed 4-based spacing/radius scale**; pill/full radius reserved for buttons/tags/avatars, larger
  block radius for cards/containers. Confirms Section 3.
- **Three authored breakpoint frames** per template, each its own layout. Confirms the responsive
  premise — but see §A for the *component-level* method it adds on top.
- **Section rhythm** (wide outer band + section padding, max-width inner container, grid-gap tokens
  differing by column count), **density oscillation**, **threaded social proof**,
  **grid-break-as-narrowing**, the **repeating section-header triad**, the **full-bleed lifestyle
  hero with copy in the image's negative space**, **zig-zag editorial alternation**, **images
  interleaved between paragraphs**, **varied shoppable-band formats**, and **in-place tabbed category
  filters**. Confirms Section 5 (page composition) — re-confirms the band chassis rather than
  extending it.
- **Tokenized named effect styles** (layered drop-shadows, background blur, a skeuomorphic
  inner-shadow button) rather than ad-hoc shadows. Confirms the elevation-as-named-ramp rule.
- **Reusable product-card molecule** (image / category eyebrow / title / price / swatch row) shared
  across home, PLP, PDP cross-sell, and cart. Confirms the atomic-molecule reuse rule — Source 04
  pins down the card's exact slots (see §B).

## Method principles learned here (genuinely new)

### A. The responsive-component method (how one component spans breakpoints)

The prior sources said *build each breakpoint from its own frame*. This source specifies the
discipline of a **single responsive component** — the part neither Source 03's "reflow by collapsing
column count" nor Section 5's band chassis fully pinned down.

- **One component set, a `Breakpoint` variant property = {Desktop, Tablet, Mobile}.** Model a
  responsive component (header, footer, nav) as ONE set whose variants are siblings, not three
  unrelated frames. Each variant is explicitly drawn at a fixed device-width anchor (wide / medium /
  narrow) with a fixed inner container and page padding that **steps DOWN** as width narrows (blocks
  grow to fill the narrower container rather than the gutter shrinking). *Why:* keeps all breakpoints
  addressable together, makes the diff between them legible, and signals that identity is shared
  while layout differs.
- **Reflow is a priority-ordered set of explicit decisions, never emergent flexbox.** The contract,
  in order:
  1. **NAV collapse threshold.** Inline horizontal nav links exist *only* at the widest breakpoint.
     At the first step down they are removed from the bar entirely and replaced by a hamburger beside
     the logo. The **bar height stays constant** across all breakpoints. *Why:* a cramped inline nav
     reads as unfinished; the collapse is a discrete swap at a named threshold, not a wrap.
  2. **ACTION icons shed by priority.** The utility icon cluster drops lower-priority items as width
     shrinks (e.g. 5→4→3), keeping the highest-value actions (search, cart) at every breakpoint;
     survivors keep their size and order. *Why:* trim secondary affordances by priority rather than
     shrinking hit targets — never compress everything uniformly.
  3. **OVERLAY state is co-located.** The expanded/open menu is authored as a hidden child frame
     *inside the same breakpoint variant*, not as a separate screen. Collapsed nav reappears as a
     full-width accordion (chevron per section) with its own pinned action footer; any rich mega-menu
     grid re-tiles to fewer columns (e.g. 3-up → 2-up) inside that panel. *Why:* the open state is
     specced in-place so the two never drift.
  4. **MULTI-COLUMN blocks follow a column-count ladder** N → N/2 → 1. Each block is a fixed-width
     unit that **widens step-wise** as columns drop, and reading ORDER is preserved via predictable
     x/y placement. *Why:* a portable recipe for the footer/grid → stacked collapse.
  5. **BANDS vs GRIDS.** Distinguish band-spanning rows from grid blocks: a newsletter /
     section-header + input row stays full-width at *every* breakpoint (only its width tracks the
     container) while the link columns below it re-grid. A composed field+button goes from a compact
     fixed-width block to a full-width field with the button pinned inline at its trailing edge.
     *Why:* not every element reflows the same way.
  6. **BOTTOM utility bar may stack AND reorder.** A right-aligned horizontal group (legal + payment
     badges) opposite copyright on wide screens becomes a vertical stack on mobile with the
     badges/legal promoted *above* the fine print. *Why:* correct responsive behavior sometimes
     reorders by importance when stacking, not merely linearizes top-to-bottom.

- **The throughline:** identity and tokens are shared across all three variants; what changes per
  breakpoint is **column count, nav disclosure, icon priority, and stacking order** — each an
  explicit authored decision, never an emergent accident. Hit-target sizing for interactive controls
  is held constant across breakpoints.

### B. Storefront anatomy (component classes an operating shop carries)

Distinct from Source 02's category-color commerce (which was about *palette as wayfinding*): this is
the *compositional anatomy* of the storefront's chrome and templates.

- **Header = category NAV + a right-pinned UTILITY CLUSTER, as different component classes.** Center/
  left holds category links (carets on parents); the right cluster holds, in order, locale/currency
  switcher → search → promo/offers entry (often badged) → account → cart bag. *Why:* storefronts
  carry transactional/global affordances a dashboard header lacks; isolating them keeps center nav
  clean and makes locale/cart reachable everywhere.
- **Mega/category menu is a TWO-PANE merchandising surface,** not a link list: a left rail of
  category links each with a one-line descriptor, beside a right pane of featured/popular product
  cards. *Why:* converts hover time into product discovery; the descriptor rail teaches taxonomy.
- **Collection page = fixed control header (title + live result count + sort) over a two-column
  body** (left collapsible filter sidebar with color-swatch facets + active-filters/clear row |
  responsive product-card grid). On mobile the sidebar collapses behind a "Filter" trigger and
  commits via a **sticky bottom "Show results"** bar. *Why:* faceted filtering + visible count + sort
  is the core collection contract; collapse-to-drawer with sticky commit is the portable mobile rule
  for any filter-heavy listing.
- **Product card is a fixed slot stack** (image + optional corner badge → optional material microcopy
  → swatch/variant row → title → price with sale emphasized in accent + struck original), with
  **card width bound to a block-size token** so grids reflow by changing column count, not card size.
  *Why:* one card then serves grids, carousels, cross-sell rails, and mega-menu panes, and reflows
  cleanly everywhere.
- **PDP = sticky thumbnail+main gallery | a conversion-ordered BUYBOX stack:** breadcrumb → title →
  rating + review count → price → short description → variant/option selectors → quantity stepper →
  primary add-to-cart + secondary action → inline trust row (shipping/returns/secure) → collapsible
  spec accordions. *Why:* this order mirrors the decision funnel (identify → trust → price →
  configure → commit → reassure → deep-detail); sticky gallery + accordion detail keeps the commit
  action in view on long PDPs. Don't reorder price above identity or bury ATC below the fold without
  a sticky.
- **Cart is a slide-out DRAWER (as well as a page):** header with item count, line items, and a
  **free-shipping / threshold PROGRESS** indicator. Its EMPTY state is a merchandising surface
  (cross-sell rows + "view all products"), never a dead end. *Why:* the drawer keeps shoppers in
  context; the threshold line is a storefront upsell primitive; a populated empty state recovers
  dead-ends into discovery. (The *full cart page* is a different skeleton — see §C.)
- **Footer = a physical-retail STORE-INFO taxonomy** in parallel columns: shop categories | store/
  company links | **store opening hours** | **contacts** (address, email, social) — plus a locale/
  currency switcher, a legal/copyright row, and a **payment-badge row**. *Why:* hours, address, local
  switcher, and payment marks signal a legitimate operating business; this column taxonomy is the
  reusable storefront footer contract.
- **Newsletter signup is a DISCOUNT-CAPTURE block,** not a bare form: value-led headline naming the
  incentive, a single email field + submit, and a fine-print consent line linking terms/privacy.
  Placed as a distinct band above the footer columns. *Why:* ties list capture to a first-order
  discount and bakes in compliance microcopy.
- **Trust signals ride one dedicated full-width STRIP** of icon+label pairs (delivery threshold,
  secure-commerce, social proof, materials/quality), placed right below the primary nav or hero.
  *Why:* consolidating reassurance front-loads credibility above the fold; a reusable band
  independent of niche. (Complements Section 5's "threaded proof" — the strip is one scannable node
  in that thread.)
- **Promotions are a layered system of reusable primitives:** an announcement/top banner, a moving
  marquee band, timed popups (bonus / discount-code), an offers/bundle surface, and a slide-out
  offers panel — each a tokenized component so campaigns swap content without relayout. *Why:*
  ecommerce runs continuous promo campaigns; naming these as reusable surfaces lets merchandising
  change copy and timing without touching layout.

### C. The page-skeleton library (chrome/body split + per-type section stacks)

Where Section 5 teaches the band *grammar* (how any one band is built) and §B teaches the storefront
*component classes*, this is the layer above both: **which sections, in what order, on which page
type** — stored so one system spans ~10 page types without redundancy.

- **Model every page as `GLOBAL CHROME + BODY STACK`, not one flat section list.** CHROME =
  {promo/announcement bar [optional], header/nav [required], footer [required]} — authored **once**
  and template-invariant. Each template defines *only* its BODY stack. *Why:* every frame repeated
  the identical banner→header…footer wrapper; modeling chrome once keeps the skeleton library DRY and
  portable.
- **Deep/transactional pages prepend a breadcrumb** as the first in-body element (PDP, PLP, cart,
  blog post, account, auth, legal); the homepage does not.
- **Each page type has a named, tagged BODY stack** (tags: required / recommended / optional; order
  = top→bottom):
  - **HOME:** hero+CTA [req] → trust/USP ticker strip [rec] → primary product rail, tab-filterable
    [req] → lookbook/editorial rail [opt] → value-props "why us" split [rec] → reviews/social-proof
    wall [rec] → featured/bestseller rail [rec] → UGC/shoppable rail [opt] → brand-story/journal rail
    [opt] → press/logo strip [opt] → newsletter capture [rec]. **Rule:** alternate
    PRODUCT-DISCOVERY bands with TRUST/STORY bands so the page never reads as a pure catalog dump.
  - **PLP / COLLECTION:** breadcrumb [rec] → collection header (title+description) [req] →
    subcategory tile rail [opt] → browse region {filter sidebar [rec] + toolbar(result count + sort)
    [req] + product grid [req] + pagination / "viewed X of Y" + load-more [rec]} → cross-sell rail
    [opt]. **Irreducible core = the toolbar (count+sort) and the grid**; filters degrade to a drawer
    on mobile.
  - **PDP:** breadcrumb [rec] → {media gallery (stage + thumbnail strip) [req] | BUYBOX} → aggregate
    rating summary (histogram + customer-media gallery) [rec] → sortable review list [rec] →
    editorial/content split [opt] → FAQ accordion [opt] → benefits split [opt] → related-products
    rail [rec].
  - **CART (full page, not the drawer):** breadcrumb → header + incentive bar (free-shipping progress
    / optional urgency) [rec] → two-column body {left: line-item list + in-cart cross-sell rail |
    right: order-summary panel (collapsible cost breakdown, grand total, note/gift field, checkout
    CTA, payment badges) + reassurance block (privacy / SSL / guarantee)} → cross-sell rail. **The
    summary panel is sticky-eligible and must bundle total + CTA + payment proof together.**
  - **BLOG POST:** breadcrumb → hero image → title + meta (author/date/read-time) → rich body
    constrained to a readable measure → tag chips + share row → prev/next pager → related-posts rail.
  - **ABOUT / STORY:** full-bleed hero image → alternating image|text split bands → value-prop/
    benefits split.
  - **AUTH (login/signup):** breadcrumb → {form (heading, stacked fields, inline security line,
    primary submit, alt-action link) | brand image}.
  - **ACCOUNT DASHBOARD:** breadcrumb → heading + sign-out → stacked editable info blocks (contact
    details, shipping address) each with an inline edit affordance.
  - **LEGAL:** breadcrumb → title → long-form rich text at a constrained measure.
- **The BUYBOX is a named *sub*-skeleton** with its own strict internal order, reusable across any
  product type (physical, digital, gift card): rating + cert badges → title → spec/attribute chips →
  short description → price (+ discount badge) → variant swatches → option controls
  (dropdown/segmented/qty stepper) → primary ATC → payment-method badges → micro trust strip →
  collapsible detail accordions → inline mini cross-sell. *Why:* it recurs verbatim; promote it to a
  named sub-skeleton rather than re-deriving it per product.
- **Section order is breakpoint-invariant.** A file that ships ~3 frames per page proves the stack is
  responsive-invariant: **author the desktop frame as the canonical skeleton and derive mobile by
  column-collapse + drawer-izing filters — never by re-ordering sections.** (Pairs with §A, which
  governs how each component within those sections reflows.)
- **Universal closers.** The **cross-sell / "you may also like" rail** closes nearly every commerce
  page (PDP, cart, PLP, blog). **Editorial pages (blog/about/legal) constrain the body to a readable
  measure and end in *lateral* navigation (related/next), never a buy-CTA** — a distinct skeleton
  family from commerce pages.

## Anti-slop rules learned here (new)

**Responsive component:**
- Don't ship a single fluid layout and call it responsive — author an explicit variant per
  breakpoint so each reflow is a deliberate decision, not a flexbox side effect.
- Don't keep inline horizontal nav links on tablet/mobile "because they fit" — collapse to a
  hamburger at the defined threshold; hold the bar height constant.
- Don't shrink icon/touch targets to fit a toolbar — drop lower-priority icons by priority and keep
  the survivors at full hit-target size.
- Don't author the menu/overlay open-state as a disconnected separate screen — co-locate it as a
  hidden state inside the component.
- Don't merely wrap multi-column content when stacking — choose column count per breakpoint
  (N → N/2 → 1), widen the block to fill, and consciously choose stacking order (promote high-value
  items).
- Don't reflow every element uniformly — keep band-spanning rows (newsletter/hero input) full-width
  while only the grid columns collapse.

**Storefront anatomy:**
- Don't merge primary nav and the utility cluster into one undifferentiated menu.
- Don't ship a retail category menu as a plain link list — include the descriptor rail and a
  featured-product pane.
- Don't render an empty cart as a dead end — cross-sell rows + "view all" path.
- Don't omit the free-shipping/threshold progress line from the cart drawer.
- Don't build a thin link footer — carry hours, address, contacts, locale switcher, legal row, and a
  payment-badge row.
- Don't present newsletter signup as a bare form — lead with the discount incentive and include
  consent microcopy.
- Never hardcode product-card width in px — bind it to a block-size token.
- Don't scatter trust signals — consolidate into one icon+label strip below nav/hero.
- On mobile, filters must collapse behind a Filter trigger with a sticky "Show results" commit bar.
- Preserve the PDP buybox order; don't put price above identity or bury ATC without a sticky.

**Page-skeleton library:**
- Don't model a page as one flat section list — split GLOBAL CHROME (authored once) from the
  per-template BODY stack.
- Don't treat the slide-out mini-cart and the full cart PAGE as the same skeleton — the page adds
  breadcrumb, incentive bar, a two-column summary+reassurance, and a cross-sell rail.
- Don't omit the convince/convert alternation on a homepage — pure stacked product rails with no
  trust/story bands read as a catalog dump.
- Don't flatten the PDP buybox into "title+price+button" — it's an ordered named sub-skeleton.
- Don't give long-form/editorial pages a full-width body or a buy-CTA ending — constrain the measure
  and close with related/next navigation.
- Don't re-order sections per breakpoint — keep order invariant; collapse columns / drawer-ize
  filters instead.
- Don't forget the PLP toolbar (result count + sort) and a progressive load affordance — they're the
  irreducible core, not decoration.
