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

If a visitor has JavaScript off, all four sections simply stack down the page —
nothing is lost. Printing the page does the same, so Cmd-P gives you everything.

## Adding your photo

Drop a portrait-crop image into `files/` and point the Overview tab's `<img>` at
it — change `src="files/profile.svg"` to `src="files/profile.jpg"`. The shipped
`profile.svg` is just a grey placeholder; delete it once yours is in.

The black vertical rule beside the photo is `--bar` in `style.css`. It's
near-black in light mode and near-white in dark mode so it stays visible either
way — if you want it black always, set both `--bar` values to `#111111`.

## Adding a paper

Copy one whole `<li>` ... `</li>` block inside `<ol class="papers">` and edit the
copy. Drop the PDF into `files/` and point the link at `files/your-file.pdf`.

## Changing the accent color

In `style.css`, edit `--accent` (two places: light mode and the dark-mode block).
