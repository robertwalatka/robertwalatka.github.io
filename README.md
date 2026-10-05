# Personal website

A single-page academic site, hosted free on GitHub Pages.

## Files

| File | What it is |
| --- | --- |
| `index.html` | All the content. Every spot you need to change is marked `EDIT ME`. |
| `style.css` | All the styling. Colors are at the top in the `:root` block. |
| `files/` | Put your `cv.pdf` and paper PDFs here. |

## How to edit

1. Open `index.html` in any text editor (TextEdit in plain-text mode works, but
   [VS Code](https://code.visualstudio.com) is nicer).
2. Change the text. Save.
3. Double-click `index.html` to preview it in your browser — no server needed.
4. In GitHub Desktop: write a short summary, **Commit to main**, then **Push origin**.
5. Wait ~30-60 seconds and reload your live site.

## The four tabs

The page has four tabs — Overview, Papers, CV, Personal — and they're just four
`<section class="panel">` blocks in `index.html`, each marked with a big comment
banner. Clicking a tab shows one and hides the others; the URL updates too, so
`...github.io/#papers` links straight to the Papers tab and the back button works.

To rename a tab, change it in *two* places: the link text in `<nav class="tabs">`
and the `<h2>` inside that section. To reorder them, reorder the `<a>` links.
To add a fifth, add an `<a href="#newid">` link and a matching
`<section class="panel" id="newid">`.

Each section's `<h2>` is hidden on screen, because the tab bar already shows the
same word. It's still in the markup on purpose: screen readers use it to
navigate, and printing brings it back — on paper there's no tab bar, so the
headings are the only thing labelling the four stacked sections. Don't delete
them.

If a visitor has JavaScript off, all four sections simply stack down the page —
nothing is lost. Printing the page does the same, so Cmd-P gives you everything.

## Font and colors

The whole site uses one type stack and one palette, both at the top of
`style.css` in the `:root` block:

- `--sans` is the font stack, led by **Lato**. Lato isn't installed on any
  operating system, so `index.html` loads it from Google Fonts — which means
  every visitor sees the same thing, Windows included. The Helvetica/Arial
  fallbacks only show for the instant before it arrives, or for people who
  block webfonts. If you ever swap the font, change the Google Fonts `<link>`
  in `index.html` *and* `--sans` here.
- `--bg` is the dark grey background, `--text` the off-white text, `--accent`
  the link and active-tab color, `--bar` the vertical rule beside your photo.

If you change `--accent`, check it still contrasts against `--bg`. Paste both
into [WebAIM's contrast checker](https://webaim.org/resources/contrastchecker/)
and aim for 4.5:1 or better, since the accent is used on link text.

The site is dark all the time — it no longer follows the visitor's light/dark
setting. Printing is the one exception: Cmd-P flips to black-on-white so you
don't get a grey slab, and prints all four tabs.

## Adding your photo

The photo lives in the masthead at the top right, in `files/profile.jpg`. To
replace it, overwrite that file with a 4:5 portrait crop and update the `<img>`
width/height to match.

Keep it small — a camera original is several megabytes and will make the page
crawl. `files/profile.jpg` is 600x750 at about 67 KB. On a Mac you can crop and
shrink one in Terminal without any extra software:

```bash
sips --cropOffset 250 1145 -c 2598 2078 original.jpg --out files/profile.jpg && sips -z 750 600 files/profile.jpg && sips -s formatOptions 72 files/profile.jpg --out files/profile.jpg
```

## The mountains and the grain

Two decorative bits, both pure CSS/SVG with no image files and no extra
requests:

**The skyline** is the inline `<svg class="range">` between the masthead and
the tab bar. It's one continuous contour in the single-line-drawing style, with
a second stroke doubling back below each summit to leave the thin ridge
"lenses", plus a scalloped line across each peak for the snow cap. It spans the
page width. Its colour follows `--bar` and its faintness is the `opacity` in
`.range` — raise that if you want it more present. To remove it, delete the
whole `<svg>`.

Three things matter if you reshape it:

- Keep the relief steep — roughly 6:1 or better. Flatter and the peaks read as
  hills, not mountains.
- Snow caps have to sit *inside* the silhouette, below the apex and between the
  two flanks, or they poke out through the skyline.
- Don't stack a snow cap on top of two ridge lenses at the same summit; the
  three lines tangle. One lens plus one snow cap per peak is the limit.

To see your edits clearly while working, temporarily set `.range`'s opacity to
`1` and narrow the `viewBox` to one peak (e.g. `700 0 260 130`).

**The grain** is the `background-image` on `body` in `style.css`: a 240px tile
of about 50 tiny dots and dashes, half a shade lighter than the page and half a
shade darker, none above 10% opacity. It covers under 1% of the tile, so it
registers as texture rather than pattern. Delete that one declaration to remove
it.

The highlighted job-title line uses `--highlight` for the block behind it. The
grain, the skyline and that block are all suppressed when printing.

## Adding a paper

Copy one whole `<li>` ... `</li>` block inside `<ol class="papers">` and edit the
copy. Drop the PDF into `files/` and point the link at `files/your-file.pdf`.
