# Change Log

Key changes to the knowledge base, oldest first (new entries go at the bottom). Private file — excluded from the Jekyll site via `_config.yml`.

Record structural changes, content merges, renamed or moved pages, and decisions. Small typo fixes don't need an entry.

---

## Before 2026-09-11

- `2a3938b` Published the v1.1 textbook as a Jekyll site (just-the-docs theme): Parts I–VII plus Appendices A–C.

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

## 2026-09-11 (rename: Part → Chapter)

Renamed the top-level structure from "Part" to "Chapter" at Barton's request: directories `part-1-background/` … `part-6-outlook/` → `chapter-1-background/` … `chapter-6-outlook/`; every `title:`/`parent:`/`grand_parent:` front-matter value and every in-text "Part N" reference (breadcrumbs, cross-links, prose) updated to "Chapter N" across all 55 site pages, `index.md`, `README.md`, `CONTRIBUTING.md`, and `TODO.md`. `_config.yml` and `.github/lychee.toml` comments updated to match.

`notes-concept-paper.md`'s own internal "Part 1"/"Part 2" section labels were deliberately left alone — those are that private document's own structure, unrelated to the book's chapters. `log.md` and `outline.md` entries from before today were left as a historical record rather than rewritten.

Verified before committing: no remaining `part-N-`/`Part N` references outside the two intentionally-untouched files; every `parent:`/`grand_parent:` value matches its target index page's `title:` exactly; no broken internal `.html` links (re-ran the same link-resolution check used after the original restructure).

## 2026-09-11 (attribution + leftover "Part" wording)

Added author/founder attribution at Barton's request, framed as an open, community-editable textbook rather than sole-authored: a credit line on `index.md` ("Started by Barton Chen — open for anyone to contribute", linking to the how-to-contribute page), a paragraph on `README.md`, and an opening-line credit on `CONTRIBUTING.md`. `LICENSE` already said "Barton Chen and contributors" — no change needed there.

While in these files, fixed leftover "Part" wording the previous rename pass missed (its regex only matched `Part <number>`, not bare/plural/lowercase uses): the `## In this part` heading on all six chapter `index.md` files, "this part surveys"/"this part is a case study" in the Chapter 4/5 landing pages, "the operational core of this part" in §4.9's landing page, the Contents table header on `index.md`, and "nested by Part"/"the Part's title" in `README.md`/`CONTRIBUTING.md`. Re-ran the case-insensitive sweep afterward — clean (remaining "part"/"parts" hits are all ordinary English, e.g. "part-load", "network of parts").

**AI-assistance disclosure added**, same three files: `index.md` (a small-print line under the founder credit), `README.md` (a short paragraph), `CONTRIBUTING.md` (a note after the founder-credit paragraph, plus a line that the sourcing standard applies equally to human- and AI-drafted contributions). Names both models actually used in this session, Claude Opus 5 and Claude Sonnet 5 (Anthropic) — the session switched from Opus to Sonnet partway via `/model sonnet`.

## 2026-09-11 (branch protection docs + site link)

Barton turned on branch protection for `main` (require PR before merging, require the `lychee` link-check status check, block force-push/deletion, no bypass even for the owner) via the GitHub UI — I don't have `gh` CLI access in this environment, so this was applied by Barton directly, not by me.

Updated docs to match the new workflow:
- `CONTRIBUTING.md`: new "How changes get in" section explaining the fork → branch → PR flow and that the link-check must pass; added a "Read the book" link at the top.
- `README.md`: added a prominent site link at the top and in the founder-attribution paragraph ("Contributions go through a pull request"); replaced the old placeholder ("once GitHub Pages is enabled... `https://<your-username>.github.io/...`") with the real live URL now that Pages is confirmed working; removed a redundant second copy of the site link; fixed the "Building locally" closing line, which still described Pages as not-yet-enabled.

