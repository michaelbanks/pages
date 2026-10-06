# CLAUDE.md

My public static site, served by GitHub Pages at https://michaelbanks.github.io/pages/. Two kinds of page live here:

- **Product pages**: what an app or extension is, its privacy policy, terms, release notes and support. Store listings
  and the apps themselves link to these, so their URLs must not move.
- **Write-ups**: pages for other people to read on their own screens (what a project does, how it works, what we
  built). Not for code or notes to myself.

No site generator, no build step, no package.json. The folder is served as it is.

## Layout

```
index.html             the front page: a card per project
styles.css, 16.png     shared by every page
sitemap.xml, robots.txt
<project>/index.html   the project's page: a card per product page, a list of write-ups
<project>/<page>.html  privacy-policy.html, release-notes.html, a write-up such as mash/what-we-built.html…
```

- One folder per project, pages named in lower-case-with-dashes. A write-up's date goes on the page, not in its name.
- Every project gets a card on the front page. On a project's `index.html`, each product page gets a card and each
  write-up a line in the Write-ups list (newest first, with its date and a one-line summary).
- Every new page gets an entry in `sitemap.xml`. When a page's content changes, its `lastmod` moves to that day.

## One look for every page

Pages in a project folder link `../styles.css` and `../16.png`, and sit in its white `.container`. A project's
`index.html` opens with a Home link; a page under it opens with a Back link to that `index.html`. Use the classes
already in `styles.css`: cards with a Learn More button, and `.write-ups` for the list of write-ups. Match the page next
to them. There is no dark mode, on any page.

## Write-ups

- They use the site's look like every other page. Anything of their own (tiles, chips, diagrams) goes in a `<style>`
  block in the page, in the site's colours: `#333` headings and strong text, `#666` body text, `#ddd` borders, `#f4f4f4`
  for shaded areas. Don't name a class `.card`: `styles.css` already styles it for the index pages.
- Everything fits the 760 px column inside the container. Diagrams are inline SVG drawn 760 wide
  (`viewBox="0 0 760 …"`), so their text shows at full size on a laptop. Nothing scrolls sideways except a wide table
  in its box.
- Pictures are built in as `data:` URIs: JPEG, about 1600 px wide at most, quality around 85. Keep a page under a few MB.
- Easy to scan: short sections, clear headings, a contents list at the top, tables where things compare.
- Written for someone opening the link cold: say what the thing is before how it works, explain jargon once, no
  internal shorthand without a word on what it means.
- Facts only from the project itself (its repo, git history, data); nothing invented.
- Monospace for names of files and commands: `ui-monospace, "SF Mono", Menlo, monospace`.

## Git

Commit each new or changed page with a message saying what it is. Pushing to `master` publishes it.
