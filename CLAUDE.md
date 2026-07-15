# bjornpaedia

Personal wiki / knowledge base for Kristian Bjornard, focused on sustainability, free/libre open source, design, and related ideas.

Live at: bjornpaedia.wjerk.shop (deployed via GitHub Pages, CNAME configured)

## Stack

- **TiddlyWiki 5** — the entire site is TiddlyWiki-based, not Jekyll or any conventional static site generator
- The site is **fully static** — no interactive/editable "live" TiddlyWiki is published here. `index.html` is a generated homepage (a filtered list of entries linking into `static/`), not the single-file interactive wiki.
- `index.html` — generated static homepage, rendered from `$:/core/templates/static.template.html` (shadow-customized in the source wiki)
- `static/` — individual tiddler exports as standalone HTML files (URL-encoded filenames)
- No build step here; GitHub Pages serves the files directly

**Why fully static (as of 2026-07-14):** the site used to also publish a full interactive single-file wiki (`index.html` built from the TiddlyWiki core's "offline save" template) plus `static.html`/`alltiddlers.html` (an all-tiddlers single-file dump). All three embedded the *entire* tiddler store with no `private`/`hide` filtering — confirmed a `private`/`hide`-tagged entry was leaking into all three published files even though it was correctly excluded from `static/`. Static-only output is now the only thing published, since per-tiddler files are the only build path that reliably respects the exclusion.

## Workflow

**This repo does not author content.** It's the deploy target for `sad2021tw/` in the separate `sentence-a-day` repo (see below), synced locally on the author's machine.

- Content is authored in TiddlyWiki inside `sentence-a-day/sad2021tw/` (via `tiddlywiki sad2021tw --listen`)
- `sentence-a-day/build.sh` does a clean rebuild into `sad2021tw/output/` (wipes and regenerates `index.html` and `static/`)
- `sentence-a-day/publish.sh` runs that build, then syncs the output into this repo:
  - `static/` is synced with `rsync --delete` — it's fully generated and disposable; hand-edits there get wiped on the next publish
  - `index.html` is copied over directly
  - everything else in this repo (this file, `README.md`, `CNAME`) is left untouched
- **Tiddlers tagged `private` or `hide` in the source wiki are intentionally excluded** from what gets published here — if a tiddler you'd expect to see is missing from `static/`, check its tags in `sentence-a-day` before assuming something's broken
- The publish script pauses for manual confirmation before committing/pushing here — pushing to `master` is what triggers GitHub Pages to redeploy

## Related repo

Source tiddlers and writing originate at: https://github.com/bjornmeansbear/sentence-a-day — that's also where `build.sh`/`publish.sh` and the publishing pipeline live (see its `CLAUDE.md` and `TIDDLYWIKI_CUSTOMIZATIONS.md`).

## What NOT to do

- Don't add a Jekyll config, Gemfile, or any static site generator scaffolding — this is not that kind of site
- Don't edit the internals of `index.html` by hand — it's a generated TiddlyWiki file; suggest TiddlyWiki-native approaches instead
- Don't hand-edit or reorganize files in `static/` — the entire directory is regenerated and `--delete`-synced from `sentence-a-day` on every publish, so manual changes here don't persist
- Don't try to "fix" missing content by loosening the private/hide exclusion — that's deliberate; the fix belongs in the source tiddler's tags, in `sentence-a-day`

## License

Content by Kristian Bjornard is CC BY-SA. Code is per TiddlyWiki's BSD license. Quotes or other attributes are © their respective authors, used here as references, please correct me if I'm missing or hae incorrectly attributed sources.
