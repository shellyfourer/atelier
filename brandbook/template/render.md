# Rendering the brand book HTML → PDF

The brand book is authored as a single HTML file whose pages are `<section class="page">` blocks,
styled by one token-driven stylesheet, then printed to a 16:9 PDF.

## The chassis

- `template.html` — the page skeleton: one `<section class="page">` per brand-book page, with the
  shared chrome (eyebrow + title) and content slots. **Copy it per project**; don't rebuild it.
- All brand values are **CSS custom properties** at the top (`:root`) — set them from the agreed
  `brand-tokens.json` and the whole book re-skins. The book is itself on-brand.
- `@page { size: 1280px 720px; margin: 0 }` + `.page { width:1280px; height:720px; break-after:page }`
  gives exactly one 16:9 page per section. (Any 16:9 box works; 1280×720 is convenient.)

## Tokens to set per project (`:root`)

```
--brand-accent      /* the bright/accent hue (eyebrows, highlights)      */
--brand-primary     /* the primary dark/brand ground                      */
--brand-tint        /* the pale tint (section grounds)                     */
--brand-ink         /* default text on light                              */
--brand-on-dark     /* text/logo color on the dark/brand ground           */
--font-display      /* primary face (headings, specimens)                 */
--font-body         /* body face                                          */
--font-secondary    /* secondary/serif face if used                       */
```

Plus the content: logo asset path(s), the color-swatch list (name + HEX/RGB/print), the type
role table, and the signature-move asset.

## Fonts & assets — the embedding mechanics (this is what makes them actually render)

A render that falls back to Georgia/system fonts, or that reconstructs the logo, is a FAIL (see
`QUALITY.md`). Do it properly:

### Real fonts, embedded
1. **Get the real font files** (woff2/ttf): Fontshare → download zip (`api.fontshare.com/v2/fonts/
   download/<family>`); Google Fonts → variable TTF from the `google/fonts` GitHub repo, or subset
   woff2 via the CSS2 API. Pick only the weights/styles you use.
2. **Base64-embed them in `@font-face`** so the PDF is self-contained:
   ```css
   @font-face{font-family:"Display Face";font-weight:600;font-style:normal;
     src:url(data:font/woff2;base64,<BASE64>) format("woff2");}
   ```
   Variable fonts: give a weight *range* (`font-weight:400 700;` with `format("truetype")`).
3. **Keep the HTML source clean, inject at build.** Author `brandbook.src.html` with a `/*FONTS*/`
   marker and `LOGO_URI` placeholders; a tiny script swaps in the base64 font CSS + logo data URI to
   produce the final `brandbook.html`. (Keeps the editable source small; the final render is large.)
4. **Verify the specimen is the real face** after rendering — not a fallback.

### The real logo, embedded — never reconstructed
- Place the **actual supplied logo file** as an `<img>` (base64 data URI so the PDF is
  self-contained) on every page the logo appears. **Do not rebuild the mark in HTML/CSS/SVG.**
- For a ground where the logo doesn't contrast, change the ground or wrap the logo in a light
  circular/rounded tile — never recolor the client's mark. An inverted/mono "color version" is only
  allowed as an explicit, labelled color version generated from the real asset.
- All other images (photography) must be local files or data URIs too. No remote URLs at render time.

## Render pipeline (headless browser print-to-PDF)

Preferred: a headless Chromium "print to PDF" of the HTML. Any of these work; pick what's installed:

1. **Headless Chrome (most portable):**
   ```
   chrome --headless --disable-gpu --no-pdf-header-footer \
     --print-to-pdf="brandbook.pdf" "file:///abs/path/template.html"
   ```
2. **Playwright / Puppeteer** (when a Node pipeline exists): load the file, call
   `page.pdf({ width: '1280px', height: '720px', printBackground: true })`.
3. **wkhtmltopdf** as a fallback (weaker CSS support; verify the result).

**Always set `printBackground: true` / ensure background colors print** — the brand grounds are
essential, and browsers omit backgrounds by default.

## Verify the output

- **Run `QUALITY.md` — the full pre-ship checklist — against the rendered PDF.** Don't skip it.
- Quick pass: correct page count, one page per section, 16:9, backgrounds present, **the real logo
  (not reconstructed)**, **real fonts rendering (not substituted)**, images sharp, no clipped
  content (check a browser's continuous scroll too).
- Then present it to the client. Iterate by editing the source HTML/tokens and re-rendering.

## Output location

`system/<project>/brandbook.pdf` + the working `system/<project>/brandbook.html` and
`system/<project>/brand-tokens.json`.
