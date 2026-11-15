# atelier — page-skeleton library

> The canonical section structure of each common page type: what sections a page SHOULD
> have, in what order, and why. Each section tagged **[required] / [recommended] / [optional]**.
> Portable skeletons — structure and rationale, never a brand's specific content.
>
> **Scope note:** currently source-extracted (distilled from real store/app designs). A dedicated
> SEO / AEO / CRO research pass is planned to harden these for conversion, semantic HTML, heading
> hierarchy, structured data, and AI-crawl depth. Until then, treat conversion/SEO notes as
> provisional. See the roadmap in README.md.

# Page-Skeleton Library (`method/page-skeletons.md`)

Cross-source, portable section-stack library for `atelier`. Synthesized from the page-anatomy findings (warm-retail storefront) plus the collective coverage of four sources: a storefront, a product-configurator commerce project, and a dashboard app. These are **portable skeletons** — the ordered sections a page type should contain and in what order — never brand content. Learn the structure, pour your own copy/tokens/imagery in.

## How to read this

- Every page = **GLOBAL CHROME** (authored once, template-invariant) wrapping a per-template **BODY STACK**. Model them separately or you duplicate the wrapper ~12 times.
- Tags: **[required]** = page is broken/incomplete without it · **[recommended]** = expected by the register, omit only with a reason · **[optional]** = include when content/campaign warrants.
- **Section order is breakpoint-invariant.** Author the stack at desktop; derive tablet/mobile by *collapsing columns* and *drawer-izing* sidebars/filters — never by re-ordering.
- Deep/transactional pages (PLP, PDP, Cart, Checkout, Blog article, Account, Auth, Legal) prepend a **breadcrumb** as the first in-body element. Landing/Home does not.
- The **product-card molecule** (image+badge / category eyebrow / title / price / swatch row) is the shared atom across Home, Collection, cross-sell rails, and Cart. The **cross-sell rail** closes almost every commerce page.

---

## GLOBAL CHROME (wraps every page; author once)

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Announcement / promo bar (optional marquee) | [optional] | Campaign-swappable band for offers, shipping thresholds, urgency; present on most but not all pages. |
| 2 | Header: brand + **primary category nav** (carets on parents) | [required] | Center/left category links are the page-to-page wayfinding spine. |
| 3 | Header **utility cluster** (right-pinned): locale/currency → search → offers/promo (badgeable) → account → cart bag | [required] | Transactional/global affordances kept distinct from nav so locale + cart are reachable everywhere; dashboard/B2B headers lack this cluster. |
| 4 | Mega/category menu (two-pane: descriptor rail + featured-product carousel) | [recommended] | Retail register turns nav hover into discovery; plain link lists waste the surface. |
| — | **{BODY STACK}** | — | Per-template, defined below. |
| 5 | Footer: parallel columns (shop categories · store/company links · opening hours · contacts+social) | [required] | Physical-retail taxonomy signals a legitimate operating business. |
| 6 | Footer: newsletter **discount-capture** band (incentive headline + email + consent microcopy) | [recommended] | Reframes list capture as a conversion offer; consent line bakes in compliance. |
| 7 | Footer: locale/currency switcher · legal/copyright row · **payment-badge row** | [recommended] | Closes the trust/compliance contract for a storefront. |

> Anti-slop: do not merge primary nav and utility cluster into one undifferentiated menu; do not ship a thin footer of bare links.

---

## 1. Landing / Home

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Full-bleed lifestyle hero, copy set into the image's negative space + primary CTA | [required] | First conversion moment; lifestyle hero (not 50/50 split, not centered) sets the register. |
| 2 | Trust / USP ticker strip (icon+label chips: rating, shipping threshold, origin, guarantee) | [recommended] | Front-loads credibility above the fold as one scannable band, not scattered. |
| 3 | Primary product rail, tab-filterable by category | [required] | Core discovery; in-place tabs expose catalog breadth without spawning a section per category. |
| 4 | Editorial / lookbook rail | [optional] | Calm full-bleed break between dense product bands (density oscillation). |
| 5 | Value-props / "why us" split (icon list + image) | [recommended] | Story/trust band that interrupts pure catalog rhythm. |
| 6 | Reviews / social-proof wall | [recommended] | Pooled proof moment; credibility also threads the page elsewhere. |
| 7 | Featured / bestseller rail | [recommended] | Second discovery band, re-skinned product-card molecule. |
| 8 | UGC / shoppable "shop-the-look" rail (creator avatar + price tag) | [optional] | Community browsing mode; varies the shoppable-band format. |
| 9 | Brand-story / journal (blog) rail | [optional] | Editorial warmth; pulls recent articles into the home scroll. |
| 10 | Press / logo / badge strip | [optional] | External validation. |
| 11 | Newsletter discount-capture band | [recommended] | Final conversion offer before footer (may live in chrome). |