Site URL used throughout: `https://bartonchentw.github.io/FM-for-Urban-Energy-Systems/` — superseded later the same day when the repo was renamed to `FM4UES`; the current URL is `https://bartonchentw.github.io/FM4UES/`.

## 2026-09-12 (diagram critique + a quick correctness fix)

Barton flagged that the six chapter-landing Mermaid diagrams (added 2026-09-11) aren't very helpful. Added `diagram-ideas.md` (private, excluded from the build): a page-by-page critique — every one of the six is a flowchart of the table of contents (section-number boxes, "comes after" arrows), which duplicates the sidebar nav and the "In this chapter" table rather than showing anything the reader couldn't already see. Proposes concrete replacements per chapter (e.g. Chapter 4's landing diagram → the actual screening funnel/2×2 instead of a TOC; Chapter 5's → promote the bipartite-graph worked example already in §5.4). Flags §5.5's temporal-hierarchy diagram and §5.1's roadmap as the two that already work, as a model for what "good" looks like here.

While reviewing, found and fixed a real bug independent of the redesign question: `chapter-4-directions/index.md`'s diagram used wrong section numbers (`4.9 Screening`, `4.10 Candidate sub-fields`, `4.11 Methods`, `4.12 Building it`) — the actual numbering (confirmed against the page's own "In this chapter" table, right below the diagram) is §4.5–4.7 (screening), §4.8 (candidate sub-fields), §4.9/4.9.1–3 (methods/tiers), §4.10 (building it). Corrected.

Added a TODO item pointing at `diagram-ideas.md`, and excluded that file from the site build.

## 2026-09-13 (light/dark mode toggle)

Barton asked to enable light/dark mode. just-the-docs already ships both color schemes (`assets/css/just-the-docs-light.css`/`-dark.css`, `color_scheme: light|dark` in `_config.yml`) and a `jtd.setTheme(name)` runtime function, but no user-facing toggle button, no click handler, and no persistence across page loads.

Researched the theme's actual mechanism directly rather than assuming (this session had already gotten one Sass convention wrong earlier by assuming instead of checking): fetched the theme's own `assets/js/just-the-docs.js` source and confirmed `jtd.setTheme`/`jtd.getTheme` work by reading/rewriting the `href` of the page's first `[rel="stylesheet"]` link — there's no `data-theme` attribute or CSS custom-property switch involved. Also confirmed, by fetching `_includes/components/sidebar.html` and `components/footer.html` directly, that `nav_footer_custom.html` (the documented include point for this kind of control) renders **twice** on every page — once in the desktop sidebar, once in a `d-md-none` mobile-only footer copy present in the DOM even on desktop. Using `id="..."` there would have caused duplicate-ID bugs; built the toggle with classes and DOM-scoped `querySelector` instead, and guarded the click-listener registration with a `window` flag so the listener (whose script tag also renders twice) doesn't attach twice and double-toggle on click.

Added:
- `_includes/nav_footer_custom.html`: the toggle button (sun/moon SVG icons, inline, no external asset) plus its script — reads/writes `localStorage.theme`, calls `jtd.setTheme`, syncs both DOM copies of the button.
- `_includes/head_custom.html`: a new script block (added before the existing external-links-in-new-tab script already there) that re-applies a saved `localStorage.theme` preference by rewriting the stylesheet `href`, as early as this include runs, so a returning visitor's preference applies before paint rather than flashing the site's default light scheme first. Not perfectly flicker-free without forking the theme's own `head.html` (this include runs after the theme's stylesheet `<link>` tags, confirmed by fetching `head.html`) -- judged not worth it for this.

`_config.yml`'s `color_scheme: light` is unchanged and correct to leave as-is: it sets the build-time default for a first-time visitor; dark is a client-side, opt-in preference on top of that.

**Not verified in this environment** -- no Ruby/Jekyll/browser here, so this could not be built and clicked. What was verified: Liquid/JS bracket balance in both new files, and that the full existing site (footnotes, bib, lychee link check) still passes untouched. The real test is the next Pages build plus Barton clicking the button.

