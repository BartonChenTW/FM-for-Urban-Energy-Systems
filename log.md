# Change Log

Key changes to the knowledge base, newest first. Private file — excluded from the Jekyll site via `_config.yml`.

Record structural changes, content merges, renamed or moved pages, and decisions. Small typo fixes don't need an entry.

---

## 2026-09-13 (light/dark mode toggle)

Barton asked to enable light/dark mode. just-the-docs already ships both color schemes (`assets/css/just-the-docs-light.css`/`-dark.css`, `color_scheme: light|dark` in `_config.yml`) and a `jtd.setTheme(name)` runtime function, but no user-facing toggle button, no click handler, and no persistence across page loads.

Researched the theme's actual mechanism directly rather than assuming (this session had already gotten one Sass convention wrong earlier by assuming instead of checking): fetched the theme's own `assets/js/just-the-docs.js` source and confirmed `jtd.setTheme`/`jtd.getTheme` work by reading/rewriting the `href` of the page's first `[rel="stylesheet"]` link — there's no `data-theme` attribute or CSS custom-property switch involved. Also confirmed, by fetching `_includes/components/sidebar.html` and `components/footer.html` directly, that `nav_footer_custom.html` (the documented include point for this kind of control) renders **twice** on every page — once in the desktop sidebar, once in a `d-md-none` mobile-only footer copy present in the DOM even on desktop. Using `id="..."` there would have caused duplicate-ID bugs; built the toggle with classes and DOM-scoped `querySelector` instead, and guarded the click-listener registration with a `window` flag so the listener (whose script tag also renders twice) doesn't attach twice and double-toggle on click.

Added:
- `_includes/nav_footer_custom.html`: the toggle button (sun/moon SVG icons, inline, no external asset) plus its script — reads/writes `localStorage.theme`, calls `jtd.setTheme`, syncs both DOM copies of the button.
- `_includes/head_custom.html`: a new script block (added before the existing external-links-in-new-tab script already there) that re-applies a saved `localStorage.theme` preference by rewriting the stylesheet `href`, as early as this include runs, so a returning visitor's preference applies before paint rather than flashing the site's default light scheme first. Not perfectly flicker-free without forking the theme's own `head.html` (this include runs after the theme's stylesheet `<link>` tags, confirmed by fetching `head.html`) -- judged not worth it for this.

`_config.yml`'s `color_scheme: light` is unchanged and correct to leave as-is: it sets the build-time default for a first-time visitor; dark is a client-side, opt-in preference on top of that.

**Not verified in this environment** -- no Ruby/Jekyll/browser here, so this could not be built and clicked. What was verified: Liquid/JS bracket balance in both new files, and that the full existing site (footnotes, bib, lychee link check) still passes untouched. The real test is the next Pages build plus Barton clicking the button.

## 2026-09-12 (diagram critique + a quick correctness fix)

Barton flagged that the six chapter-landing Mermaid diagrams (added 2026-09-11) aren't very helpful. Added `diagram-ideas.md` (private, excluded from the build): a page-by-page critique — every one of the six is a flowchart of the table of contents (section-number boxes, "comes after" arrows), which duplicates the sidebar nav and the "In this chapter" table rather than showing anything the reader couldn't already see. Proposes concrete replacements per chapter (e.g. Chapter 4's landing diagram → the actual screening funnel/2×2 instead of a TOC; Chapter 5's → promote the bipartite-graph worked example already in §5.4). Flags §5.5's temporal-hierarchy diagram and §5.1's roadmap as the two that already work, as a model for what "good" looks like here.

While reviewing, found and fixed a real bug independent of the redesign question: `chapter-4-directions/index.md`'s diagram used wrong section numbers (`4.9 Screening`, `4.10 Candidate sub-fields`, `4.11 Methods`, `4.12 Building it`) — the actual numbering (confirmed against the page's own "In this chapter" table, right below the diagram) is §4.5–4.7 (screening), §4.8 (candidate sub-fields), §4.9/4.9.1–3 (methods/tiers), §4.10 (building it). Corrected.

Added a TODO item pointing at `diagram-ideas.md`, and excluded that file from the site build.

## 2026-09-11 (branch protection docs + site link)

Barton turned on branch protection for `main` (require PR before merging, require the `lychee` link-check status check, block force-push/deletion, no bypass even for the owner) via the GitHub UI — I don't have `gh` CLI access in this environment, so this was applied by Barton directly, not by me.

