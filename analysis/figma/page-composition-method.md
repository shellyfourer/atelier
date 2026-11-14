# Page composition method — section sequencing, rhythm, grid discipline, and intentional grid-breaks (homepage + PDP of a mature e-commerce design system)

_Confidence: high_

**Portable vs discard:** Portable: the band-chassis + token-ramp + density-oscillation + narrowing-as-grid-break + decision-ordered section sequence are all reusable on any project. Discard as source-specific: the actual palette (a restrained neutral + single accent), the body typeface, the exact pixel widths, the source copy, and the exact section list — re-derive widths and sequence from the new project's own grid and funnel.

## Method principles

- **Build the page from a fixed vocabulary of full-width horizontal bands ('Sections'), each a self-contained row that owns a uniform outer margin and a uniform top inner-padding, and let content height — not a fixed template slot — set each band's height. Every band in the studied pages shares one outer margin and one vertical-padding token; they differ only in what lives inside.**
  - *Why:* A shared band chassis makes an arbitrarily long page read as one coherent system rather than stacked templates, while variable height lets each section breathe to its content. This is the single biggest driver of 'intentional, not templated.'

- **Oscillate density: never place two heavy, tall sections back-to-back. Alternate a tall high-information band (product grid, reviews, buybox) with a short low-information band (a thin trust strip, a one-line pull-quote, a category-link row). Tall, information-dense sections are consistently separated by short, quiet ones — the alternating rhythm is the lesson, not any specific height.**
  - *Why:* Rhythm comes from contrast in vertical weight. Uniform-height sections feel like a spreadsheet; a measured loud/quiet/loud cadence gives the scroll a pulse and gives the eye recovery points, which is what makes a long page feel composed.

- **Treat the hero as a stage, not a container — give it the full viewport height but keep it visually light (a single image/carousel with minimal overlaid text), then immediately hand proof to a thin credibility strip directly beneath it. The studied hero is a 100VH band followed within one scroll by a 4-up icon trust row.**
  - *Why:* A hero overloaded with copy and CTAs reads as a template. Separating 'impression' (hero) from 'justification' (the proof strip right below) lets each do one job well and establishes credibility before the catalog begins.

- **Run two nested width systems: a wide content container for grids and media, and a deliberately narrower measure for reading-dominant content. Constrain section headers and long prose to a ~fixed max line-length even inside a full-width band, and shrink the whole container to a centered narrow width for quote/editorial/capture moments.**
  - *Why:* The intentional grid-break is almost always a narrowing, not a widening. Pulling text into a centered narrow column amid full-width neighbors signals 'slow down and read,' creates visual punctuation, and keeps line-length readable without needing a different layout engine.

- **Use the 50/50 image+content split as a repeatable storytelling unit, and FLIP its sides on each consecutive use (image-left/text-right, then text-left/image-right). The pages chain alternating split sections rather than repeating the same orientation.**
  - *Why:* Mirroring consecutive splits breaks the templated 'every row looks identical' feeling with near-zero extra components, and the zig-zag guides the eye diagonally down the page instead of in a dead-straight column.

- **Drive all spacing, type, and layout widths from one small token ramp (a single geometric-ish spacing scale like 4/8/12/16/24/32, one display+body family, a headline scale whose negative letter-spacing tightens as size grows) and reuse it everywhere. Section padding, grid gutters, and block spacing in the data all resolve to the same handful of values.**
  - *Why:* A constrained token set is what makes dozens of distinct sections feel authored by one hand. Shared rails mean variety lives in composition and content, not in ad-hoc pixel values — which reads as discipline, the opposite of slop.

- **Make proof and credibility recurring structural elements, not a one-off section. Ratings, review counts, badges, before/after pairs, and pull-quotes recur at multiple depths (inside cards, in a dedicated reviews band, as standalone quote bands) and are spaced through the page rather than clustered.**
  - *Why:* Threading evidence throughout the scroll sustains trust at every decision point. Distributing it (vs one testimonial block) is a composition decision that makes the page feel purpose-built for conversion rather than filled with generic sections.

- **Compose long transactional pages (PDP) as hero/decision band → sticky commitment bar → alternating explainer splits → full-bleed moment → social proof → FAQ → cross-sell, i.e. a narrative arc from 'what/why buy' to 'answer objections' to 'keep shopping,' with a persistent CTA pinned across the arc.**
  - *Why:* Section order is an argument, not a stack. Sequencing by the user's decision journey (desire → justification → objection-handling → next step) and keeping the buy action always reachable is what separates a designed funnel from a pile of modules.

- **Keep section-internal structure consistent: a reusable Section-Header unit (optional badge + heading + supporting line, held to the narrow measure and often centered) opens most bands, so the reader instantly parses 'new topic starts here.'**
  - *Why:* A recurring header grammar gives the page predictable entry points and scannability. Consistency at the section-opening level is what lets the content inside each band vary freely without the page feeling chaotic.


## Anti-slop rules learned here

- Do not stack two tall, dense sections consecutively — insert a short calm band (thin strip, one-line quote, link row) between heavy ones to create vertical rhythm.

- Do not give every section the same height or the same content weight; uniform-height bands are the signature of a templated page.

- Do not repeat the same 50/50 split orientation twice in a row — flip image/text sides on each consecutive split.

- Do not let text run the full container width in reading-heavy sections; cap prose and section headers to a fixed readable measure even inside full-width bands.

- Do not break the grid by widening/going full-bleed for text; the intentional break is a NARROWING to a centered column for editorial/quote/capture moments.

- Do not overload the hero with copy, multiple CTAs, and feature lists — keep it a light full-viewport stage and move proof/justification to the band immediately below.

- Do not invent ad-hoc spacing or widths per section; resolve every gap, padding, and width to the shared token ramp.

- Do not cluster all social proof into one testimonials block — thread ratings, badges, and quotes through the whole scroll.

- Do not order sections arbitrarily; sequence them as a decision narrative (desire → justify → handle objections → next step) and keep the primary CTA reachable throughout.

- Do not mix multiple type families or let headline letter-spacing stay loose at large sizes — one family, and tighten tracking as size grows.

- Do not drop a section in without a recognizable header grammar (badge/heading/support) so each new topic has a clear, consistent entry point.