## 2026-09-13 (new §2.9: UES-FM evaluation criteria)

Barton shared a draft (originally from ChatGPT) proposing seven evaluation dimensions for judging UES-specific foundation-model claims — generality, transferability, task generality, physical consistency, data efficiency, uncertainty awareness, computational benefit — plus a benchmark table and a proposed alternative FM definition, and asked whether/where it fits.

Assessment: the seven-dimension framework fills a real gap (§2.1 defines what an FM *is* generically; nothing previously said how to judge whether a *UES* FM proposal is good specifically), but the draft as supplied couldn't go in directly:
- Two of its five references ([2], [4]) were cited with no author list, which this book's own sourcing standard treats as unverified.
- It restated the §2.1 definition and proposed a second, competing "working definition" — redundant with, and in tension with, the one already in the book.
- It assumed a direct line to "the case study in Chapter 5" that didn't exist yet.

Verified all five references before using any of them (Crossref API for the four DOI-based ones, arXiv/search for the specific claims attributed to each):
- Reference [2] ("Foundation models for the electric power grid", Joule 8(12):3245-3258) is exactly the paper already in this book's bib as `hamann2024foundation` -- reused that key rather than adding a duplicate.
- [1] Bommasani et al. 2021 -- already cited in this book (§1.3, §2.1).
- [3] Karniadakis et al. 2021, "Physics-informed machine learning", *Nature Reviews Physics* 3(6):422-440 -- real, confirmed via Crossref.
- [4] Ma, Jiang, Hu & Chen (2025), "A review of physics-informed machine learning for building energy modeling", *Applied Energy* 381:125169 -- real, confirmed via Crossref; also independently verified the specific "physics-informed inputs/loss functions/architectural design/ensemble models" fourfold taxonomy is genuinely this paper's own categorisation (not [3]'s), via a direct search of its abstract, and attributed it correctly to [4] alone rather than to both papers jointly as the draft implied.
- [5] Xu, Hu, Atamturktur, Chen & Wang (2025), "Systematic review on uncertainty quantification in machine learning-based building energy modeling", *Renewable and Sustainable Energy Reviews* 218:115817 -- real, confirmed via Crossref; the "aleatoric and epistemic uncertainty" claim and the "three primary sources: building operations, simulation tools, ML model" detail both independently confirmed via search of the paper's actual findings.

Added, on branch `docs/ues-fm-evaluation-criteria`:
- `chapter-2-fm-foundations/2-9-ues-fm-evaluation-criteria.md`: the seven dimensions, trimmed from the original draft -- no restated FM definition (already in §2.1), no duplicate surrogate/FM contrast (already in §2.8, cross-referenced instead), framed as sharpening the existing definition rather than replacing it. Cross-links out to where this book already touches each dimension (§5.6 physics loss, §3.2 data scarcity, §2.8/§3.4/§3.5 amortisation, Chapter 6 G4 benchmarks gap).
- `chapter-5-case-study/5-8-risks.md` §5.8.3: a new sub-section applying the seven dimensions honestly to this book's own case study -- a table stating plainly which dimensions are demonstrated (none), designed-for-but-undemonstrated (generality, task generality), concretely addressed as a design target (physical consistency, computational benefit), or genuinely unaddressed (data efficiency, uncertainty awareness). This is the "bridge to Chapter 5" the original draft claimed but didn't yet have, since Chapter 5 didn't reference the framework before this change.
- 3 new `.bib` entries (`karniadakis2021piml`, `ma2025piml_bem`, `xu2025uq_bem`); reused `hamann2024foundation` and `bommasani2021opportunities` rather than duplicating.
- Updated `chapter-2-fm-foundations/index.md` (TOC table + diagram) and `2-8-surrogates-vs-fms.md`'s footer nav link for the new §2.9.

