# kora-aerospace-web

Company site, www.kora-aerospace.com. Plain HTML and CSS, no build step,
no JavaScript. GitHub Pages serves the repo root of `main`.

| File | What |
| --- | --- |
| `index.html` | The landing page. |
| `404.html` | Shown for unknown paths, such as old kora-aerospace.org links. |
| `tokens.css` | Colors, fonts, sizes. Copy of `design/tokens.css` from the monorepo. Do not edit here. |
| `styles.css` | Layout. Uses only the variables from `tokens.css`. |
| `media/` | Images, WebP, compressed. |

Run locally:

    python3 -m http.server 8080

Update the design tokens (from the monorepo root):

    cp design/tokens.css web/kora-aerospace-web/tokens.css

Add an image: convert it to WebP, about 1400 px wide, and set `width`,
`height` and `loading="lazy"` on the `<img>`:

    cwebp -q 75 -resize 1400 0 in.png -o media/name.webp
