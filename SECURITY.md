# Security Policy

This repository contains the source for [yantosca.github.io](https://yantosca.github.io), a personal
academic website built with Jekyll and hosted on GitHub Pages. It is a static site with no server-side
code, database, authentication, or user data collection beyond optional third-party analytics/comments
configured in `_config.yml`.

## Supported Versions

This site tracks a single `main` branch, which is deployed directly by GitHub Pages. There are no
maintained older versions — only the latest commit on `main` is in service.

## Reporting a Vulnerability

If you discover a security issue with this site (e.g. a vulnerable dependency in `Gemfile`/`Gemfile.lock`
or `package.json`, an XSS vector in the templates, or a misconfiguration exposing sensitive data), please
report it privately rather than opening a public issue:

- Email: yantosca@seas.harvard.edu

Please include a description of the issue, the affected file(s)/URL, and steps to reproduce if
applicable. I'll acknowledge reports as soon as possible and push a fix or mitigation.

## Dependency Notes

- Ruby gem versions are pinned via `Gemfile.lock`. If GitHub flags a vulnerability in a transitive
  dependency of `github-pages`, the usual fix is to delete `Gemfile.lock` and run `bundle install` to
  regenerate it against the latest allowed versions.
- Front-end vendor libraries (jQuery and plugins under `assets/js/vendor/`, `assets/js/plugins/`) are
  bundled from the upstream Minimal Mistakes theme; updates should come from upstream rather than ad hoc
  patching.