> Rule: **alternate PRODUCT-DISCOVERY bands with TRUST/STORY bands** so the page never reads as a catalog dump. Oscillate density; break the grid to narrow the column on emotional moments.

---

## 2. Collection / Category (PLP)

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [recommended] | Orients within taxonomy on a deep page. |
| 2 | Collection header (title + description) | [required] | Names the set and its context. |
| 3 | Subcategory / child-collection tile rail | [optional] | Drills into taxonomy before committing to the grid. |
| 4 | Control toolbar: **live result count + sort** | [required] | Irreducible PLP core; count+sort is the contract. |
| 5 | Left filter sidebar: collapsible groups (category, **color swatch chips**, price range, attributes) + active-filters/clear row | [recommended] | Faceted filtering; swatch facets are retail-specific. |
| 6 | Responsive product-card grid (tokenized card width → reflow by column count) | [required] | The merchandise itself; grid reflows by changing columns, not card size. |
| 7 | Pagination OR "viewed X of Y" + load-more progress | [recommended] | Progressive reveal of a long catalog. |
| 8 | Cross-sell / related rail | [optional] | Recovery path if the collection didn't convert. |

> Mobile rule: filters **collapse behind a "Filter" trigger** and commit via a sticky bottom "Show results" bar — never an always-open sidebar.

---

## 3. Product / PDP

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [recommended] | Taxonomy orientation + back-path. |
| 2 | Hero row: media gallery (thumbnail strip + main stage, sticky on desktop) **\|** BUYBOX | [required] | Identify-the-product + the conversion panel side by side. |
| 3 | Aggregate-rating summary (histogram + customer-media gallery) | [recommended] | Deep social proof below the fold. |
| 4 | Sortable review list | [recommended] | Detailed proof for considered purchases. |
| 5 | Editorial / content split (story, materials) | [optional] | Re-grounds specs in warmth; imagery interleaves copy. |
| 6 | FAQ accordion | [optional] | Handles objections inline. |
| 7 | Benefits / "why this" split | [optional] | Reinforces value before exit. |
| 8 | Related / cross-sell rail | [recommended] | Standard closing discovery band. |

### BUYBOX micro-skeleton (ordered — do not reorder)

| Order | Element | Tag | Why |
|---|---|---|---|
| 1 | Star rating + review count (+ certification badges) | [recommended] | Trust before price (identify→trust→price funnel). |
| 2 | Title | [required] | Identity anchor. |
| 3 | Attribute / spec chips | [optional] | Fast at-a-glance facts. |
| 4 | Short description | [recommended] | One-line value framing. |
| 5 | Price (+ discount badge; sale emphasized in accent, original struck) | [required] | The decision number. |
| 6 | Variant selector (color/material swatches) | [required, if variants] | Configure the SKU. |
| 7 | Option controls (size dropdown / segmented / kit options) | [recommended, if options] | Configurator surface — critical for product-configurator commerce. |
| 8 | Quantity stepper | [recommended] | Standard commerce control. |
| 9 | **Primary add-to-cart** + secondary action | [required] | The commit; keep in view (sticky on long PDPs). |
| 10 | Payment-method badges | [optional] | Reassurance at point of commit. |
| 11 | Micro trust strip (secure / shipping / returns) | [recommended] | Reassures right after the CTA. |
| 12 | Collapsible detail accordions (specs/shipping/care) | [recommended] | Deep detail without pushing the CTA below the fold. |
| 13 | Inline mini cross-sell | [optional] | Attach/accessory prompt in context. |

> Anti-slop: never flatten the buybox to "title + price + button"; never put price above identity or add-to-cart below the fold without a sticky.

---

## 4. Cart (full page)

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [recommended] | Positions within the checkout path. |
| 2 | Header + incentive bar (free-shipping **progress** + optional urgency/countdown) | [recommended] | Threshold progress is a storefront upsell primitive. |
| 3 | **Left:** line-item list (image, title, remove, unit price, badge, qty stepper) | [required] | The order being edited. |
| 4 | **Left:** in-cart cross-sell rail | [optional] | Attach-rate lift while editing. |
| 5 | **Right:** order-summary panel (collapsible cost breakdown, grand total, note/gift field, **checkout CTA**, payment badges) — sticky-eligible | [required] | Bundles total + CTA + payment proof as one conversion panel. |
| 6 | **Right:** reassurance block (privacy / SSL / guarantee) | [recommended] | Calms friction at the money step. |
| 7 | Cross-sell rail | [optional] | Closing discovery band. |

> Note: the slide-out **mini-cart drawer** is a *different* skeleton — header + item count + threshold progress + line items, and its **empty state cross-sells** with a "view all products" escape (never a dead end).

---

