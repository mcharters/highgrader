# HIGH GRADER

Band site, built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages.

## Running locally

**One-time setup** (Windows):

1. Install [Ruby+Devkit](https://rubyinstaller.org/) (latest 3.x). Run `ridk install` at the end and pick option **3**.
2. From the repo root:
   ```bash
   gem install bundler
   bundle install
   ```

**Start the dev server:**

```bash
bundle exec jekyll serve --livereload
```

Then open <http://localhost:4000>. Edits to layouts, includes, and pages hot-reload automatically. Changes to `_config.yml` require a restart.

## Adding a page

Create an `.html` or `.md` file at the repo root with front matter:

```yaml
---
layout: default
title: Shows
permalink: /shows/
---
```

Then add a link in [_includes/nav.html](_includes/nav.html).

## Structure

- `_layouts/default.html` — shared `<head>`, CSS, starfield, nav
- `_includes/header.html` — emoji title art + NFB easter-egg script
- `_includes/nav.html` — site menu
- `assets/images/` — image files
- `index.html` — home page (minesweeper)
- `about.md` — band bio