Updated docs to match the new workflow:
- `CONTRIBUTING.md`: new "How changes get in" section explaining the fork → branch → PR flow and that the link-check must pass; added a "Read the book" link at the top.
- `README.md`: added a prominent site link at the top and in the founder-attribution paragraph ("Contributions go through a pull request"); replaced the old placeholder ("once GitHub Pages is enabled... `https://<your-username>.github.io/...`") with the real live URL now that Pages is confirmed working; removed a redundant second copy of the site link; fixed the "Building locally" closing line, which still described Pages as not-yet-enabled.

Site URL used throughout: `https://bartonchentw.github.io/FM-for-Urban-Energy-Systems/` — superseded later the same day when the repo was renamed to `FM4UES`; the current URL is `https://bartonchentw.github.io/FM4UES/`.

## 2026-09-11 (attribution + leftover "Part" wording)

Added author/founder attribution at Barton's request, framed as an open, community-editable textbook rather than sole-authored: a credit line on `index.md` ("Started by Barton Chen — open for anyone to contribute", linking to the how-to-contribute page), a paragraph on `README.md`, and an opening-line credit on `CONTRIBUTING.md`. `LICENSE` already said "Barton Chen and contributors" — no change needed there.

While in these files, fixed leftover "Part" wording the previous rename pass missed (its regex only matched `Part <number>`, not bare/plural/lowercase uses): the `## In this part` heading on all six chapter `index.md` files, "this part surveys"/"this part is a case study" in the Chapter 4/5 landing pages, "the operational core of this part" in §4.9's landing page, the Contents table header on `index.md`, and "nested by Part"/"the Part's title" in `README.md`/`CONTRIBUTING.md`. Re-ran the case-insensitive sweep afterward — clean (remaining "part"/"parts" hits are all ordinary English, e.g. "part-load", "network of parts").

**AI-assistance disclosure added**, same three files: `index.md` (a small-print line under the founder credit), `README.md` (a short paragraph), `CONTRIBUTING.md` (a note after the founder-credit paragraph, plus a line that the sourcing standard applies equally to human- and AI-drafted contributions). Names both models actually used in this session, Claude Opus 5 and Claude Sonnet 5 (Anthropic) — the session switched from Opus to Sonnet partway via `/model sonnet`.

## 2026-09-11 (rename: Part → Chapter)

Renamed the top-level structure from "Part" to "Chapter" at Barton's request: directories `part-1-background/` … `part-6-outlook/` → `chapter-1-background/` … `chapter-6-outlook/`; every `title:`/`parent:`/`grand_parent:` front-matter value and every in-text "Part N" reference (breadcrumbs, cross-links, prose) updated to "Chapter N" across all 55 site pages, `index.md`, `README.md`, `CONTRIBUTING.md`, and `TODO.md`. `_config.yml` and `.github/lychee.toml` comments updated to match.

`notes-concept-paper.md`'s own internal "Part 1"/"Part 2" section labels were deliberately left alone — those are that private document's own structure, unrelated to the book's chapters. `log.md` and `outline.md` entries from before today were left as a historical record rather than rewritten.

Verified before committing: no remaining `part-N-`/`Part N` references outside the two intentionally-untouched files; every `parent:`/`grand_parent:` value matches its target index page's `title:` exactly; no broken internal `.html` links (re-ran the same link-resolution check used after the original restructure).

## 2026-09-11 (restructure)

**Full restructure into six Parts, one page per section**, implementing `outline.md` with the amendments agreed in `TODO.md`: split the outline's draft Part 4 into Part 4 (neutral survey of directions) / Part 5 (case study: multi-carrier energy hub FM) / Part 6 (outlook), broadened Part 4 with four new stub directions, and added ML-basics content to Part 2.

**New file layout** (just-the-docs nesting via `parent:` / `has_children:` / `grand_parent:`):