Dropped from the original draft: the restated Bommasani definition, the proposed second "working definition" blockquote, and the generic benchmark table (replaced with one specific to this book's actual case study rather than a hypothetical generic one).

Verified locally: footnote ref/def integrity clean site-wide, 77 bib entries (74 -> 77), no duplicate keys, brace-balanced. 0 link-check errors, 127 OK.

## 2026-09-13 (switched log.md to append-at-bottom, oldest-first)

Barton asked why merge conflicts kept recurring across the several parallel branches in flight. Root cause: `log.md` was newest-first, so every branch inserted its new entry at the same "top of file" location. Two branches doing that from the same starting version is a guaranteed textual conflict — Git cannot tell which entry should come first — even though the entries never actually overlap in content. It was not caused by starting a new task before the previous branch merged; it was this file's ordering colliding with working on several branches at once.

Reordered to oldest-first, with new entries appended at the bottom. Two branches appending at the end of a file merge cleanly far more often, since Git only conflicts where both sides touch the same lines, and an append touches only the tail. Updated the file's own intro line to state the convention, so future entries (mine or a contributor's) go to the right place.

Pure reordering — no entry content removed or altered, verified by diffing old and new content sorted, and by word count.

Note on this branch's own history: the first attempt at this reordering was cut from a `main` that predated the §2.9 entry, so once §2.9 merged the branch conflicted across the whole file (one side had rewritten every line's position, the other had inserted a new section at the top). Rather than resolve that hunk-by-hunk, the branch was reset onto current `main` and the reordering redone against the nine-section content — same end state, no conflict.


## 2026-09-13 (Chapter 4 landing: screening 2×2)

Replaced the Chapter 4 landing-page Mermaid diagram. It was a table-of-contents flowchart (section boxes and "comes after" arrows), which duplicates the sidebar nav and the "In this chapter" table on the same page. `diagram-ideas.md` already named this page as the first replacement: the chapter's actual argument is a *screening decision*, which is a 2×2, not a reading-order flowchart.

The new diagram is a Mermaid `quadrantChart` with axes "public-data availability" × "basic-element clarity", placing the five sub-fields already assessed in §4.5 / §4.8:

- Load FM and Grid FM in the mature quadrant (clean basic element + public or physically-simulated data).
- UBEM in the "element exists; generate the data" quadrant (simulator-grounded, privately generable).
- Weather / microclimate in the "data exists; fusion missing" quadrant (HLS / Sentinel / ERA5 abundant, not yet fused with load or grid).
- Multi-carrier hub in the immature quadrant (no clean basic element, essentially no public data) — the reason it is the Chapter 5 case study.

No new claims; a short caption under the chart points at §4.5–4.8 and at the T1–T9 task screen in §4.6/§4.7. `last_reviewed` on the landing page bumped to 2026-09-13.

Uses `quadrantChart`, which needs Mermaid 11 (already pinned as `11.4.1` in `_config.yml`). If GitHub Pages fails to render it, fall back to a labelled 2×2 flowchart — noted in TODO.md.

## 2026-09-13 (fix: Chapter 4 quadrantChart syntax error)

Barton reported a large "Syntax error in text — mermaid version 11.4.1" box on the Chapter 4 landing page, in place of the screening 2×2 added by PR #19.

