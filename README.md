# CSU Advanced Utilities — Data Governance Hub

The governance hub for the **Command Center** meter-data program. It documents how the data
is governed — scope, lifecycle, quality (VEE / M2T), security, lineage, stewardship, and
KPIs. The live **Data Dictionary** and **Code Catalog** live in the separate
[`command-center-data-catalog`](https://github.com/csu-advanced-utilities-tech/command-center-data-catalog)
repo and are linked from the site navigation.

**Live site:** https://csu-advanced-utilities-tech.github.io/data-governance/

## How it's built

A [Jekyll](https://jekyllrb.com/) static site served by GitHub Pages from the [`docs/`](docs/)
folder. There is **no build step to edit content** — push Markdown and Pages rebuilds.

```
docs/
├─ _config.yml            # Jekyll config (baseurl = /data-governance)
├─ _data/nav.yml          # left-sidebar navigation (edit to add/reorder sections)
├─ _layouts/default.html  # shared layout: top bar, sidebar nav, Mermaid support
├─ assets/styles.css      # styling (matches the data-catalog site)
├─ index.md               # landing page with section cards
└─ NN-section-name.md     # one Markdown file per section
references/                # source PDFs / links (EPA, DOE, NREL, …)
```

## How to contribute

1. Edit the relevant `docs/NN-*.md` file (or add a new one and list it in `docs/_data/nav.yml`).
2. Update the status badge at the top: `placeholder` → `draft` → `review` → `approved`.
3. Replace `_TODO_` markers with real content; keep the **Source references** section accurate.
4. Open a pull request to `main`. On merge, GitHub Pages redeploys automatically.

### Authoring notes
- Diagrams use Mermaid — put them in ` ```mermaid ` fenced blocks (see *Architecture & Lineage*).
- Convert relative dates to absolute dates.
- Cross-link sections with `{% raw %}{{ '/NN-target.html' | relative_url }}{% endraw %}`.

## Local preview (optional)

```bash
cd docs
bundle exec jekyll serve   # requires Ruby + the github-pages gem
```

## Sources

See [`references/`](references/) for the EPA / DOE / NREL guidance this hub draws on.
