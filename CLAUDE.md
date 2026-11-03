# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

`yantosca.github.io` — Bob Yantosca's personal academic website, built on the **academicpages** Jekyll
template (a fork of the **Minimal Mistakes** theme), hosted via GitHub Pages. Content (CV, publications,
teaching, videos, blog posts) lives as Markdown/YAML front matter in collection folders; the
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
`_config.yml` is not hot-reloaded, so restart the server after editing it. (The README's `jekyll liveserve`
comes from the `hawkins` gem.) There are no automated tests, linters, or CI in this repo — verification is "does the site build and
does the page look right in a browser".

Front-end asset build (rarely needed — only if editing `assets/js/_main.js` or vendor JS):
```bash
npm install
npm run build:js     # runs uglify to regenerate assets/js/main.min.js from assets/js/_main.js + vendor plugins
npm run watch:js      # rebuild main.min.js on change
```

Publication markdown generation (one-off data import helpers, not part of the normal build):
```bash
cd markdown_generator
python pubsFromBib.py     # or run the .ipynb equivalents (PubsFromBib.ipynb, publications.ipynb)
```
These read a `.bib`/`.tsv` file and emit one Markdown file per entry into `_publications/`. The
`talks.py`/`talks.ipynb` halves target a `_talks/` folder that does not exist here. `markdown_generator/`
is excluded from the build in `_config.yml`, so nothing in it is published.

## Architecture

**Jekyll collections are the primary content model.** Each top-level content type is its own collection,
configured in `_config.yml` under `collections:` with matching `defaults:` blocks that set its layout:

| Collection | Folder | Layout | Notes |
|---|---|---|---|
| pages | `_pages/` | `single` | CV, About, Projects, Publications index, Teaching, Personal, etc. |
| posts | `_posts/` | `single` | Blog entries, dated filenames |
| publications | `_publications/` | `single` | One file per paper, `output: true` |
| teaching | `_teaching/` | `single` | |
| videos | `_videos/` | `video` | |

There is no `_projects/` folder and no `projects` collection; the Projects page is just `_pages/projects.md`.
The `talks` and `projects` collection declarations, the `/talks/` and `/talkmap.html` pages and the
`talkmap/` tooling were all removed — they were empty academicpages scaffolding.

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

**`markdown_generator/`** holds standalone one-off Python/Jupyter data-import tools that generate the
Markdown files in `_publications/`. They are not part of the Jekyll build and are excluded from it.

**Static assets:** images in `images/`, downloadable files (PDFs etc.) in `files/` — anything placed in
`files/` is served at `https://yantosca.github.io/files/<name>`. `files/` is currently absent because it
held only the template's placeholder PDFs; recreate it and drop files in, `_config.yml` still includes it.

## Working-tree notes

- `_sass/custom.scss`, `_sass/custom.scss.~1~`, `_sass/custom.scss.~2~` and `assets/css/was.main.scss` are untracked
  work in progress or backups, and `assets/css/main.scss` does not import `custom`. Don't delete or commit them without asking.
- `CHANGELOG.md` and `package.json` come from upstream Minimal Mistakes; they are not this site's history.
- `_pages/cv.md` is edited by hand and updated often.
- `_includes/seo.html` diverges from upstream academicpages by one line: the `{% if page.title %}`
  guard on line 9 is `{% if page.title and page.title != site.title %}`. Without it the home page,
  whose own title matches `site.title` ("Bob Yantosca"), renders `<title>Bob Yantosca - Bob Yantosca</title>`.
  There is no `custom.html` override slot for `seo.html`, so re-apply this if the theme is ever updated.
- Commit messages are short imperative sentences, e.g. "Add QFYAML to projects page".