- `part-1-background/` (index + 6 sections, 1.1–1.6) — was `01-the-domain.md` plus new intro material.
- `part-2-fm-foundations/` (index + 12 sections, 2.1–2.8 with 2.4 having 5 sub-children 2.4.1–2.4.5) — was `02-fm-fundamentals.md`, `03-basic-elements.md`, `04-fm-landscape.md`, plus new ML-basics sections 2.6–2.8.
- `part-3-sim-opt/` (index + 8 sections, 3.1–3.8) — was `01-the-domain.md` §2–4, plus new material (3.2 building-simulation data, 3.3 energy-hub formalism, 3.4/3.5 dispatch and design framing, 3.7 schemas) drawn from `add/reference.md` §4–7.
- `part-4-directions/` (index + 13 sections, 4.1–4.10 with 4.9 having 3 sub-children 4.9.1–4.9.3) — was `05-screening.md`, `06/07/08-methods-tierN.md`, `09-building-it.md`, plus four new stub sections (4.1–4.4) and `add/FM_for_UES.md` §3–4 (screening/candidate sub-fields).
- `part-5-case-study/` (index + 8 sections, 5.1–5.8) — entirely new pages built from `add/FM_for_UES.md` §5, §6, §8.2–8.4, §9, §10 (roadmap, representation problem, concrete representation, token schema, physics loss, module decomposition, risks).
- `part-6-outlook/` (index + 2 sections, 6.1–6.2) — was `10-open-gaps.md`, plus a new "how to contribute" page.
- `appendices/` (index + A, B) — was `appendix-a-glossary.md`, `appendix-b-checklist.md`, internal links renumbered throughout.

**Deleted** (fully migrated, verified via a link/content audit before removal): `01-the-domain.md` through `10-open-gaps.md`, `11-references.md` (folded into per-page footnotes + `references/fm-for-ues.bib`; see decision below), `appendix-a-glossary.md`, `appendix-b-checklist.md`, `appendix-c-buildfm-bs2027.md` (moved to private notes, see below), and the entire `add/` directory (`add/FM_for_UES.md`, `add/reference.md`).

**Private notes file added**: `notes-concept-paper.md` (excluded from the site build via `_config.yml`), merging the former public `appendix-c-buildfm-bs2027.md` (the BS2027 applied example) with `add/FM_for_UES.md` §7 (concept-paper structure notes) — per the decision that project-specific submission strategy (venue choice, author-list-as-argument, double-blind handling) isn't public-textbook material, even though the reasoning is a useful internal reference.

**Dropped entirely**: `add/reference.md` §8 "Project resources & personal communication" (NEST facility entry and personal-communication citation) and §9 "Notes on using this list in a manuscript" (meta-content about citation practice, judged not worth carrying into the public book — the substance, e.g. arXiv-vs-venue-of-record citation practice, is already reflected in how footnotes were written).

**11-references.md decision**: folded entirely into per-page footnotes plus `references/fm-for-ues.bib`, then deleted, rather than kept as a slimmed "further reading" page. Rationale: with every claim now footnoted at point of use, a separate reference-pointers page would only duplicate the `.bib` (already the machine-readable source of truth) without adding reader value. Added `redirect_from: /11-references.html` on `references/README.md` as the closest surviving destination.

**References**: extended `references/fm-for-ues.bib` from ~16 to ~22 entries, adding confirmed-metadata entries from `add/reference.md` §5–6 (Geidl & Andersson energy-hub papers ×3, MATPOWER, PyPSA, PGLib-OPF, CESAR-P). Entries marked `[to confirm]` in the original source notes (e.g. TimeGPT, Granite TSPulse/FlowState, several `[to confirm]` author/institution fields) were not added, per the no-fabrication rule. Converted all inline claims across every new page to Markdown footnotes keyed to match `.bib` entries, per `CONTRIBUTING.md`'s convention; verified programmatically that every footnote key used in the text has a corresponding `[^key]:` definition, and that `.bib`/footnote key names agree (one mismatch found and fixed: `cesarp2022` → `orehounig2022cesarp`).

**Redirects**: added `redirect_from:` front matter for all 13 old public URLs (`01-the-domain.html` through `10-open-gaps.html`, `11-references.html`, `appendix-a-glossary.html`, `appendix-b-checklist.html`) pointing to wherever the bulk of that page's content landed. `appendix-c-buildfm-bs2027.html` has no redirect, since its content is now private (a redirect would point to a 404 on the built site).

**Diagrams**: enabled Mermaid via `mermaid: { version: "11.4.1" }` in `_config.yml`. Added diagrams to every Part landing page (1–6 minus 6, appendices — landing pages without a natural "flow" to show were left as lists), the Tier 1→2→3 progression page (§4.9), the roadmap Phase 0→5 flow (§5.1), and the token-schema temporal hierarchy (§5.5) — the two sections flagged in an earlier review as most needing a picture. Per-section illustration for the remaining ~45 pages is logged as open in `TODO.md`.