## 5. Checkout

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Minimal header (brand + secure badge; nav/utility stripped) | [required] | Remove exits to protect conversion focus. |
| 2 | Breadcrumb / step indicator (Information → Shipping → Payment → Review) | [recommended] | Sets expectation and progress on a multi-step flow. |
| 3 | Contact / email field | [required] | Order identity + receipt destination. |
| 4 | Shipping address form | [required] | Fulfillment destination. |
| 5 | Delivery / shipping-method selector | [required] | Cost + speed choice. |
| 6 | Payment method (+ billing address) | [required] | The transaction. |
| 7 | Order review + place-order CTA | [required] | Final confirm before charge. |
| 8 | **Right-rail order summary** (line items, breakdown, total, discount-code field) — sticky | [required] | Keeps what's being bought and its total visible throughout. |
| 9 | Trust / reassurance strip (secure, returns, support) | [recommended] | Reduces last-step abandonment. |
| 10 | Minimal footer (legal + support links only) | [recommended] | Compliance without exit-tempting navigation. |

> Rule: checkout strips global chrome down to brand + security; the summary rail is non-negotiable and sticky.

---

## 6. About / Story

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [optional] | Light orientation; editorial pages can skip. |
| 2 | Full-bleed hero image + mission statement | [required] | Emotional entry; narrative not spec-sheet. |
| 3 | **Zig-zag** alternating image\|text story bands (image/text swap sides each block) | [required] | Imagery is a co-equal narrative column; alternation prevents a stacked list. |
| 4 | Inline mini-benefit grids within story blocks | [optional] | Grounds narrative in concrete value. |
| 5 | Values / benefits split (icon list + image) | [recommended] | Consolidates the "why us" before CTA. |
| 6 | Team / makers band | [optional] | Humanizes the brand. |
| 7 | Press / credibility strip | [optional] | External validation. |
| 8 | Lateral CTA (explore collection / journal) — **not a hard buy** | [recommended] | Editorial pages close with discovery, not a conversion button. |

---

## 7. Contact

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [optional] | Light orientation. |
| 2 | Page heading + short intro | [required] | Names the page and sets expectation. |
| 3 | Contact form (name, email, subject, message, consent) | [required] | Primary action. |
| 4 | Direct-contact block (email, phone, address, **opening hours**) | [required] | Physical-retail legitimacy; alternatives to the form. |
| 5 | Map / location embed | [optional] | For a store with a physical presence. |
| 6 | Social links | [optional] | Alternate channels. |
| 7 | Support/FAQ shortcut or deflection links | [optional] | Reduces inbound volume. |

---

## 8. Blog Index

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [optional] | Orientation. |
| 2 | Index header (title + description) | [required] | Names the journal. |
| 3 | Featured / hero post | [recommended] | Anchors the page with the lead story. |
| 4 | Category / tag filter row | [recommended] | Lets readers narrow by topic. |
| 5 | Responsive post-card grid (image, category eyebrow, title, excerpt, meta) | [required] | The article listing itself. |
| 6 | Pagination OR load-more | [recommended] | Progressive reveal of the archive. |
| 7 | Newsletter / subscribe band | [optional] | Converts readers to subscribers. |

---

## 9. Blog Article

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [recommended] | Orientation back to index/category. |
| 2 | Hero image | [recommended] | Visual entry to the piece. |
| 3 | Title + meta (author / date / read-time) | [required] | Identity + context. |
| 4 | Rich-text body at **constrained measure (~768px)**, lifestyle images interleaved between paragraphs | [required] | Readability; interleaved imagery prevents a text wall. |
| 5 | Tag chips + share row | [recommended] | Topical connection + distribution. |
| 6 | Author bio block | [optional] | Credibility + voice. |
| 7 | Prev/next pager | [recommended] | Lateral navigation close (not a buy CTA). |
| 8 | Related-posts rail | [recommended] | Keeps readers in the journal. |

---

## 10. Account / Dashboard Overview

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [recommended] | Position within account area. |
| 2 | Page heading + sign-out | [required] | Identity + exit. |
| 3 | Account nav (sidebar or tabs: orders, details, addresses, payment, wishlist) | [recommended] | Wayfinding across account sub-pages (dashboard-app pattern). |
| 4 | Summary / at-a-glance cards (recent order, loyalty, store credit) | [recommended] | Dashboard-overview glance layer before detail. |
| 5 | Recent orders list (status, date, total, re-order/track) | [recommended] | Most common account task surfaced first. |
| 6 | Stacked **editable info blocks** (contact details, shipping address) with inline edit affordance | [required] | Labeled editable cards are the core dashboard pattern. |
| 7 | Secondary actions (payment methods, password, preferences) | [optional] | Less-frequent management tasks. |

---

