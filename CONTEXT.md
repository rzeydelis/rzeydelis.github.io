# Project Context

## Overview

This repository powers a personal website at `www.robertzeydelis.com` using Jekyll (based on the Beautiful Jekyll theme).

Current homepage intent:
- short personal intro
- "Fun Projects" list
- optional blog feed (rendered only if posts exist)

## Stack

- Static site generator: Jekyll
- Theme base: Beautiful Jekyll (customized locally)
- Ruby dependencies managed with Bundler
- Core gems from `Gemfile`:
  - `github-pages` (`197`)
  - `jekyll-paginate`
- Frontend:
  - Bootstrap
  - jQuery
  - custom CSS in `css/main.css`
  - custom JS in `js/main.js`

## Key Files And Directories

- `_config.yml`: site-wide configuration (colors, socials, analytics, pagination, plugins)
- `index.html`: homepage content (intro + projects + post listing loop)
- `css/main.css`: global styling plus homepage-specific classes (`.home-*`)
- `js/main.js`: navbar behavior and optional rotating header image logic
- `_layouts/`: page layout templates
  - `base.html` composes head/nav/footer and shared assets
  - `default.html` wraps normal page content
- `_includes/`: reusable partials (`head.html`, `nav.html`, `footer.html`, analytics includes)
- `_data/`: data files used by templates (for example social network metadata)
- `img/`: static image assets
- `travel_journal/index.html`: standalone simple page
- `CNAME`: custom domain (`www.robertzeydelis.com`)
- `staticman.yml`: Staticman comment config

## Content Model

- Pages are mostly root-level `.html` / `.md` files with front matter.
- Posts would normally live in `_posts/` and are paginated on the homepage.
- Current repo snapshot has no `_posts/` directory, so the "Latest Posts" section is effectively inactive until posts are added.

## Build And Run

Local Ruby flow:

```powershell
bundle install
bundle exec jekyll serve
```

Site is served locally at `http://127.0.0.1:4000` by default.

Docker flow (from `Dockerfile`):

```powershell
docker build -t beautiful-jekyll .
docker run -d -p 4000:4000 --name beautiful-jekyll -v "${PWD}:/srv/jekyll" beautiful-jekyll
```

## Deployment And Hosting

- Intended for GitHub Pages deployment (via `github-pages` gem and standard Jekyll layout conventions).
- Custom domain is set with `CNAME`.
- `_config.yml` excludes local/dev files from production output.

## Project-Specific Editing Notes

- This repo still contains upstream Beautiful Jekyll docs (`README.md`, `CHANGELOG.md`), but site behavior should be inferred from local files first.
- Homepage structure is intentionally customized in `index.html` and matching `.home-*` styles in `css/main.css`.
- `head.html` includes analytics snippets; preserve this unless tracking is intentionally changed.
- There is currently an untracked `_preview_shot/` directory used for local preview assets.

## Useful Sanity Checks After Changes

```powershell
bundle exec jekyll build
```

Then verify:
- homepage layout on desktop/mobile
- navbar collapse behavior
- footer links/social icons
- custom domain and metadata still render correctly
