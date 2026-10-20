# kora-aerospace-web

Company site, www.kora-aerospace.com, in English (`/`) and Turkish
(`/tr/`). Plain HTML and CSS, no build step. GitHub Pages serves the repo
root of `main`. The only JavaScript is the pause button of the video.

Design language: `design/DESIGN.md` in the monorepo (owner: designer).
Media: `design/media/` (real photos and the takeoff clip).

| File | What |
| --- | --- |
| `index.html`, `tr/index.html` | The page in English and Turkish. Change both together. |
| `404.html` | Shown for unknown paths, such as old kora-aerospace.org links. |
| `tokens.css` | Copy of `design/tokens.css`. Do not edit here. |
| `styles.css` | Self-hosted `@font-face` rules and the layout. Uses only the `--kora-*` tokens. |
| `fonts/` | Space Grotesk and JetBrains Mono, woff2, latin and latin-ext. |
| `media/` | Logo (copy of `design/logos/kora-logo-on-dark.svg`), clip, photos, `og.jpg` link preview. |
| `favicon.*`, `favicon-96.png`, `icon-512.png`, `apple-touch-icon.png` | Copies of `design/logos/favicon/`. |
| `LICENSES/` | Font (SIL OFL 1.1) and icon (Lucide, ISC) licences. |

Run locally:

    python3 -m http.server 8080

Update design files (from the monorepo root):

    cp design/tokens.css web/kora-aerospace-web/tokens.css
    cp design/logos/favicon/* web/kora-aerospace-web/

The clip has two sizes. A phone gets the 720 px file, a wider screen the
1280 px file, and a visitor who asks for reduced motion gets only the
poster (`<source media>`). Encode from `design/media/takeoff.mp4`:

    ffmpeg -i takeoff.mp4 -an -vf scale=1280:-2 -c:v libx264 -preset slow -crf 27 -pix_fmt yuv420p -movflags +faststart media/takeoff-1280.mp4
    ffmpeg -i takeoff.mp4 -an -vf scale=720:-2 -c:v libx264 -preset slow -crf 28 -pix_fmt yuv420p -movflags +faststart media/takeoff-720.mp4

Photos: WebP at twice the shown size, with `width`, `height` and
`loading="lazy"` on the `<img>`:

    cwebp -q 72 -resize 1100 0 in.jpg -o media/name.webp

To check a phone width, load the page in an iframe of that width. A
headless Chrome window cannot be narrower than about 500 px, so a
`--window-size=390,...` screenshot shows a 500 px layout cut at 390 px.

Icons are inline SVG from Lucide 1.47.0 (lucide.dev). The stroke width
comes from `.icon` in `styles.css`.