**`_config.yml`**: removed `add/` from `exclude:` (directory deleted); added `notes-concept-paper.md` to `exclude:`; added the `mermaid:` block.

**`index.md`** and **`README.md`**: rewritten tables of contents/structure tables to match the six-Part layout; version label bumped to "2.0" to mark the structural break from v1.1.

**`CONTRIBUTING.md`**: updated the glossary link and the front-matter guidance paragraph to describe the new `parent:`/`has_children:`/`status`/`last_reviewed` pattern.

**`.github/lychee.toml`**: broadened the internal-link exclusion regex from a bare-filename pattern (`^[a-zA-Z0-9_-]+\.html(#.*)?$`) to also match relative paths with slashes (`^(?:\.\./)*[a-zA-Z0-9_/-]+\.html(#[^\s)]*)?$`), since cross-Part links now routinely look like `../part-4-directions/4-9-1-methods-tier1.html`.

**Verification performed before considering the restructure complete**: (1) a script-based check that every internal `.html` link in every new page resolves to an actual `.md` file at the linked relative path — zero broken links; (2) a check that every `parent:` front-matter value matches an existing page's `title:` exactly — zero mismatches; (3) a check for duplicate page titles and duplicate `nav_order` values within the same parent group — zero collisions; (4) a check that every footnote key used in text has a matching `[^key]:` definition — zero missing; (5) manual cross-check of the outline's source-mapping table against the new file layout to confirm every old section landed somewhere.

## 2026-09-11

- Added private planning files, excluded from the site: `TODO.md` (task list), `outline.md` (proposed new textbook structure, for review), `log.md` (this file).
- `_config.yml`: added an `exclude:` list (`TODO.md`, `outline.md`, `log.md`, `Gemfile`, `Gemfile.lock`, `vendor/`).
- Added `add/FM_for_UES.md` and `add/reference.md`: working notes and references from an earlier conversation, to be merged into the textbook.
- Recorded the repo aim in `TODO.md`: a living knowledge base for UES people to learn about FMs; long-term goal to build an FM for UES.
- Added `LICENSE` (CC BY 4.0 for the written content).
- `_config.yml`: enabled `jekyll-redirect-from` (ready for use once the outline restructure renames pages); excluded `add/` from the build so the working notes and personal-communication references aren't reachable on the published site before merging.
- Added `CONTRIBUTING.md` and `.github/ISSUE_TEMPLATE/` (error report, reference suggestion, section proposal) to support outside contributions.
- Added `references/fm-for-ues.bib`: starter BibTeX bibliography (~16 entries) for Zotero import, seeded from confirmed-metadata entries in `add/reference.md` §1–4 and `11-references.md`. Citation keys follow `firstauthorYEARshortname`, matching the planned footnote-citation convention. Added `references/README.md` explaining import and how to contribute entries; excluded the `.bib` itself from the site build but kept the README as a page.
- Claude's setup suggestions from the prior session (LICENSE, redirects, CONTRIBUTING, `add/` exclusion, references folder) are now implemented; marked done in `TODO.md`. Still open: references workflow decision (hand-written footnotes vs. `jekyll-scholar` via GitHub Actions), and the outline restructure itself (blocked on Barton's review of `outline.md`).
- Added `_includes/page-status.html`: renders a "Status / Last reviewed" badge from page front matter. Added `status: draft` + `last_reviewed: 2026-09-10` (the v1.1 publish date) and the include call to all 14 chapter/appendix pages (skipped `index.md`, which already has a version/date label).
- Added `.github/workflows/link-check.yml` (lychee, on push/PR to main + weekly) and `.github/lychee.toml`. Internal `chapter-name.html` cross-links are excluded (Jekyll-rendered paths, not real files against raw `.md` source).
- **Found while setting up the link checker:** `add/reference.md` links to `inbox.md` (~20 times) and once to `FM_for_UES.md`, but `inbox.md` doesn't exist in the repo. Logged in `TODO.md`; not fixed yet since it's tied to the still-open `add/` merge decision.

## Before 2026-09-11

- `2a3938b` Published the v1.1 textbook as a Jekyll site (just-the-docs theme): Parts I–VII plus Appendices A–C.
