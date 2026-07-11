# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

`yantosca.github.io` — Bob Yantosca's personal academic website, built on the **academicpages** Jekyll
template (a fork of the **Minimal Mistakes** theme), hosted via GitHub Pages. Content (CV, publications,
talks, teaching, projects, blog posts) lives as Markdown/YAML front matter in collection folders; the
theme (in `_layouts`, `_includes`, `_sass`, `assets`) is mostly upstream template code that should rarely
need changing.

## Common commands

Local development (Ruby/Jekyll):
```bash
bundle install                    # install Ruby gems (delete Gemfile.lock first if this errors)
bundle exec jekyll serve          # build + serve at http://localhost:4000, rebuilds on change
bundle exec jekyll serve --config _config.yml,_config.dev.yml   # serve with local dev overrides (analytics off, expanded CSS)
bundle exec jekyll build          # one-off build to _site/ without serving
```
There are no automated tests, linters, or CI in this repo — verification is "does the site build and
does the page look right in a browser".

Front-end asset build (rarely needed — only if editing `assets/js/_main.js` or vendor JS):
```bash
npm install
npm run build:js     # runs uglify to regenerate assets/js/main.min.js from assets/js/_main.js + vendor plugins
npm run watch:js      # rebuild main.min.js on change
```

Publication/talk markdown generation (one-off data import helpers, not part of the normal build):
```bash
cd markdown_generator
python pubsFromBib.py     # or run the .ipynb equivalents (PubsFromBib.ipynb, publications.ipynb, talks.ipynb)
```
These read a `.bib`/`.tsv` file and emit one Markdown file per entry into `_publications/` or `_talks/`.

Talk map generation (optional, only if `talkmap_link: true` in `_config.yml`):
```bash
cd _talks && python ../talkmap.py    # scrapes location from each _talks/*.md, geocodes it, writes talkmap/ data
```

## Architecture

**Jekyll collections are the primary content model.** Each top-level content type is its own collection,
configured in `_config.yml` under `collections:` with matching `defaults:` blocks that set its layout:

| Collection | Folder | Layout | Notes |
|---|---|---|---|
| pages | `_pages/` | `single` | CV, About, Projects, Publications index, Teaching, Personal, etc. |
| posts | `_posts/` | `single` | Blog entries, dated filenames |
| publications | `_publications/` | `single` | One file per paper, `output: true` |
| talks | `_talks/` | `talk` | `output: false` — rendered only via the talks listing page, not individual URLs |
| teaching | `_teaching/` | `single` | |
| videos | `_videos/` | `video` | |

Adding new content almost always means adding a new Markdown file with YAML front matter to the
appropriate collection folder (following the pattern of existing files there), not writing Ruby/Liquid
code.

**Site-wide config is split across two files:** `_config.yml` (author info, nav behavior, collections,
plugins, permalinks) and `_config.dev.yml` (local-only overrides — disables analytics, uses expanded
CSS — merged in via `--config _config.yml,_config.dev.yml`). Navigation menu items live separately in
`_data/navigation.yml`. Author sidebar fields (name, bio, employer, social links) live in `_config.yml`
under `author:`.

**Theme layer (`_layouts`, `_includes`, `_sass`) is upstream Minimal Mistakes/academicpages code.**
`_includes` has several "provider" sub-directories (`analytics-providers/`, `comments-providers/`) that
are switched between via config values (`analytics.provider`, `comments.provider`) rather than edited
directly. Several `_includes/*` names are directories with a `custom.html` override slot
(`_includes/head/custom.html`, `_includes/footer/custom.html`) — use these for site-specific
head/footer injections instead of editing the shared theme files. Styling is Sass under `_sass/`,
compiled by Jekyll's built-in Sass support (`sass:` block in `_config.yml`, compressed in prod).

**`markdown_generator/`** and **`talkmap.py`** are standalone one-off Python/Jupyter data-import tools,
not part of the Jekyll build — they generate the Markdown files that live in `_publications/`/`_talks/`
and the standalone Leaflet map under `talkmap/`, respectively.

**Static assets:** images in `images/`, downloadable files (PDFs etc.) in `files/` — anything placed in
`files/` is served at `https://yantosca.github.io/files/<name>`.
