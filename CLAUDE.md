# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

```bash
# Install dependencies
bundle install

# Local development server with live reload (available at localhost:4000)
bundle exec jekyll serve -l -H localhost

# One-time build to _site/
bundle exec jekyll build
```

## Architecture Overview

This is a Jekyll static site built on the [Academic Pages](https://academicpages.github.io/) template (forked from Minimal Mistakes). It is deployed via GitHub Pages.

**Content is split across collections and pages:**

- `_pages/` — standalone pages included via `_config.yml`'s `include` list. `about.md` serves as the homepage (`permalink: /`). `publications.md` is the main research page and is **manually maintained** (not auto-generated).
- `_publications/`, `_talks/`, `_teaching/`, `_portfolio/` — Jekyll collections; each file becomes a page. Front matter fields (title, date, venue, paperurl, etc.) drive how content renders.
- `_posts/` — standard Jekyll blog posts (currently unused in nav).
- `files/` — static PDFs (CV, papers, slides) served at `/files/filename`.
- `images/` — static images.

**Configuration files that control site behavior:**

- `_config.yml` — author info, social links, collection definitions, plugin list, and per-collection layout defaults. Changes here require restarting the dev server.
- `_data/navigation.yml` — controls which links appear in the header nav (several sections are commented out).
- `_data/ui-text.yml` — UI string overrides.

**Templates:**

- `_layouts/` — page layouts (`single` for most content, `archive` for index pages, `talk` for talks).
- `_includes/` — reusable partials (sidebar, author profile, SEO, analytics, etc.).
- `_sass/` — SCSS partials; compiled from `_sass/_variables.scss` for theming.

**Markdown generation tools** (`markdown_generator/`): Python scripts and Jupyter notebooks that generate `_publications/*.md` or `_talks/*.md` from TSV files (`publications.tsv`, `talks.tsv`). Run `publications.py` or `talks.py` to regenerate those markdown files after editing the TSV. Alternatively, `pubsFromBib.py` / `PubsFromBib.ipynb` generates from BibTeX.

**`_site/`** is the generated output directory — never edit files there directly.

## Adding Content

- **New publication**: add a `.md` file in `_publications/` with front matter fields `title`, `collection: publications`, `category` (books/manuscripts/conferences), `date`, `venue`, `paperurl`, `citation`, and `excerpt`. Or edit `publications.tsv` and run `markdown_generator/publications.py`.
- **CV update**: replace `files/Song_Chloe_CV.pdf`.
- **Enable a nav section**: uncomment the relevant entry in `_data/navigation.yml` and ensure the corresponding page/collection exists.
- **Author sidebar**: edit the `author:` block in `_config.yml`.