## 11. Pricing

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [optional] | Orientation. |
| 2 | Heading + value proposition | [required] | Frames what's being priced. |
| 3 | Billing toggle (monthly/annual) or currency switcher | [recommended] | Primary pricing control. |
| 4 | **Plan / tier cards** (name, price, feature list, per-plan CTA, highlighted recommended tier) | [required] | The core pricing decision surface. |
| 5 | Feature comparison table | [recommended] | Side-by-side for considered buyers. |
| 6 | Trust / logos / testimonials | [recommended] | De-risks the commitment. |
| 7 | FAQ accordion (billing, cancellation, refunds) | [recommended] | Clears pricing objections. |
| 8 | Final CTA / contact-sales band | [recommended] | Captures decided and enterprise buyers. |

---

## 12. Auth (Login / Signup)

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [optional] | Light orientation. |
| 2 | **Centered form \| brand image split** | [required] | Single focused form flanked by a reassurance/brand panel. |
| 3 | Heading + sub | [required] | Names the action (sign in / create account). |
| 4 | Social / SSO buttons (if offered) | [optional] | Lower-friction entry. |
| 5 | Stacked fields (email, password; + name/confirm on signup) | [required] | The credentials. |
| 6 | Inline options (remember-me, forgot-password) | [recommended] | Standard auth affordances. |
| 7 | Inline security-reassurance line | [recommended] | Calms data-entry anxiety. |
| 8 | Primary submit | [required] | The commit. |
| 9 | Alt-action link (switch login↔register) | [required] | Routes the wrong-mode user without a dead end. |

---

## 13. Legal (Terms / Privacy / Policy)

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Breadcrumb | [recommended] | Orientation on a deep page. |
| 2 | Title + last-updated date | [required] | Identifies the document and its version. |
| 3 | Table of contents / anchor nav | [recommended] | Navigates a long single-column document. |
| 4 | Long-form rich text at **constrained measure**, sectioned headings | [required] | Readable legal body; editorial-measure rule applies. |
| 5 | Contact / data-request block | [optional] | Compliance follow-up path (e.g. privacy requests). |

---

## Universal rules (apply across the library)

- **Chrome once, body per-template.** Never model a page as one flat list.
- **Breakpoint-invariant order.** Author at desktop; collapse columns + drawer-ize filters/sidebars for mobile. Never re-order per breakpoint.
- **Shared product-card molecule** across Home / PLP / cross-sell / Cart; bind card width to a block-size token so grids reflow by column count (never hardcode px).
- **Cross-sell rail closes almost every commerce page** (PLP, PDP, Cart).
- **Editorial pages** (About, Blog article, Legal) constrain body to a readable measure and close with **lateral navigation**, not a buy CTA.
- **Thread social proof** (edge rails, header ratings, inline avatars, badge rows) rather than pooling it all in one section.
- **Distinguish drawer vs page** variants: mini-cart drawer ≠ cart page; mega-menu ≠ plain nav list.


---

## 14. Personal Brand / Editorial Blog — Home

A personal brand's home page is not a storefront and not a plain blog index. Its job is to introduce the person, hand the reader to the journal, and open lateral paths to About and Contact. The register is editorial; there are no product rails.

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Full-bleed editorial hero: person or lifestyle photo + headline statement + 3 lateral CTAs (Journal / About / Contact-or-Work-with-me) | [required] | First impression and wayfinding; editorial hero is a stage-setter, not a sale. Three CTAs because the top-level IA has three arms. |
| 2 | Featured article or recent articles grid (2-3 cards, equal height, real images) | [required] | Shows the journal is live and gives an immediate read path. |
| 3 | About/intro split band: person photo + 2-sentence bio + CTA to About | [recommended] | Anchors the person behind the brand mid-scroll; positions the About page. |
| 4 | Value-props or "why this space" band | [optional] | Grounds the editorial voice in a concrete promise; skip if the hero headline already does it. |
| 5 | Testimonial pull-quotes (2-3, editorial format, no star ratings) | [optional] | Social proof in register; use reader pull-quotes, not commerce-style reviews. |
| 6 | Newsletter capture band | [recommended] | The primary conversion action on a personal brand site. |
| 7 | Footer | [required] | Author name, nav, social. |

Rules:
- The hero MUST have lateral CTAs to all major sections (Journal, About, Contact). A hero with one CTA leaves the visitor without a map.
- Include real photos of the person at minimum in: the hero (or just below it), the About-split band, and the article author band.
- No product rails, trust-strips, payment badges, or commerce patterns.
- The about-split band image shows the person — not a lifestyle stock photo without a face.

---

## 15. Personal Brand / Editorial Blog — About

