# kora-aerospace-web

Company site, www.kora-aerospace.com. Plain HTML and CSS, no build step,
no JavaScript. GitHub Pages serves the repo root of `main`.

Design language: `design/DESIGN.md` in the monorepo (owner: designer).

| File | What |
| --- | --- |
| `index.html` | The landing page. |
| `404.html` | Shown for unknown paths, such as old kora-aerospace.org links. |
| `tokens.css` | Copy of `design/tokens.css`. Do not edit here. |
| `styles.css` | Self-hosted `@font-face` rules and the layout. Uses only the `--kora-*` tokens. |
| `fonts/` | Space Grotesk and JetBrains Mono, woff2, latin and latin-ext. |
| `media/` | Logo (`design/logos/kora-logo-light.svg`), WebP photos, `og.jpg` link preview. |
| `favicon.*`, `apple-touch-icon.png` | From `design/logos/kora-icon-*.svg`. |
| `LICENSES/` | Font (SIL OFL 1.1) and icon (Lucide, ISC) licences. |

Run locally:

    python3 -m http.server 8080

Update the design tokens (from the monorepo root):

    cp design/tokens.css web/kora-aerospace-web/tokens.css

To check a phone width, load the page in an iframe of that width. A
headless Chrome window cannot be narrower than about 500 px, so a
`--window-size=390,...` screenshot shows a 500 px layout cut at 390 px.

Add an image: convert it to WebP, about 1400 px wide, and set `width`,
`height` and `loading="lazy"` on the `<img>`:

    cwebp -q 75 -resize 1400 0 in.png -o media/name.webp

Icons are inline SVG from Lucide 1.47.0 (lucide.dev). The stroke width
comes from `.icon` in `styles.css`.
