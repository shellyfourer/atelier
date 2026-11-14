# Photography — always present real, on-brand photos (never placeholder blocks)

Placeholder color blocks on the placement / on-imagery pages undercut the whole premium feel. A
brand book must **always show real photography** on those pages. This is the sourcing method.

## The source decision (studied, 2026)

The keyless/no-setup stock routes have degraded, so the licensing-safe landscape is:

| Source | Keyless? | Quality | License | Use |
|---|---|---|---|---|
| Unsplash Source (keyless URL) | — | — | — | **Dead** (sunset June 2024) |
| **Unsplash API** | needs a free key | **high, curated** | commercial OK; attribution required | **Default** — best quality/effort |
| Pexels API | key issuance **paused** (2026) | high | commercial OK, no attribution | use if keys reopen |
| Openverse API | yes, keyless | low (CC Flickr grab-bag) | often CC-BY → attribution required | keyless fallback only |
| AI image generation | n/a | controllable | model-dependent | when no stock fits / fully on-brand needed |

**Default: Unsplash API** (free developer key, 50 req/hr demo). If no key is available, fall back to
AI-generated on-brand imagery, then Openverse as a last resort. Never ship raw placeholder blocks.

## Method (mood + color matched)

1. **Derive queries from the brand's register + subject matter** (from the brief / tokens), not
   generic terms. E.g. a wellness blog → "yoga morning calm", "herbal tea still life", "journaling
   self care", "movement studio". Aim for *specific* scenes, not "lifestyle".
2. **Match tone to the palette.** Unsplash supports a `color` filter and returns each photo's
   dominant tone — prefer photos whose tone harmonizes with the brand (warm/green/cream here).
   Color-match makes the photos feel *chosen*, not random stock.
3. **Orientation per slot:** `portrait` for vertical frames, `landscape` for horizontal. Fetch the
   `regular` size.
4. **Curate — don't take the first blindly:**
   - **No third-party trademarks/logos** in frame (a branded teabag, a visible brand on a product
     implies endorsement and violates stock licenses). Re-query if the top result has one.
   - Avoid clichés and anything off-register. A clean texture (linen, paper, stone) is often a
     better "logo-on-imagery" background than a busy literal object.
5. **Embed + credit.** Base64-embed the photos (self-contained PDF). Add a **small photographer
   credit** on the image (`Photo — <name>`, ~10px, white with a shadow for legibility) — Unsplash
   attribution is required, and it reads appropriately editorial. Add a scrim/gradient behind any
   logo/text placed on a photo so it stays legible.
6. **Trigger Unsplash's download endpoint** per their API guidelines when you use a photo.

## Unsplash API quick reference

- Search: `GET https://api.unsplash.com/search/photos?query=<q>&orientation=portrait&color=green&per_page=6&content_filter=high`
  with header `Authorization: Client-ID <ACCESS_KEY>`.
- Each result: `urls.regular` (download), `user.name` (credit), `color` (dominant tone),
  `links.html` (photo page), `links.download_location` (ping on use).
- Get a free key at `unsplash.com/developers` → New Application → Access Key.

## Which pages need real photos

- **Logo placement** — logo on a brand bar over a photo (vertical + horizontal).
- **Logo on imagery** — emblem in a light tile over a dark photo; wordmark in cream over a textured
  photo (with scrim).
- Optionally a **cover** or **divider** that uses full-bleed photography for a given register.

Record the chosen photos + credits + source in the project folder (e.g. `assets/photos/credits.json`)
so the attribution and provenance are traceable.