| Order | Section | Tag | Why |
|---|---|---|---|
| 1 | Full-bleed hero: person photo + name/headline statement + signature identity element | [required] | Emotional entry; this is literally about the person. |
| 2 | Zig-zag alternating story bands (image swap sides each block) | [required] | Imagery co-equal with narrative; alternation prevents a wall of text. |
| 3 | Values or "how I work" summary | [recommended] | Concise beliefs that give a potential reader/client a quick read. |
| 4 | Lateral CTA to Journal | [recommended] | Editorial pages close with discovery, never a buy CTA. |

Rules:
- The hero image is the person. Not landscape, not flat color — the person.
- The zig-zag story bands must both show real photos (not the same photo twice).
- Text on a photo hero must be cream/white with a dark gradient scrim on the image; never dark ink on a mid-toned photo.

---

## Refinements from Source 05

## Home / Landing — refinement: convince/convert purpose-alternation (storefront register)

Refines the standard home skeleton by adding a *purpose* tag to every in-body band plus an ordering law layered on top of density oscillation. Does not change which sections exist — it governs their sequencing.

Tag each home band as **[discovery]** (sells: product rails, shoppable grids, featured/bestseller, category tiles) or **[trust/story]** (reassures: USP ticker, value-props split, reviews wall, brand/journal, press strip), then interleave them.

Ordered body stack (after global chrome; home has **no** breadcrumb):
1. Hero — light full-viewport stage, copy composed into the image's negative space, single CTA [required]
2. Credibility strip — thin trust band handed off immediately below the hero (logos / ratings / one-line proof) [recommended] — *[trust/story]*; separates impression from justification
3. Primary catalogue entry — category tiles or collection grid [required] — *[discovery]*; first path into the catalogue
4. Value-props / USP split [recommended] — *[trust/story]*; alternates off the discovery band above
5. Curated / featured / bestseller rail [recommended] — *[discovery]*
6. Reviews wall / social-proof band [recommended] — *[trust/story]*
7. Editorial / brand / journal band [optional] — *[trust/story]*; held to the narrow reading measure
8. Conversion band — newsletter / primary CTA [recommended]
9. Footer [required]

Rules specific to this refinement:
- **Never place two same-purpose bands back-to-back** even when their visual weights already oscillate — two product rails in a row reads as a catalog dump, two story bands in a row stalls the sell. Alternate discovery with trust/story by band intent, independently of the dense/airy weight rhythm.
- Thread proof at multiple depths (ratings inside cards, a dedicated reviews band, standalone pull-quotes) rather than clustering all social proof into one testimonials block.
- The sequence is a decision narrative (desire → justify → handle objections → next step) and is **breakpoint-invariant**: reflow only by column-collapse (N → N/2 → 1), never by re-ordering bands.

## Editorial / long-form body (about · article · legal) — refinement: reading register + lateral-nav closer

Refines the standard content/article and about/legal skeletons by binding them to a single interior register for the whole body and forbidding the commerce closer. The section list is conventional; the refinement is the register and the ending.

Ordered body stack (deep page → prepend **breadcrumb [required]** as the first in-body element):
1. Breadcrumb [required] — signals page depth
2. Hero / title block — narrow measure, no full-bleed text [required]
3. Long-form body held to a **constrained reading measure** for its entire length [required] — centered column, capped line-length, images interleaved **between** paragraphs rather than beside them
4. Proof interludes — pull-quote / inline stat at the same narrow measure [optional]
5. Lateral-navigation closer — related / next / more-in-this-topic [recommended]
6. Footer [required]

Rules specific to this refinement:
- The body stays in the **reading register** throughout — no switch to grid/merchandising logic mid-page; the only grid-break is a *narrowing*, never a widening.
- **Close on lateral navigation, never a buy-CTA and never a dead-end.** The cross-sell / buy-CTA closer is reserved for commerce pages (PDP/collection); an editorial page that ends on "add to cart" or on nothing is the register error.
- Section headers and prose are both capped to the narrow measure even though the band is full-width.


---

## Additions from Source 06

# Page-Skeleton Additions

Only page types this source **adds** or **materially refines** vs the standard catalogue. Standard pages (home, collection, PDP-basic, cart, checkout, about, contact, blog index/article, account, pricing, auth, legal) are omitted unless the refinement is load-bearing. All skeletons are breakpoint-invariant in order (author desktop → reflow by column-collapse + drawer-izing); every section opens with the standardized **Section-Header organism** {eyebrow [opt] / heading [req] / support line [opt] / trailing action [opt]}.

---

## PDP — two-phase: Decision Band → Evidence Narrative (REFINES standard PDP)
Replaces the bare "gallery + buybox + tabs" model with a conversion-ordered long page.

**Phase 1 — Decision band (2-col):**
1. Sticky gallery column `[required]` — pinned media while buybox stays in view.
2. Buybox column `[required]` — price / variants / primary CTA, in this order.
3. Conversion-ribbon inside buybox `[recommended]` — 3–4 icon+title trust props; repeats the hero trust band at decision point.
4. Accordion (details/shipping/ingredients) `[recommended]` — defers depth without pushing CTA below fold.

