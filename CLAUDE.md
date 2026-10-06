# CLAUDE.md

My public static site, served by GitHub Pages at https://michaelbanks.github.io/pages/. Two kinds of page live here:

- **Product pages**: what an app or extension is, its privacy policy, terms, release notes and support. Store listings
  and the apps themselves link to these, so their URLs must not move.
- **Write-ups**: pages for other people to read on their own screens (what a project does, how it works, what we
  built). Not for code or notes to myself.

No site generator, no build step, no package.json. The folder is served as it is.

## Layout

```
index.html             the front page: a card per product, then every write-up, newest first
styles.css, 16.png     shared by the product pages
sitemap.xml, robots.txt
<project>/index.html   a product's page, with privacy-policy.html, release-notes.html and so on beside it
<project>/<topic>.html a write-up, e.g. mash/what-we-built.html
```

- One folder per project, pages named in lower-case-with-dashes. A write-up's date goes on the page, not in its name.
- Every new page gets an entry in `sitemap.xml`. When a page's content changes, its `lastmod` moves to that day.
- Adding a write-up means adding its line to the Write-ups list in `index.html` (newest first, with its date and a
  one-line summary).

## Product pages

They link `../styles.css` and `../16.png`, open with a Home link, and use the classes already in `styles.css`. Match
the page next to them.

## Write-ups: every page is one self-contained file

- Inline CSS, no external scripts, fonts or stylesheets: the file opens, emails and hosts on its own. It does not use
  `styles.css`.
- Pictures are built in as `data:` URIs: JPEG, about 1600 px wide at most, quality around 85. Keep a page under a few MB.
- Diagrams are inline SVG with a `viewBox`, inside a wide container, so they scale with the page.
- Light and dark mode (`prefers-color-scheme`), readable on a laptop and on a phone: body 16–17 px, line height about 1.6,
  text column about 760 px, wide figures up to about 1200 px, nothing that scrolls sideways except a wide table in its box.
- Easy to scan: short sections, clear headings, a contents list at the top, tables where things compare.
- Written for someone opening the link cold: say what the thing is before how it works, explain jargon once, no
  internal shorthand without a word on what it means.
- Facts only from the project itself (its repo, git history, data); nothing invented.
- A breadcrumb at the top leads back: `<a href="../index.html">Pages</a> / <Project>`.

### The shared look

Copy this `:root` block into every write-up so they belong together:

```css
:root {
  --bg: #fafaf9; --surface: #ffffff; --text: #18181b; --muted: #52525b; --border: #e4e4e7; --accent: #2b76b3;
  --day1: #dbeefb; --day1-ink: #0b3a5c; --day2: #afd6f2; --day2-ink: #0b3a5c; --day3: #6fb0e0; --day3-ink: #06263d;
  --day4: #2b76b3; --day4-ink: #ffffff; --day5: #0e3a63; --day5-ink: #ffffff;
  font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", system-ui, sans-serif;
}
@media (prefers-color-scheme: dark) {
  :root { --bg: #111113; --surface: #1c1c1f; --text: #f4f4f5; --muted: #a1a1aa; --border: #2e2e33; --accent: #6fb0e0; }
}
```

Monospace for names of files and commands: `ui-monospace, "SF Mono", Menlo, monospace`.

## Git

Commit each new or changed page with a message saying what it is. Pushing to `master` publishes it.
