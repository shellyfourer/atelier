# Source 05 — method notes (app-leaning store / shadcn admin register)

> Anonymized. An app-leaning commerce/admin design on a thin-semantic (shadcn) register.
> Teacher, not template. Its headline contribution: the three color 'methods' are composable
> TIERS, not a forced choice (app = thin-semantic stacked on a ramp primitive library). Also
> alpha-ramp tokens, translucent borders, sub-namespaced roles, and a greybox/wireframe method.

## Source Method — App/Dashboard Register (shadcn-based admin/commerce, light+dark)

**Register:** A rich application / dashboard / admin-commerce product (a settings-and-data UI, not a marketing storefront). Light and dark modes. This is the first source in the corpus whose primary register is the **app shell**, and it resolves several ambiguities the storefront/library sources left open.

### What this source proves (headline)
The three color "methods" atelier documents (tonal-ramp / category-color / thin-semantic) are **not a forced single choice** — in an app register two of them **STACK as composable tiers**. A full primitive ramp library sits at the bottom; a thin closed semantic role set selects from it; UI binds only the semantic tier. The register decides how many tiers you expose.

### Color (observed)
- Closed shadcn role set, verbatim: background/foreground, card(-foreground), popover(-foreground), primary(-foreground), secondary(-foreground), muted(-foreground), accent(-foreground), destructive, border, input, ring. Confirms thin-semantic method C.
- Light and dark are two **value columns over one role vocabulary** — names never change, values swap.
- Every semantic role resolves to a **primitive step**; UI never binds a raw value or a ramp step directly.
- Primitive ramps are present underneath (uniform 11-step 50→950 across hue families) but are **library-tier, not UI-facing**.
- Spacing (4-base), radius, and type tokens colocate on the same foundation.
- **New structural moves** this source introduces: (1) layered tiers (ramp under semantic); (2) a **prefix namespace split** so the token name encodes its tier (library-prefixed primitive vs bare-role semantic); (3) **sub-namespaced role families** inside the thin layer — a fixed `chart-1..N` set and a full mirrored **sidebar/app-shell sub-theme** (its own fg/primary/accent/border/ring) that rethemes independently; (4) an **extended status quartet** (info/success/warning/destructive) promoted into the role set rather than lone destructive; (5) an **alpha-ramp family** (one base stepped through fixed opacity levels) for scrims/hovers/disabled; (6) **translucent borders** — border/divider = foreground-at-low-alpha so one token survives any surface shade in either mode; (7) **adopt-don't-author** the primitive tier — in app register the ramps can be an off-the-shelf utility palette taken wholesale, relocating the design craft entirely to semantic selection + mode mapping.

### Type (observed)
- Composite tokens confirmed (family + weight + size + line-height + tracking under one name), breakpoint-prefixed.
- Multi-typeface strategy confirmed, with a **new third role**: a **monospace face reserved for a micro/status register** (trust bars, stock/status pills, timestamps, counters) — the face itself signals "system/technical/factual metadata."
- **Semantic ordinal naming** (H1/H2, Title 1/2, Body 1/2, Caption 1/2, Button) catalogued as a valid alternative axis-labelling to role×t-shirt-size.
- Line-height law **refined**: pin to **1.0 for single-line vertically-centered roles** (buttons, nav, chips, run-in labels) vs ~1.5 for flowing body — the deciding variable is centering-in-a-control vs multi-line-flow, not size alone.
- Letter-spacing law **disconfirmed as universal**: tracking is **register-dependent**; a clean clinical/B2B/technical brand holds tracking at 0 across the whole scale including large display. Negative-on-display is an editorial/luxury convention, not a default.
- **Two independent centralization substrates**: a file can centralize every style as a named text style while binding NONE of its type to variables (variables reserved for color/number). "Is it a named style" and "is it variable-bound" are separate audit questions.

### Component architecture (observed)
- Confirms the full instanced-ladder method (named base atoms, altitude-in-name, family-of-siblings, states-as-axes, density hoisted to a parallel library, path taxonomy, one-line usage, responsive = one set with Breakpoint variant + priority reflow ladder, semantic-tokens-only).
- **New:** function-first is the **primary organizing spine** (promote from naming footnote); the family-split and small-matrix rules are **causally linked** (you split siblings precisely to keep each one's axes orthogonal — split the moment two axes stop being orthogonal); and a **greybox/wireframe kit** is a legitimate fifth construction method (architecture shipped decoupled from skin, re-skinned per brand downstream).

### Page composition (observed)
- Confirms band chassis, density oscillation, grid-break-as-narrowing, nested width systems, flip-the-split, one token ramp, threaded proof, hero-as-stage, decision-ordered sequence, header grammar.
- **New:** convince/convert **purpose alternation** as a distinct homepage law (never two same-PURPOSE bands adjacent — discovery vs trust/story — orthogonal to weight oscillation); **section order is breakpoint-invariant** (reflow only by column-collapse + drawer-izing filters); **chrome/body split** as the composition substrate (global chrome authored once + per-template body stack; breadcrumb = first in-body element on deep pages only); grid-narrowing **selects a reading register** that dictates the band's closer (commerce→cross-sell, editorial→lateral nav); hero copy lives in the image's **negative space**, not a scrimmed overlay.

### One BLOCKED layer (honest)
The page-anatomy/skeleton layer was **BLOCKED** — the supplied fileKey was the literal string "undefined" and no key was recoverable. That layer produced **zero observations and zero new findings** (correctly), only a re-validation checklist. No skeleton claims from this source may be trusted as evidence. The methodological takeaway (an anti-slop rule, below) is: a missing/placeholder fileKey must halt-and-report, never be back-filled with plausible lore.

### Teacher, not template
Nothing here is client-specific. Treat this source as the canonical answer to "how do I do color/type/components/pages for an APP register" and to "are the three color methods a choice or a stack" (answer: in an app, a stack).
