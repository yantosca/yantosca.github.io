# Contributing

This repository holds the source for [yantosca.github.io](https://yantosca.github.io),
Bob Yantosca's personal academic website. It is a personal site rather than a
community project, so it does not take feature contributions.

Corrections are welcome, though. If you spot a factual error — a wrong citation,
a broken link, a misattributed paper, a typo — please
[open an issue](https://github.com/yantosca/yantosca.github.io/issues) describing
what is wrong and, where it helps, what it should say instead. A DOI or other
source for the correct value is always appreciated.

Small, self-contained pull requests that fix such an error are also fine. Please
keep each one to a single fix and say in the description what evidence it is
based on.

## Building locally

The site is a [Jekyll](https://jekyllrb.com) build hosted on GitHub Pages:

```bash
bundle install
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

That serves the site at <http://localhost:4000> with analytics disabled and
expanded CSS. `_config.yml` is not reloaded while the server runs, so restart
after editing it.

Content lives as Markdown with YAML front matter in the collection folders
(`_pages/`, `_posts/`, `_publications/`, `_teaching/`, `_videos/`). Adding
something almost always means adding a file that follows the pattern of the
existing files in that folder, not changing the theme.

## Upstream

The theme is a fork of [academicpages](https://github.com/academicpages/academicpages.github.io),
which is itself a fork of
[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes). Issues with
the theme itself are better reported to those projects. `CHANGELOG.md` comes
from Minimal Mistakes upstream and is not this site's history.
