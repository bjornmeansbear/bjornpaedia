# bjornpaedia

Personal wiki / knowledge base for Kristian Bjornard, focused on sustainability, free/libre open source, design, and related ideas.

Live at: bjornpaedia.wjerk.shop (deployed via GitHub Pages, CNAME configured)

## Stack

- **TiddlyWiki 5** — the entire site is TiddlyWiki-based, not Jekyll or any conventional static site generator
- `index.html` — current single-file TiddlyWiki (v5.3.3), the primary file
- `dynamic.html` — older TiddlyWiki version (v5.2.0), kept for reference
- `static/` — individual tiddler exports as standalone HTML files (URL-encoded filenames)
- `z-old/` — archived older content, don't touch unless explicitly asked
- No build step; GitHub Pages serves the files directly

## Workflow

- Content is authored inside TiddlyWiki (in the browser)
- The single-file `index.html` is saved/exported from TiddlyWiki and committed here
- Individual tiddler HTML exports land in `static/`
- Push to `master` → GitHub Pages deploys automatically

## Related repo

Source tiddlers and writing originate at: https://github.com/bjornmeansbear/sentence-a-day

## What NOT to do

- Don't add a Jekyll config, Gemfile, or any static site generator scaffolding — this is not that kind of site
- Don't edit the internals of `index.html` by hand — it's a generated TiddlyWiki file; suggest TiddlyWiki-native approaches instead
- Don't delete or rename files in `static/` without checking — filenames are URL-encoded tiddler titles

## License

Content by Kristian Bjornard is CC BY-SA. Code is per TiddlyWiki's BSD license.
