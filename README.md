# Hand chain

Static site: seven pages about hand chain jewelry (what the piece is, the
styles, sizing, bracelet comparison, layering, metals, FAQ).

Plain HTML and one stylesheet. No JavaScript, no framework, no build step, no
third-party requests — no CDN, no analytics, no webfont CDN. Two typefaces are
self-hosted from `fonts/` and one photograph is served from `img/`. Open any
page directly in a browser; what is in the repo is what is served.

## Branches

| Branch | What it is |
|---|---|
| `main` | v1 design: warm ivory, system font stack, no photography. |
| `v2` | the v2.1 "specimen plate" design: Archivo + Newsreader, cobalt accent, the hand plate, numbered sections in the margin. Not merged, not deployed. |

## Files

```
index.html                          home — the plate page
types-of-hand-chains.html           five styles, compared
how-to-measure-hand-chain-size.html wrist, ring and span measurements
hand-chain-vs-bracelet.html         fit, wear and styling comparison
layering-hand-chains.html           stacking with rings, bracelets, a watch
materials-guide.html                gold filled vs plated vs sterling
faq.html                            short answers, FAQPage schema
style.css                           the only stylesheet (17.0 KB)
fonts/                              three woff2 subsets + both OFL licences
img/                                the hero plate, 640w and 1024w
robots.txt
sitemap.xml
```

All links are relative, so the site works at any path, on any static host, and
from `file://` without a server.

## Local preview

```
python3 -m http.server 8000
```

Then open http://localhost:8000/. A page loads one CSS file, three woff2
subsets (two preloaded, all `font-display: swap`), and — on the home page only —
one WebP rendition selected from `srcset`.

## Typography

| Face | Role | File | Bytes |
|---|---|---|---|
| Archivo 600 | display, numerals, labels | `fonts/archivo-600-sub.woff2` | 7,768 |
| Newsreader 400 | body, captions | `fonts/newsreader-400-sub.woff2` | 13,608 |
| Newsreader 400 italic | body italic | `fonts/newsreader-400i-sub.woff2` | 14,820 |

All three are Latin subsets: ASCII, NBSP, §, №, °, ·, ×, é, quotes and dashes,
primes, guillemets, €, ™ and the four arrows. Archivo ships as a variable font
and is instanced to `wght=600, wdth=100` before subsetting; Newsreader is
instanced to `wght=400, opsz=18`. Both families are under the SIL Open Font
License 1.1 — the licence files sit beside the subsets in `fonts/`.

## Page contract

Each page carries: a title under 60 characters, a meta description under 155,
a canonical URL, Open Graph tags (`og:type`, `og:site_name`, `og:title`,
`og:description`, `og:url`, `og:image`, `og:locale`), exactly one `h1`, and a
JSON-LD block (`Article`, or `FAQPage` on the FAQ) carrying the canonical `url`,
`mainEntityOfPage` and `image`.

Markup is semantic — `header`, `nav`, `main`, `section`, `h1`–`h3`, `ul`/`ol`/
`li`, `time`. Section elements are labelled with `aria-labelledby`, and the
rotated margin keys are links to the section they label.

## Design

v2.1 tokens: `paper` #EFEBE3 (the studio sweep the plate was graded to),
`ink` #14120E, `muted` #575147, `rule` #CBC2B1, `rule-strong` #8F8676, and one
accent — blueprint cobalt #1C34C8. Ink on paper is 15.73:1, muted 6.61:1,
accent 7.44:1, on-accent on accent 7.84:1; every pair used for copy clears WCAG
AA. Cobalt never appears as a large fill; it carries numerals, links, the button
and hairlines.

Layout is a 12-column grid with the type set off it: hero copy in columns 1–8
and the plate bleeding off the right edge, section rails in 1–2 and body copy
starting at 4. Numbered sections change shape as you scroll — two-column prose,
full-width numbered rows, a table whose rules leave the page, a full-bleed dark
band, a single-column close, a two-column index. Motion is limited to 150 ms
hover transitions.

## Content

Copy, titles, meta descriptions, headings and JSON-LD come from the content
pack (seven markdown pages). Both editors were written for one search intent
each and cross-link in a closed loop of three links per page; the pack's FAQ
answers are deliberately shorter than the guides they point to.

Editorial copy only. No products, prices, reviews or claims are stated, and
nothing here sells anything.

## Canonical origin

The canonical origin is `https://hand-chain-dev.digitalbuildr.com/`, the host
the site is served from. It is used in exactly four places per page — canonical,
`og:url`, JSON-LD `url`, JSON-LD `mainEntityOfPage` — plus `og:image`,
`og:image` metadata in JSON-LD, `sitemap.xml` and `robots.txt`. The path is the
page's own file name, with the home page at `/`, so every canonical names a
file the server returns; there are no extensionless URLs. Search and replace the
origin, not the paths.

## Still open

- JSON-LD omits `publisher`, which Article rich results can use; that needs a
  site-level logo URL first.
- `datePublished` in the schema and the visible "Updated" line are build dates.
  Replace them with real publish dates when the pages go live.
- The plate is one strand. The multi-strand and multi-ring constructions have
  no image of their own; a second plate would be the next purchase.
- Sitemap and robots point at the live origin above; nothing has been deployed
  from `v2` yet — the host answered 503 when checked on 24 November 2026, so
  those URLs do not resolve.

## Live

- Dev: https://hand-chain-dev.digitalbuildr.com
- Deploy: Coolify app `tp1j26ftf2brku0urquyc74l`, static build pack, auto-deploy
  on push to `main`.
