# Foundation Models for Urban Energy Systems — A Working Textbook

A working textbook on what gets simulated in urban energy systems, what could plausibly be
learned by a foundation model, and how to build it. Written for someone who knows urban
energy systems well and machine learning less well.

**Read it as a website:** once GitHub Pages is enabled for this repo (Settings → Pages →
Source: Deploy from a branch → `main` / root), it will be published at
`https://<your-username>.github.io/FM-for-Urban-Energy-Systems/`.

**Read it as Markdown:** every page is a plain `.md` file in this repo, starting at
[`index.md`](index.md).

## Structure

| File | Contents |
| :--- | :--- |
| `index.md` | Landing page and table of contents |
| `01-the-domain.md` | Scales, task taxonomy, tool landscape, where cost lives |
| `02-fm-fundamentals.md` | What makes a model a foundation model; the five design decisions |
| `03-basic-elements.md` | **The core argument** — a criterion for choosing a basic element, applied to buildings |
| `04-fm-landscape.md` | Time-series FMs, grid FMs, tabular FMs and the cell, what doesn't exist yet |
| `05-screening.md` | Which sub-domains pass the screen for FM treatment |
| `06-methods-tier1.md` | Single-hub dispatch: build path and baselines |
| `07-methods-tier2.md` | Multi-hub, multi-carrier: graph neural networks and neural operators |
| `08-methods-tier3.md` | Design and sizing: amortised optimisation, the decision-space problem |
| `09-building-it.md` | Data generation, physics enforcement, evaluation, budget realism |
| `10-open-gaps.md` | Nine open gaps, ordered by defensibility as research contributions |
| `appendix-a-glossary.md` | Plain-language definitions of every ML term used |
| `appendix-b-checklist.md` | Thirteen questions to ask before starting a project |
| `appendix-c-buildfm-bs2027.md` | An applied example — public, redacted |
| `11-references.md` | Full bibliography |

## Status

Version 1.1 — actively revised. Corrections and additions welcome via issue or pull request.

## Building locally (optional)

```bash
bundle install
bundle exec jekyll serve
```

Requires Ruby and Bundler. Not needed to publish — GitHub Pages builds this automatically
from the `main` branch once enabled in repo Settings.
