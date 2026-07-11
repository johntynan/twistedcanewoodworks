# Copilot / AI Agent Instructions — twistedcanewoodworks.github.io

Purpose: quick orientation for AI coding agents working on this Jekyll-based personal site.

- **Big picture**: This repository is a static Jekyll site published to GitHub Pages. Content lives as Markdown and HTML includes; the site uses the `jekyll-theme-tactile` theme specified in `_config.yml`.

- **Where to look (key files & folders)**:
  - Site config: [_config.yml](../_config.yml)
  - Page templates/includes: [_includes/header.html](../_includes/header.html), [_includes/footer.html](../_includes/footer.html), [_includes/default.html](../_includes/default.html)
  - Content pages: top-level Markdown files (e.g. [about.md](../about.md), [index.md](../index.md))
  - Blog posts: all posts live under `/_posts/` and use Jekyll front matter; example: [_posts/2025-12-20-ASAP-Choir-Performance.md](../_posts/2025-12-20-ASAP-Choir-Performance.md)
  - Static assets: `stylesheets/`, `javascripts/`, `images/`
  - CI/deploy workflow: [.github/workflows/static.yml](./workflows/static.yml) — pushes to `master` trigger Pages deployment.

- **Architecture & data flow**:
  - Markdown + Liquid templates -> Jekyll build -> static HTML served by GitHub Pages. Includes are stitched via Liquid `{% include %}` calls in `_includes/*`.
  - Assets referenced with site-root-relative paths (e.g. `stylesheets/stylesheet.css` in header include). Keep paths as-is.

- **Project-specific conventions**:
  - Posts must be placed in `/_posts/` with a `YYYY-MM-DD-title.md` filename and YAML front matter (`title`, `date`). Follow the date format seen in existing posts.
  - Use the existing include fragments rather than creating new top-level HTML templates when adding common header/footer behavior.
  - CSS and JS live under `stylesheets/` and `javascripts/` and are linked directly from `_includes/header.html` — avoid changing linking conventions unless intentionally altering site structure.

- **Build / preview / deploy**:
  - Production deploys via GitHub Actions: see [.github/workflows/static.yml](./workflows/static.yml). The workflow uploads the whole repo and deploys via Pages on pushes to the `master` branch.
  - Local preview: there is no Gemfile or bundler setup in the repo. To preview locally, install Jekyll and run from the repo root:

    ```bash
    gem install jekyll bundler
    jekyll serve
    ```

    If you add a `Gemfile` or choose to pin dependencies, prefer `bundle exec jekyll serve`.

- **Testing & debugging**:
  - There are no automated tests. Validate changes by running a local `jekyll serve` preview and by checking the GitHub Actions run after pushing.
  - CI logs are available in the repository Actions tab; the workflow is minimal and fails most often due to branch mismatch or large artifacts.

- **Integration points & external dependencies**:
  - Theme: `jekyll-theme-tactile` from `_config.yml` (no theme files are included here). GitHub Pages will apply the theme at build time.
  - External fonts loaded from Google Fonts in `_includes/header.html`.
  - Deployment uses built-in GitHub Pages + Actions (no external hosting).

- **Safe edits & common tasks (examples)**:
  - Add a new post: create `/_posts/YYYY-MM-DD-your-title.md` with front matter and Markdown body (see [_posts/2025-12-20-ASAP-Choir-Performance.md](../_posts/2025-12-20-ASAP-Choir-Performance.md)).
  - Update site title/description: edit `_config.yml`.
  - Add an image: put the file in `images/` and reference it from Markdown with `/images/your.png`.

- **Do not change without verification**:
  - `_includes/header.html` and `_includes/footer.html` control global layout; any change affects all pages. Preview locally before pushing.
  - The GitHub Actions workflow expects pushes to `master`. If the repository default branch is renamed, update `.github/workflows/static.yml` accordingly.

- **Notes for AI agents**:
  - Prefer minimal, surgical changes. Keep file and URL paths stable.
  - When adding functionality (new JS/CSS), follow existing naming and placement conventions (`javascripts/` and `stylesheets/`).
  - If you modify deploy or build behavior, document the changes in `README.md` and update the workflow.

If anything above is unclear or you'd like examples expanded (e.g., a local `Gemfile` + `bundle` setup), tell me which section to expand and I'll iterate.
