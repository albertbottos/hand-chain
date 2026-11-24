# Hand chain

Static site: seven pages about hand chain jewelry (what the piece is, the
styles, sizing, bracelet comparison, layering, metals, FAQ).

Plain HTML and one stylesheet. No JavaScript, no framework, no build step, no
web fonts, no third-party requests — no CDN, no analytics, no images. Open any
page directly in a browser; what is in the repo is what is served.

## Files

```
index.html                          home
types-of-hand-chains.html           five styles, compared
how-to-measure-hand-chain-size.html wrist, ring and span measurements
hand-chain-vs-bracelet.html         fit, wear and styling comparison
layering-hand-chains.html           stacking with rings, bracelets, a watch
materials-guide.html                gold filled vs plated vs sterling
faq.html                            short answers, FAQPage schema
style.css                           the only stylesheet (7.2 KB)
robots.txt
sitemap.xml
```

All links are relative, so the site works at any path, on any static host, and
from `file://` without a server.

## Local preview

```
python3 -m http.server 8000
```

Then open http://localhost:8000/. Every page loads one CSS file and nothing else.

## Page contract

Each page carries: a title under 60 characters, a meta description under 155,
a canonical URL, Open Graph tags (`og:type`, `og:site_name`, `og:title`,
`og:description`, `og:url`, `og:locale`), exactly one `h1`, and a JSON-LD block
(`Article`, or `FAQPage` on the FAQ) copied from the content pack with the
canonical `url` and `mainEntityOfPage` added at build time.

Markup is semantic — `header`, `nav`, `main`, `article`, `section`, `h1`–`h3`,
`ul`/`li`, `time`. Section elements are labelled with `aria-labelledby`. There
are no layout wrappers beyond one `.wrap` per band.

## Design

Tokens are taken unchanged from the visual kit (`design/tokens.json`): warm
ivory ground, one terracotta accent, gold restricted to hairlines and the
ornament, system font stacks only — Charter/Iowan/Palatino/Georgia for display,
`system-ui` for body. Body text 14.59:1 on the page ground, muted 5.96:1, links
5.75:1; every pair used for copy clears WCAG AA. The hero is CSS gradients plus
an inline 768-byte SVG chain ring, so it costs no requests. Motion is limited to
180 ms hover transitions and is disabled under `prefers-reduced-motion`.

## Content

Copy, titles, meta descriptions, headings and JSON-LD come from the content
pack (seven markdown pages). Both editors were written for one search intent
each and cross-link in a closed loop of three links per page; the pack's FAQ
answers are deliberately shorter than the guides they point to.

Editorial copy only. No products, prices, reviews or claims are stated, and
nothing here sells anything.

## Canonical origin

The canonical URLs assume GitHub Pages at
`https://albertbottos.github.io/hand-chain/`. If the site moves to its own
domain, the origin is used in exactly four places per page — canonical,
`og:url`, JSON-LD `url`, JSON-LD `mainEntityOfPage` — plus `sitemap.xml` and
`robots.txt`. Search and replace the origin, not the paths.

## Still open

- No OG image exists, so social previews fall back to text. The design kit has
  no photography and the repo carries no image assets by design.
- JSON-LD omits `publisher` and `image`, which Article rich results can use;
  both need a site name, logo and image assets first.
- `datePublished` in the schema and the visible "Updated" line are build dates.
  Replace them with real publish dates when the pages go live.
- Sitemap and robots point at the Pages origin above; the site has not been
  deployed, so those URLs are not live yet.
