# Brand-book quality checklist (run before presenting)

Render the PDF, open it, and check every box. Hard-won from real runs: a first pass that skipped
this read as weak/templated even though it "looked fine" unrendered. Do not present a brand book
until every item passes.

## 1. The logo (the #1 failure mode)
- [ ] **The REAL supplied logo is used** — the actual file, placed as an image, on every page the
      logo appears (cover, logo, exclusion zone, color versions, icon, composition, placement,
      misuse, co-branding).
- [ ] **No hand-reconstruction anywhere.** The mark was never rebuilt in HTML/CSS/SVG. Letterforms,
      script, ring, proportions are the original's — unchanged.
- [ ] **Contrast handled without altering the mark.** On any ground where the logo doesn't read, the
      ground was changed or the logo framed (light tile) — never recolored. Any inverted/mono
      version is explicitly labelled a "color version", generated from the real asset.
- [ ] Logo is **embedded** (data URI / local) so the PDF is self-contained.

## 2. Fonts (the #2 failure mode)
- [ ] **Real faces render** — open the PDF and confirm the specimens are the *chosen* typefaces,
      not Georgia / Times / a system sans fallback.
- [ ] Fonts are **embedded** (`@font-face` base64 or local woff2/ttf), not hotlinked.
- [ ] The pairing came from a **real font study** for the register (see `fonts.md`) — not a
      reflexive default. For editorial/long-form, the **body is a serif**, not a UI sans.
- [ ] The faces are free/self-hostable and the exact `next/font` / `@font-face` setup is recorded in
      `brand-tokens.json` so they match the client's live site.

## 3. Layout & alignment
- [ ] **Chrome is consistent**: tracked uppercase eyebrow (accent) + display-face title, tight
      top-left stack, on the same left-margin line on every page.
- [ ] **Margins are generous and equal**; panels inset consistently; nothing drifts off the grid.
- [ ] **Scale is confident**: typeface specimens are large; pages breathe. No cramped/timid pages.
- [ ] **No clipped content** — every element fits inside its 16:9 page (check in a browser's
      continuous scroll too, where `overflow:hidden` reveals clipping that print hides).
- [ ] Source URLs present (accent-underlined, top-right) on the typeface pages.

## 4. Brand fidelity
- [ ] Colors are the **real brand values** (from the logo / client), extended coherently, with
      real HEX/RGB shown; contrast verified (note any accent that fails AA at small sizes and scope
      it to large/graphic use).
- [ ] The **one bold move** (atelier standing policy) is present as a dedicated page and is
      nameable — a real signature, not decoration.
- [ ] Register match: the book *feels* like this specific brand's register (premium/editorial/
      playful/clinical…), not a generic template with the colors swapped in.

## 5. Photography (no raw placeholder blocks, ever)
- [ ] **Real photos are present** on the placement / on-imagery pages — never a flat color block.
      Sourced per `photography.md` (Unsplash default), mood + color matched to the brand.
- [ ] **No third-party trademarks/logos** visible in any photo (a branded product implies
      endorsement and violates the license) — re-query if the top result has one.
- [ ] Photos are **embedded** (base64) so the PDF is self-contained; a **scrim** sits behind any
      logo/text over a photo for legibility; a small **photographer credit** is shown.
- [ ] Credits + source recorded (e.g. `assets/photos/credits.json`) for traceable attribution.

## 6. Completeness
- [ ] All required pages present (see `pages.md`); recommended pages included where the brief needs.
- [ ] Any remaining placeholder (lorem copy, etc.) is clearly flagged for the client — not passed
      off as final.
- [ ] Page count and order match the intended structure.

## 7. Final
- [ ] **Rendered and reviewed page-by-page** — not judged unrendered. If you can't point to each
      fix above in the actual PDF, it isn't done.
- [ ] Honest limits stated to the client (logo = direction if generated; photos are licensed stock
      unless the client supplies their own; "strong first draft, not zero-edit final").
