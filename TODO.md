# TODO

Private working list — excluded from the Jekyll site via `_config.yml`. Key changes are recorded in [log.md](log.md).

Items tagged **[Claude]** are suggestions from Claude (2026-09-11), not yet agreed. Untagged items are Barton's.

## Aim of the repo

- A living knowledge base that helps people in the urban energy systems (UES) domain learn about foundation models (FMs).
- Long-term goal: build an FM for UES.

## In progress

- [ ] 

## Next

- [ ] **Merge `add/` notes into the textbook.** `add/FM_for_UES.md` and `add/reference.md` hold material from an earlier conversation. Fold their content into the relevant chapter `.md` files. *(Blocked on agreeing the outline — see below — so content isn't moved twice.)*
- [ ] **Add detailed references with footnotes.** Many chapters have lots of text but few citations. Kramdown (Jekyll's Markdown engine) supports footnotes natively: `text[^key]` in the body, `[^key]: Author (Year). Title.` at the bottom of the page. They render as numbered superscripts with a back-linked list at the page end. Use the citation keys now in `references/fm-for-ues.bib` as footnote names.
- [x] **Create a `references/` folder for Zotero import.** Done 2026-09-11: [`references/fm-for-ues.bib`](references/fm-for-ues.bib) (starter set, ~16 entries seeded from `add/reference.md` §1–4 and `11-references.md`, limited to entries with confirmed metadata) plus [`references/README.md`](references/README.md) explaining import and how to add entries. Excluded the `.bib` from the site build; kept the README as a page.
- [ ] **Restructure the textbook into clearer layers.** Proposed chapters (draft in [outline.md](outline.md)):
  1. Background of UES and FMs
  2. Foundation knowledge of FMs
  3. Simulation / optimisation in UES
  4. Potential directions / options for FMs in UES
  5. Outlook
  - Map the existing chapters (01–11, appendices A–C) onto this structure. Some will merge, some become sub-pages (just-the-docs supports `parent:` / `has_children:` for nesting).
- [ ] **Add an illustration to every section.** Each section opens with a diagram or image showing what it covers. Options: Mermaid diagrams written inline in the Markdown (just-the-docs supports these once `mermaid:` is enabled in `_config.yml`), or SVG/PNG files stored in an `assets/images/` folder.

## Suggestions from Claude (2026-09-11) — to review

### Setup

- [x] **[Claude] Exclude `add/` from the site now.** Done 2026-09-11: added `add/` to `exclude:` in `_config.yml`.
- [ ] **[Claude] Decide the references workflow before writing footnotes.** `jekyll-scholar` (auto-build citations from a `.bib`) is not supported by the standard GitHub Pages build. Choose one:
  - (a) hand-written footnotes whose names match `.bib` citation keys — simple, but two copies to keep in sync;
  - (b) build the site with a GitHub Actions workflow so `jekyll-scholar` can run — more setup, single source of truth.
  - Either way: manage references in Zotero with the Better BibTeX plugin, which gives stable citation keys and auto-exports the `.bib`. Key convention `firstauthorYEARshortname` (e.g. `raissi2019physics`) already used in `references/fm-for-ues.bib` — confirm or change.
- [x] **[Claude] Add `jekyll-redirect-from` before renaming files.** Done 2026-09-11: added to `plugins:` in `_config.yml` (bundled via the `github-pages` gem already in the Gemfile, no Gemfile change needed). Not yet *used* — add `redirect_from:` front matter when pages are actually renamed in the restructure.
- [x] **[Claude] Add a LICENSE.** Done 2026-09-11: [`LICENSE`](LICENSE), CC BY 4.0 for the written content.
- [x] **[Claude] Add `CONTRIBUTING.md` and GitHub issue templates.** Done 2026-09-11: [`CONTRIBUTING.md`](CONTRIBUTING.md) plus three templates in `.github/ISSUE_TEMPLATE/` (error report, reference suggestion, section proposal).
- [x] **[Claude] Add a status / last-reviewed line to each page** (e.g. `status: draft | reviewed`, `last_reviewed: 2026-09-11` in front matter, displayed at the top), so readers can tell mature pages from rough ones. Done 2026-09-11: `_includes/page-status.html` renders the badge; added `status: draft` + `last_reviewed: 2026-09-10` (the v1.1 publish date, from git history) to front matter and the include call to all 14 chapter/appendix pages. Skipped `index.md` — it already shows a version/date label. Flip `status` to `reviewed` and bump `last_reviewed` per page as each is actually re-checked.
- [x] **[Claude] Add an automated link checker** (e.g. lychee or html-proofer in GitHub Actions). Reference-heavy pages collect broken links quickly. Done 2026-09-11: `.github/workflows/link-check.yml` (lychee, runs on push/PR to main + weekly cron), config in `.github/lychee.toml`. Chose lychee over html-proofer since it doesn't require building the Jekyll site first (no Ruby/remote-theme build step in CI). Internal `chapter-name.html` cross-links are excluded from the check (see comment in `lychee.toml`) since those are Jekyll-rendered paths that don't exist as literal files against the raw `.md` source — a real check of those would need to run against the *built* site instead.
  - **Found a real pre-existing broken link while setting this up:** `add/reference.md` links to `inbox.md` (~20 times, as the place to triage new references/abstracts) and to `FM_for_UES.md` in one spot — but `inbox.md` does not exist anywhere in the repo. Either create a stub `inbox.md`, or update those links/instructions once `add/reference.md` is merged into the real reference workflow. Not fixed here since it's a content decision tied to the still-open `add/` merge.

### Outline

- [ ] **[Claude] Separate the neutral survey from the research proposal.** Outline §4.4–4.6 and §5.2–5.3 describe one specific programme (the multi-carrier hub FM); a knowledge base loses credibility when readers can't tell "what the field knows" from "what we propose". Suggested split:
  - Part 4 — Directions: broader, neutral survey.
  - Part 5 — Case study: an FM for multi-carrier energy hubs (representation, token schema, modules, roadmap, risks).
  - Part 6 — Outlook: open gaps, how to contribute.
- [ ] **[Claude] Broaden Part 4 (Directions).** Currently missing:
  - using existing FMs off the shelf, e.g. zero-shot load forecasting with Chronos / TimesFM (most useful to practitioners today);
  - FMs for whole building stocks;
  - LLMs and agents that build or run simulation models (gap G7 already assumes this);
  - generative design.
- [ ] **[Claude] Add ML basics to Part 2** for readers from the energy side: self-supervised pretraining, fine-tuning, scaling laws; transformers, graph neural networks, neural operators (all used later in the book).
- [ ] **[Claude] Add a "surrogate models vs FMs" section to Part 2.** UES readers already know surrogates; the contrast is the best way in, and explains why an FM is more than a bigger surrogate.
- [ ] **[Claude] Frame Part 3 as "UES through an ML lens", not a domain tutorial:** what's learnable, data shapes, inputs/outputs, where the cost is.
- [ ] **[Claude] Add a dedicated data and benchmarks section to Part 3** (BDG2, ResStock/ComStock, BuildingsBench, weather data, etc.), currently scattered.
- [ ] **[Claude] Resolve the overlap between outline §2.3 (basic elements) and §4.4 (representation problem):** merge, or make §2.3 the general concept and §4.4 its application.
- [ ] **[Claude] Phase the illustrations.** One per section is ~40 diagrams. Start with one per Part plus sections where a picture explains a mechanism (token schema, tier progression), then fill in.

### Suggested order of work

- [ ] **[Claude] Do the items above in dependency order** to avoid moving content twice:
  1. Exclude `add/` from the site
  2. Agree the outline (answer the decisions at the end of [outline.md](outline.md))
  3. Add redirects, then restructure the files
  4. Merge `add/` content into the new structure
  5. Decide the references workflow, then add footnotes and the `.bib`
  6. Add diagrams

## Later / ideas

- [ ] 

## Done

- [x] Publish v1.1 textbook as Jekyll site (just-the-docs)
- [x] Create `TODO.md`, `outline.md` and `log.md` as private planning files