**Phase 2 — Evidence narrative (full-width stack, each section independently optional + reorderable):**
5. Science / mechanism explainer `[recommended]` — justifies the claim before asking for commitment.
6. Before/after or proof demonstration `[recommended]` — shows the result, not just describes it.
7. How-to-use / onboarding `[recommended]` — handles the "will I use it right" objection.
8. Social proof — reviews + aggregate rating `[recommended]` — threaded proof concentrated at decision depth.
9. FAQ `[optional]` — final objection handling.
10. Cross-sell / related `[recommended]` — next step once convinced.

*Why:* the evidence narrative is the conversion engine; model it as an ordered desire→justify→objection→next-step arc, not collapsed into tabs. Buybox is the only required organism.

---

## Order Confirmation — post-purchase receipt (ADDS; split out from checkout)
A separate template, **not** "checkout minus the form."

1. Success headline `[required]` — confirms the transaction completed.
2. Customer / shipping info recap (left col) `[required]` — reassurance the details are correct.
3. Primary "continue/home" + secondary "download invoice" actions `[required]` — clear next step + record-keeping.
4. Support block `[recommended]` — pre-empts "something's wrong" anxiety.
5. Order summary + money math (right col) `[required]` — item recap + totals.
6. Loyalty / points-earned callout `[recommended]` — distinct post-purchase reward slot that drives return visits.

*Why:* confirmation has its own required slots (headline, recap, loyalty callout, support) that a generic catalogue wrongly folds into checkout.

---

## Cart — transaction skeleton with incentive mechanics (REFINES standard cart)
2-col: left editable line-items | right sticky summary.

1. Editable line-items (left) `[required]`.
2. Free-shipping / gift **stepper** — progress-to-threshold bar `[recommended]` — turns "add more" into a visible goal (e.g. tier-1 free ship, tier-2 gift).
3. Bought-together cross-sell carousel (above summary) `[optional]`.
4. Sticky order-summary + money math (right) `[required]`.
5. Discount-code block with suggested-coupon tiles `[recommended]` — surfaces available offers instead of hiding behind a blank field.
6. Primary checkout CTA `[required]`.

*Why:* the stepper and coupon tiles are concrete reusable incentive mechanics worth cataloguing as named cart sub-sections.

---

## Guided Quiz Funnel — page-type family (ADDS; `[optional]`, but full skeleton when present)

**A. Start / intro:**
1. Value-prop headline + what-you'll-get `[required]`.
2. Start CTA + time/length reassurance `[recommended]`.

**B. Question step (repeated frame; two layouts):**
1. Progress indicator `[recommended]` — orients the user in the funnel.
2. Single question `[required]`.
3. Answer field — **option-card** layout OR **tag/chip multi-select** layout `[required]` — enumerate both as sibling variants.
4. Advance / back controls `[required]`.

**C. Recommendations / personalized results (its own reusable personalized-merch skeleton):**
1. Diagnostic headline `[required]` — "here's what we found" reflects the inputs back.
2. Recommended-product set `[required]` — the personalized payload.
3. Comparison / "why these" `[recommended]` — justifies the recommendation.
4. Social proof — press logos + customer count `[recommended]`.
5. UGC grid `[optional]`.

*Why:* quiz→result is not in a standard storefront catalogue; the result page is a distinct personalized-merchandising template.

---

## Self-Service Return / RMA — 3 terminal-state frames (ADDS; `[optional]`)
Model each outcome as its **own named frame**, never one page with runtime conditionals.

- **Enabled (eligible / input):** header `[req]` → eligibility/intro `[req]` → return form (order ref, items, reason) `[req]` → submit `[req]`.
- **Disabled (ineligible / window closed):** header `[req]` → explanation of why ineligible `[req]` → alternative action / support link `[recommended]`.
- **Success (submitted):** header `[req]` → confirmation headline `[req]` → next-steps / tracking `[recommended]` → return-home action `[req]`.

*Why:* extends the "draw every terminal state as a canonical frame" discipline to transactional non-commerce pages.

---

## Slide-Out / Overlay — first-class template family (ADDS)
Cart drawer, search, product-finder/attribute-filter — each a full artifact, not a loose page state. Shared skeleton:

1. Header — title + close `[required]`.
2. Scrollable body `[required]` — the overlay's content stack (line-items, results, or facet groups).
3. Pinned footer action `[required]` — the one commit CTA stays reachable without scrolling.

*Why:* overlays deserve the same {header / body / pinned-action} anatomy discipline as full pages; author at all 3 breakpoints.

---

## Shared "content tail" (REFINES Blog index + Article)
A reusable tail spanning both content page types:
- Email-capture / newsletter band `[recommended]`.
- Related-items grid `[recommended]`.

