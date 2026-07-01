# bjornpaedia

Personal wiki / knowledge base for Kristian Bjornard, focused on sustainability, free/libre open source, design, and related ideas.

Live at: bjornpaedia.wjerk.shop (deployed via GitHub Pages, CNAME configured)

## Stack

- **TiddlyWiki 5** — the entire site is TiddlyWiki-based, not Jekyll or any conventional static site generator
- `index.html` — current single-file TiddlyWiki (v5.3.3), the primary file
- `static.html` / `alltiddlers.html` — generated all-tiddlers views
- `static/` — individual tiddler exports as standalone HTML files (URL-encoded filenames)
- `dynamic.html`, `tiddlers.html`, `tiddlywiki.html`, `0202401050238-alltiddlers.html`, `z-old/` — legacy/archived files from earlier setups, **not** touched by the current publish pipeline; don't touch unless explicitly asked
- No build step here; GitHub Pages serves the files directly

## Workflow

**This repo does not author content.** It's the deploy target for `sad2021tw/` in the separate `sentence-a-day` repo (see below), synced locally on the author's machine.

- Content is authored in TiddlyWiki inside `sentence-a-day/sad2021tw/` (via `tiddlywiki sad2021tw --listen`)
- `sentence-a-day/build.sh` does a clean rebuild into `sad2021tw/output/` (wipes and regenerates `index.html`, `static.html`, `alltiddlers.html`, `static/`)
- `sentence-a-day/publish.sh` runs that build, then syncs the output into this repo:
  - `static/` is synced with `rsync --delete` — it's fully generated and disposable; hand-edits there get wiped on the next publish
  - `index.html`, `static.html`, `alltiddlers.html` are copied over directly
  - everything else in this repo (this file, `README.md`, `CNAME`, the legacy files above) is left untouched
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

Content by Kristian Bjornard is CC BY-SA. Code is per TiddlyWiki's BSD license.
