# Fonts — the study method + a starter pairing library

Fonts are the fastest way a brand book reads as premium or as generic. A real run proved it: a
reflexive pairing (and generic fallbacks) read as a SaaS product; a deliberate study read as a
considered editorial brand. **Never reach for a default. Study, pick, embed, verify.**

## The method (run every project)

1. **Name the register** (from the brief / `method/00-decide.md`): editorial, clinical, playful,
   luxury, technical, warm, etc. The register decides the pairing far more than personal taste.
2. **Choose the pairing strategy by register** (not reflexively):
   - **Editorial / long-form / warm-premium → serif + serif** (display serif + *reading* serif
     body). A UI sans (Inter/Roboto/Open-Sans class) under long essays reads "clean tech / SaaS,"
     which kills editorial warmth. The body serif is the single biggest lever here.
   - **Modern product / app / clinical → sans + sans** (a humanist or neo-grotesque), or a serif
     display over a sans body for a touch of authority.
   - **Luxury / fashion → high-contrast Didone display + a calm text serif or refined sans body.**
   - **Playful → a characterful display + a friendly, legible sans body.**
3. **Pick real, self-hostable, free faces** — Fontshare (ITF Free Font License) and Google Fonts
   (OFL) are the two go-to sources; both are free for commercial use and self-hostable. Avoid
   hotlinking a CDN.
4. **Reach past the overused defaults** unless you can make a strong specific case: Inter, Roboto,
   Open Sans, Lato, Montserrat, Poppins, Playfair Display. They read as "every website."
5. **Echo the logo.** If the mark is a serif monogram, the display serif should rhyme with it; if a
   script tagline exists, a sparing script accent can echo it.
6. **EMBED and VERIFY.** Embed the faces (`@font-face` base64 or local woff2/ttf) so they render in
   the PDF, then open it and confirm the specimen is the real face — not a fallback. See
   `render.md` for the embedding mechanics.
7. **Record the production setup** in `brand-tokens.json`: exact family names, weights, sources, and
   the `next/font` / `@font-face` wiring, so the client's live site uses the identical faces.

## Role map (how the pairing maps to the book + site)

Display/H1 → display face (semibold) · H2 → display (medium) · Subtitle/deck → display *italic* ·
Subheading → body face semibold, tracked caps, accent color · Body → body face regular (serif for
editorial) · Pull-quote → display italic · Caption/meta → body small · Button/nav → display or body
medium · Tagline/signature → script accent (if any), used sparingly.

## Starter pairing library (free, self-hostable, proven)

Draw from these or override with a studied choice. Verify current availability before use.

| Register | Display | Body | Accent (optional) | Why |
|---|---|---|---|---|
| **Editorial / warm-premium** | **Gambetta** (Fontshare) | **Newsreader** (Google) | **Pinyon Script** (Google) | Serif+serif, shared old-style DNA → one voice; drawn italics; built-for-reading body. Calm luxury. |
| **Literary / classic editorial** | **Fraunces** (Google) | **Source Serif 4** (Google) | — | Fraunces has character as display; Source Serif is a calm, warm reading body. Serif+serif. |
| **Luxury / fashion** | **Boska** (Fontshare, high-contrast Didone) | **Source Serif 4** or **Newsreader** | **Great Vibes** (Google) | Dramatic display + calm body; use display with discipline so it stays luxe not loud. |
| **Modern product / SaaS** | **Clash Display** or **Satoshi** (Fontshare) | **Satoshi** / **Supreme** (Fontshare) | — | Clean humanist/neo-grotesque; crisp, contemporary, legible at UI sizes. |
| **Clinical / technical / B2B** | **General Sans** (Fontshare) | **General Sans** (Fontshare) | a **mono** (e.g. **JetBrains Mono**) for status/metadata | Neutral, trustworthy; mono third face signals "system/factual metadata." Tracking ≈ 0. |
| **Playful / lifestyle commerce** | **Clash Display** or **Zodiak** (Fontshare) | **Satoshi** (Fontshare) | a script if the brand is romantic | Characterful display + friendly legible body; keep chroma/energy in color, discipline in type. |

Notes:
- **Fontshare** fonts are downloaded as a zip of static + variable woff2 (ITF Free Font License).
- **Google Fonts** variable TTFs are in the `google/fonts` GitHub repo (OFL); the CSS2 API also
  serves subset woff2.
- These are starting points — a real study may land on a better face for the specific brand. The
  rule is *study and justify*, not *obey the table*.