Blog index adds a **featured/lead post** `[recommended]` above the card grid; Article adds **breadcrumb → title/hero → body → tag chips → author box** before the shared tail.

*Why:* the capture band + related grid recur across content pages as one portable slot pattern.

---

## Cross-cutting composition rules (apply to ALL skeletons above)

- **Conversion-ribbon** (3–4 equal-width icon+title+subtitle trust props, one line each) is a canonical `[recommended]` thin band directly under the hero and inside the PDP buybox.
- **Section-Header organism** opens every content section; toggle unused slots via hidden flags — never delete-and-redraw, never leave a section headerless.
- **Density oscillation on two axes** in expressive/high-chroma registers: alternate tall/short **and** light-surface/saturated-surface bands. Never place two full-bleed saturated bands back-to-back; intersperse a light/neutral band for recovery.
- **Grid-break = narrowing** to a centered readable measure for editorial/quote/capture moments — never a full-bleed widening of text. In a high-contrast register the break may be doubly marked by inverting the surface behind the narrowed column; the narrowing (not the color) is still the load-bearing act.
- **Threaded proof** distributes ratings/badges/counts/quotes across depths (in cards, a proof band, standalone strips) AND, in a high-chroma register, binds them to the single reserved accent so "saturated" reliably reads as "credible/commit." Don't spend that accent on decoration.
- **One token ramp** drives every gap/padding/width even when the palette is loud; variety comes from surface color + content, not ad-hoc pixels.
- **Breakpoint-invariant order:** author desktop as canonical; derive mobile by column-collapse + drawer-izing only — never re-order sections per breakpoint.


---

## The page-shell container contract (from Source 07)

Every page skeleton sits inside a breakpoint-scoped container:
- **Desktop:** a wide, capped content column, centered, with symmetric margin.
- **Tablet:** a mid-width column; smaller margin.
- **Mobile:** a narrow column that goes **edge-to-edge** (margin → 0); padding does the insetting.

Container width = `device-width − 2 × margin`. Section rhythm, container inset, and device margin
are three independent responsive knobs. Author section *order* once (breakpoint-invariant); reflow
by collapsing columns and drawer-izing filters, never by resequencing.


---

## Additions from Source 08

## Compliance / Age / Consent Gate (interstitial)
*Chrome-less full-screen frame that gates entry to the store; first frame in the journey, no global nav. Material addition — not covered by auth or any content page.*

1. Brand mark / minimal lockup — **[required]** — orient the user; this frame has no header, so identity must live inline.
2. Gate statement (one-line requirement, e.g. age/region/consent) — **[required]** — states the single condition to proceed.
3. Binary choice control (confirm / deny) — **[required]** — the gate's whole purpose is one decision; keep it to two paths.
4. Deny-path fallback (redirect or soft-block message) — **[recommended]** — the "no" branch needs a defined destination, not a dead end.
5. Fine-print / legal line — **[optional]** — regulatory context where the niche demands it.

> No header/footer chrome. Breakpoint-invariant (centers on both). Regulated niches (age, alcohol, region-lock, cookie/consent) require this; omit otherwise.

## Order Confirmation / Success (standalone)
*Terminal frame of the checkout flow, distinct from checkout steps. Added because checkout here is a step-family, not one page.*