I had reviewed that PR and said the diagram would render, on the strength of having confirmed `quadrantChart` shipped in Mermaid v10.2.0 (so the repo's 11.4.1 pin covers it). That was the wrong check: the version was never the problem, and I asserted it would render without ever running the block through a parser.

**Root cause: two unquoted semicolons.** In the quadrant grammar (`quadrant.jison`), `";"` returns a `SEMI` token and `eol` is defined as `NEWLINE | SEMI | EOF` — a semicolon terminates a statement. So `quadrant-2 Element exists; generate the data` parsed as `quadrant-2 Element exists`, then failed trying to read `generate the data` as a fresh statement. Same for `quadrant-4 Data exists; fusion missing`.

Verified empirically rather than by inference this time — installed Mermaid 11.4.1 locally and parsed the exact block plus isolated single-character variants:

| Case | Result |
| :--- | :--- |
| Exact block from `main` | FAIL — `Parse error on line 6: ...s; generate the data` |
| Semicolon in a quadrant label, isolated | FAIL — same error |
| Colon in `title`, isolated | PASS (lexer rule `<title>(?!\n\|;\|#)*[^\n]*` does not exclude `:`) |
| Slash in a point name, isolated | PASS (`/` is in the grammar's `PUNCTUATION` class) |
| Fix A — semicolons replaced with dashes | PASS |
| Fix B — quadrant labels wrapped in double quotes | PASS |

So the title colon and the `Weather / microclimate` slash were both innocent; only the semicolons broke it.

Applied **Fix B** (quoting) rather than Fix A (rewording), to preserve the PR author's exact wording. Re-extracted the block from the file on disk after the edit and re-parsed it: PASS.

Also scanned every other Mermaid block in the book for the same bug class — no other block contains a semicolon, and `quadrantChart` is the only non-`flowchart` diagram in use, so this is contained to this one page.

Updated the `TODO.md` note that had said to fall back to a `flowchart` if Pages failed to render the quadrant chart; that advice was based on the wrong diagnosis and is now corrected.

## 2026-09-13 (four energy-domain FM references)

Applied Barton's 14-point editing guideline: add four references, each **tied to a specific claim in the main text** rather than parked in the bibliography. Placement was chosen by topic (Barton's call) rather than by the chapter numbers the guideline listed, so each citation sits where the book already makes the relevant argument.

| Reference | Placed in | Claim it supports |
| :--- | :--- | :--- |
| Arjunan et al. 2026, *EnergyFM* (e-Energy '26) | §2.4.2, new subsection | Domain-specific energy FMs already exist on the demand side; their basic element is a single-carrier meter series, which is exactly what the multi-carrier layer lacks |
| Park et al. 2025, *Energy and Buildings* 348:116446 | §2.9, dimensions 2 and 6 | Zero-shot transfer can fall short off-distribution while fine-tuning recovers much of it — so transferability is measured, not assumed; also that probabilistic forecasting is achievable with FMs |
| Bose et al. 2024, arXiv:2411.14421 | §2.6, scaling laws | Dataset heterogeneity and architecture outweighed parameter count — reframes the planning question as sampling design, not model budget |
| Lin et al. 2024, arXiv:2411.08888 | §6.1, G4 — Benchmarks | Building-scale TSFM benchmarks exist but score only single-modality metered data, so a UES benchmark cannot be assembled by pointing generic FM benchmarks at energy data |

**Fixed a fabricated author field.** The pre-existing `energyfm2026` entry credited the institutions (`{Empa and IBM Research and IISc Bangalore}`) as the author — a placeholder, not real metadata. Crossref gives the actual authors: Arjunan, Srivastava, Kumar, Jati, Ekambaram, Dayama, pages 556–568. Entry corrected and rekeyed to `arjunan2026energyfm` to match the `firstauthorYEARshortname` convention; the old key was uncited anywhere, so nothing dangled. It is now cited for the first time.

**Date discrepancy recorded rather than smoothed over.** Barton's guideline dates Park et al. to 2026; Crossref returns 2025 (online-first, in a 2026-dated issue). The `.bib` entry uses 2025 with a `note` field stating both, so the next person doesn't silently "correct" it in either direction.

Added the guideline's item 13 to `CONTRIBUTING.md`'s references workflow as a standing rule: a reference must be attached to a statement making explicit (1) what the work demonstrated, (2) what limitation remains, (3) how that limitation bears on urban energy systems. The second and third are the ones usually skipped, and are what make a citation load-bearing rather than decorative.

All four references verified against Crossref/arXiv before use. Checked after editing: footnote ref/def integrity on all four edited pages, bib key uniqueness, brace balance (596/596), and DOI/arXiv identifiers matching between `.bib` and footnotes.
