---
name: brandbook
description: >-
  Creates a complete, professional brand book (brand guidelines) as a PDF, from
  intake to signed-off document. Use at the START of any brand/design project:
  if the client has no brand book, this skill creates one — asking the client
  questions first (logo? colors? fonts? direction?), generating what's missing
  (including a wordmark when there's no logo), and producing a 16:9 PDF built
  from a proven agency structure. Nothing else in a project proceeds until the
  brand book is agreed and signed off. Output: an HTML/CSS → PDF brand book plus
  the structured brand tokens other tools consume.
---

# brandbook

Creates a real brand book — the kind an agency ships — as a **PDF document**, and treats it as
the **gate** for everything downstream. A design system, website, or any branded artifact is
built *from* an agreed brand book. If the client doesn't have one, this skill makes one; and no
token, component, or page is produced until the client and the agent **agree on the brand book
and sign it off.**

It is a standalone skill, and it is the first thing `atelier`'s `GENERATE.md` invokes.

## The non-negotiable flow

```
1. ASK  — intake questions first (never assume). Does the client have a logo? colors?
          fonts? a direction? references? existing assets?
2. GATHER — collect what exists; identify what's missing.
3. GENERATE — create everything missing (wordmark if no logo, palette, type pairing,
          usage rules) using the atelier method.
4. PRESENT — render the brand book PDF and show it to the client.
5. ITERATE — revise against feedback.
   ───────────────── HARD GATE: do not proceed past here without sign-off ─────────────────
6. SIGN-OFF — explicit client agreement on the brand book.
7. HANDOFF — emit brand tokens for the design-system / page build to consume.
```

**Steps 3–6 can loop many times.** The agent must not start the design system, components, or
pages until step 6 is reached. The brand book is the contract.

## Step 1 — Intake questions (ask these first, always)

Collect before generating anything. Ask conversationally; don't dump all at once if a few
answers make others moot.

**Brand basics**
- Brand / company name, and the one-line "what it is".
- Industry / register, and the organizing idea (what makes it *this* brand, not a competitor).
- Audience and tone (3–5 adjectives: e.g. clinical, playful, premium, warm, technical).

**Existing assets (the key branching questions)**
- **Do you have a logo?** If yes → ask for the file (SVG/PNG/PDF) and whether it's final.
  If no → the skill will generate a **wordmark direction + candidates** (see below).
- **Do you have brand colors?** If yes → collect exact values (HEX/RGB/Pantone/CMYK if print).
  If no → generate a palette per the color method.
- **Do you have brand fonts?** If yes → names + licensing/source. If no → propose a pairing.
- **Any existing brand book, references, or sites** you like (and dislike)?
- **Where will this brand live?** (web, print, app, packaging) — decides which pages matter.

**Logistics**
- Primary language; any secondary languages.
- Who signs off, and by when.

Record answers in `brandbook/intake/<project>.md`.

## The no-logo path — generate a wordmark

When the client has no logo, **do not block and do not fake a final mark.** Generate a
**typographic wordmark direction + a few candidates** (the reference agency brand book is exactly this — a
styled text logo, not a pictorial mark):

- Build 2–4 wordmark candidates from the chosen/ proposed typeface, each making one deliberate
  letterform move (a distinctive terminal, an italic swap, a ligature, a cut).
- Present them honestly as **direction to iterate**, not a finished logotype (per atelier's logo
  limits: a client-ready final mark needs human iteration).
- Once the client picks one, it becomes the book's logo and all logo pages are built around it.

## Step 3 — Generate missing pieces with the atelier method

Everything generated obeys the atelier method (don't reinvent it):
- **Color** → `../method/01-color.md` (pick the posture; produce the palette + the swatch
  values the Brand-colors page needs: HEX always, RGB, and Pantone/CMYK if print is in scope).
- **Type** → `../method/02-typography.md` (typeface strategy + the role hierarchy the
  Typographic-hierarchy page needs: Title / Subtitle / Subheading / Body mapped to faces).
- **The one bold move** → the brand's signature, surfaced as a dedicated spread (the reference book
  spends it on "logo elements in typography" — the italic *u* threaded into words).

## The page structure (extracted from a reference agency brand book)

A complete book is ~18–24 landscape (16:9) pages. Build the pages the brief needs; this is the
canonical superset and order. See `template/pages.md` for the detailed spec of each.

| # | Page | Required? | Contents |
|---|---|---|---|
| 1 | **Cover** | required | Wordmark, "Brand Guidelines", year / version, author / agency |
| 2 | **Logo** | required | Primary logo, clean, on white |
| 3 | **Exclusion zone** | required | Clearspace in logo-derived units |
| 4 | **Logo guidelines / construction** | recommended | Cap-height / baseline, proportions |
| 5 | **Color versions** | required | Primary / secondary / achromatic lockups |
| 6 | **Brand colors** | required | Swatches with HEX / RGB / (Pantone / CMYK if print) |
| 7 | **Logo icon** | recommended | App-icon treatments (circle, squircle, tiny sizes) |
| 8 | **Minimum size** | recommended | Smallest legible size (print mm / screen px) |
| 9 | **Main typeface** | required | Primary font, specimen, source |
| 10 | **Secondary typeface** | recommended | Secondary font, specimen, source |
| 11 | **Typographic hierarchy** | required | Title / Subtitle / Subheading / Body roles |
| 12 | **Typographic hierarchy — color variations** | optional | Hierarchy across grounds |
| 13 | **The signature move** | recommended | The brand's one bold move, shown |
| 14 | **The signature move — guidelines** | optional | How to construct/apply it |
| 15 | **Interactive / UI text elements** | optional (web) | Buttons/links across grounds + states |
| 16 | **Logo composition rules** | recommended | Logo in H / square / V formats |
| 17 | **Logo composition — guidelines** | optional | Construction of the above |
| 18 | **Logo placement** | recommended | Logo on photography, corner anchoring |
| 19 | **Logo placement — guidelines** | optional | Safe-area construction |
| 20 | **Logo on background image** | recommended | Legibility over imagery |
| 21 | **Logo misuse** | required | Don'ts grid (stretch, recolor, rotate, crowd…) |
| 22 | **Co-branding** | optional | Partner lockups |

**Page chrome (every inner page):** a small brand-name eyebrow (accent color) + the page title,
top-left; generous margins; one idea per page. Cover and section pages may use a full brand-color
ground; spec pages are on white.

## Step 7 — Output

1. **The PDF** — `system/<project>/brandbook.pdf`, rendered HTML/CSS → PDF (see `template/`).
2. **Brand tokens** — `system/<project>/brand-tokens.json`: the agreed logo path(s), color
   values (named + HEX/RGB/print), type roles + faces, the signature move. This is what the
   design-system / page build consumes downstream. The PDF is for humans; the tokens are for the
   next tool.

## How the PDF is built (HTML/CSS → PDF)

- Each page is an HTML section sized to a 16:9 page box; print CSS gives one page per section.
- A single stylesheet carries the brand tokens as CSS variables, so the book is *itself* on-brand.
- Render with a headless-browser print-to-PDF step (see `template/render.md` for the exact
  pipeline and the page/@media-print setup). Fonts are embedded; images are local.
- The template is in `template/` — adapt it per project by setting the token variables and
  filling each page's content; don't rebuild the chassis each time.

## Honest limits

- **Logo = direction, not final.** When generated, it's a wordmark direction + candidates to
  iterate, never presented as a finished, trademark-ready logotype.
- **The gate is real.** If the user tries to skip to the website/design system, stop and point
  back to sign-off. An unsigned brand book means the foundation isn't agreed yet.
- **Print values** (Pantone/CMYK) are only generated when print is in scope; otherwise HEX/RGB.