1. Success headline + confirmation glyph — **[required]** — resolves the transaction emotionally and functionally.
2. Order meta block (order #, email, totals) — **[required]** — the receipt record the user came to see.
3. Delivery/fulfilment summary — **[recommended]** — restates where/when, closing the loop on the flow's inputs.
4. Primary next-step CTA (track order / continue shopping) — **[required]** — gives the resolved user one clear onward path.
5. Cross-sell or account-prompt band — **[optional]** — low-pressure continuation once the goal is met.

## Empty / Zero-State variant (per data-page)
*A first-class state skeleton, not an edge case. Budget one for cart, search/PLP, and any data-backed page.*

1. Persistent header/footer — **[required]** — the shell stays so the empty state reads as "within the store," not an error.
2. Illustration / empty glyph — **[required]** — fills the vacated data region and sets a non-alarming tone.
3. Zero-state message (what's missing + why it's fine) — **[required]** — reframes absence as recoverable.
4. Single recovery CTA (browse / reset filters) — **[required]** — exactly one path back to a populated state; avoid choice overload here.
5. Suggestions / popular carousel — **[optional]** — seeds re-engagement without cluttering the recovery intent.

## Checkout = Stepped-Flow Family (refines "Checkout")
*Treat as an ordered sibling sequence sharing one persistent summary rail, not a single page. Materially refines the standard one-page checkout skeleton.*

Flow order: customer/auth → delivery address → shipping method → payment → review.
Per step:
1. Step indicator / progress — **[recommended]** — situates the user in a multi-frame sequence.
2. Step body (the fields/choices for this step only) — **[required]** — each frame owns one decision cluster.
3. Shared order-summary slot — **[required]** — desktop = pinned right rail; mobile = top accordion. Identical content across every step.
4. Back / advance controls — **[required]** — explicit movement between sibling frames.

> The portable unit is `step-sequence + shared-summary slot`, terminating in the Order-Confirmation skeleton above.

## Register-Specific Overlay Track (breakpoint-tagged)
*A separate track from full-page skeletons. Each overlay tags its breakpoint(s) and the inline region it replaces. Material addition — a page-only catalogue cannot express "promote inline region to overlay below breakpoint."*

- **Filter drawer** (mobile) ↔ inline desktop filter rail — **[required where PLP has filters]** — full-height slide-up; same filter controls as the desktop rail, reflowed vertically.
- **Add-to-cart confirmation sheet** (mobile) ↔ inline desktop cart feedback — **[recommended]** — bottom-sheet confirming the add + mini-summary + continue/checkout; a net-new mobile organism with no desktop twin.
- **Auth modal** (login / signup) ↔ inline desktop auth page/region — **[recommended]** — overlay on mobile, inline on desktop.
- **Persistent floating launcher** (chat/assistant/CTA, pinned corner) — **[optional]** — fixed overlay layer present on *every* frame, both breakpoints; authored once, threaded globally.

> Overlay-track rule: tag each with breakpoint + the inline equivalent it replaces. A breakpoint may OWN net-new organisms (bottom-sheets, slide-up filters) that the other solves inline — responsive method is not purely column reflow.

## PLP / Collection — parametrized-by-taxonomy (refines "Collection")
*Collapse N per-category frames into ONE skeleton with a taxonomy slot; do not inflate the catalogue with structural duplicates.*

1. Category/taxonomy selector strip (active-taxonomy = the variable slot) — **[required]** — the single parameter that distinguishes otherwise-identical siblings.
2. Filter region (desktop inline rail / mobile drawer) — **[required]** — same function, two renderings by breakpoint.
3. Product grid — **[required]** — the data region re-fed per taxonomy.
4. Sort control — **[recommended]** — orthogonal to taxonomy; shared across variants.
5. Load-more / pagination — **[required]** — bounds the grid.

> Refinement: one parametrized template, not one page type per category. Restricted-subcategory variants reuse this skeleton behind the gate.

## Blog as INDEX↔ARTICLE pair (refines "Blog index + article")
*Catalogue as a linked pair; the article's sidebar is a distinct reusable organism. Refines a single "Blog" entry.*

**Index:** uniform card grid **[required]** → pagination **[required]**.

**Article/Detail:**
1. Article hero (title / meta / cover) — **[required]**.
2. Narrow reading column — **[required]** — constrained measure for long-form.
3. Persistent content sidebar (author card + taxonomy list + popular list + CTA) — **[recommended]** — the reusable organism that the index lacks.
4. Social-share rail — **[recommended]**.
5. Mid-article promo band — **[optional]** — inline interstitial absent from the index.
6. Related-articles row — **[recommended]**.

## Long-Form Storefront Home — band-rhythm skeleton (refines "home/landing")
*Refines the generic home into a density-oscillating band sequence with named compositional seams. Each band keeps identical content/order across breakpoints; only the layout axis flips.*

1. Sticky nav — **[required]**.
2. Hero statement (oversized headline + one-line body + single CTA, optional playful illustration cluster) — **[required]** — *airy* band opening the rhythm.
3. Uniform N-up product grid — **[required]** — *dense* band.
4. Interstitial RESET band (short full-bleed saturated strip; often carries threaded proof/trust badges) — **[recommended]** — *compressed* palette-cleanser whose structural role is the reset, independent of content.
5. GRID-BREAK feature split — narrows the multi-column grid to ONE focal object — **[recommended]** — *airy*; emphasis signalled by narrowing column count, not by another same-weight grid. May use a DIAGONAL SEAM (slanted color-block edge the focal cluster straddles) or a STACKED-DECK FAN (peer cards overlapped + slightly rotated as one object).
6. Editorial 3-up cards — **[optional]** — *medium* band.
7. Secondary CTA / app / cross-channel band — **[optional]** — *airy*.
8. Dense footer (with threaded ratings/reviews cues) — **[required]**.

> Composition rules baked in: DENSITY OSCILLATION (alternate airy↔dense↔compressed band-to-band); TILTED DIVIDER PLANES (subtly skewed sheet seams between sections instead of straight rules) for a "playful" register; THREADED PROOF (mid-page band + in-card ratings + footer reviews, never concentrated once). Anti-slop: never a uniform stack of equal-weight full-width cards.
