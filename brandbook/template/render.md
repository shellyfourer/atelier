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

## Fonts & assets (must embed / be local)

- Self-host the brand fonts via `@font-face` with local files (or base64 data URIs) so the PDF
  embeds them — never rely on a remote font at print time.
- All images (logo, photography) must be local files or data URIs. No remote URLs at render time.

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

- Open the PDF: correct page count, one page per section, 16:9, backgrounds present, fonts
  embedded (not substituted), images sharp, no clipped content.
- Then present it to the client. Iterate by editing the HTML/tokens and re-rendering — fast loop.

## Output location

`system/<project>/brandbook.pdf` + the working `system/<project>/brandbook.html` and
`system/<project>/brand-tokens.json`.
