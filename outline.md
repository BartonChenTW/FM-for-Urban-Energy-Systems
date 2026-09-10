# Proposed Textbook Outline (draft for review)

Private planning file — excluded from the Jekyll site via `_config.yml`.

**Aim:** a living knowledge base that helps people in the urban energy systems (UES) domain learn about foundation models (FMs), building towards the long-term goal of an FM for UES.

**How to read this outline:** each section lists its *sources* — where the content comes from today. `add/FM` = `add/FM_for_UES.md`, `add/ref` = `add/reference.md`. Sections marked **NEW** have little or no existing text and need writing.

---

## Part 1 — Background: Urban Energy Systems and Foundation Models

*Goal: orient a UES reader. What the domain is, what FMs are at a glance, why the two should meet now.*

| § | Section | Sources |
|---|---|---|
| 1.1 | What an urban energy system contains | `01-the-domain` §1 |
| 1.2 | FMs in one page: what changed in AI since ~2018 | **NEW** (short, non-technical) |
| 1.3 | The FM landscape today, by domain | `add/FM` §1.1 |
| 1.4 | Directions the FM field is moving | `add/FM` §1.2 |
| 1.5 | Why UES, why now | **NEW**, drawing on `01-the-domain` §4 (cost) |
| 1.6 | Scope of this book and how to use it | `index` "How to use this document" |

## Part 2 — Foundation Knowledge of FMs

*Goal: give the reader the conceptual toolkit to judge any FM proposal.*

| § | Section | Sources |
|---|---|---|
| 2.1 | What actually defines a foundation model | `02-fm-fundamentals` §5, `add/FM` §2 |
| 2.2 | The five design decisions (unit, tokenisation, architecture, objective, evaluation) | `02-fm-fundamentals` §6, `add/FM` §8.1 |
| 2.3 | Choosing a basic element | `03-basic-elements` (all) |
| 2.4 | Existing FMs relevant to energy | |
| 2.4.1 | — Time-series FMs | `04-fm-landscape` §7.1, `add/ref` §2 |
| 2.4.2 | — Power-grid FMs | `04-fm-landscape` §7.2, `add/ref` §1 |
| 2.4.3 | — Clean-energy forecasting FMs | `04-fm-landscape` §7.3 |
| 2.4.4 | — Tabular FMs | `04-fm-landscape` §7.4 |
| 2.4.5 | — Geospatial & weather FMs | `add/ref` §3 (**NEW** text) |
| 2.5 | What does not exist yet | `04-fm-landscape` §7.5 |

## Part 3 — Simulation and Optimisation in UES

*Goal: give the ML reader the domain side. What gets computed, with which tools, and where the cost is.*

| § | Section | Sources |
|---|---|---|
| 3.1 | Taxonomy of modelling tasks | `01-the-domain` §2, §2.1 |
| 3.2 | Building energy simulation: loads, datasets, benchmarks | `add/ref` §4 (**NEW** text) |
| 3.3 | Multi-carrier energy hub formalism | `add/ref` §5 (**NEW** text) |
| 3.4 | Operation / dispatch optimisation | **NEW**, bridging to `06-methods-tier1` §11.1 |
| 3.5 | Design and sizing optimisation (MILP etc.) | **NEW**, bridging to `08-methods-tier3` §13.1 |
| 3.6 | The tool landscape | `01-the-domain` §3, `add/ref` §6 |
| 3.7 | Schemas and data standards | `add/ref` §7 (**NEW** text) |
| 3.8 | Where the computational cost actually is | `01-the-domain` §4 |

## Part 4 — Potential Directions for FMs in UES

*Goal: the core of the book. Which problems an FM could plausibly learn, and how.*

| § | Section | Sources |
|---|---|---|
| 4.1 | Screening: which sub-fields fit the FM pattern | `05-screening` (all), `add/FM` §3 |
| 4.2 | Candidate sub-fields for a new FM | `add/FM` §4 |
| 4.3 | Methods by problem class | |
| 4.3.1 | — Tier 1: single hub, dispatch | `06-methods-tier1` |
| 4.3.2 | — Tier 2: multi-hub, multi-carrier | `07-methods-tier2` |
| 4.3.3 | — Tier 3: design and sizing | `08-methods-tier3` |
| 4.4 | The representation problem | `add/FM` §8.2–8.4 |
| 4.5 | A concrete proposed representation (bipartite graph, token schema, worked 50-building example, temporal hierarchy, masking, physics loss, invariances, minimum viable v0) | `add/FM` §9 |
| 4.6 | Module and task decomposition (encoders, pretraining tasks, benchmark suite) | `add/FM` §6 |
| 4.7 | Building it: data, physics, evaluation, budget | `09-building-it` (all) |

## Part 5 — Outlook

*Goal: what is open, what the path looks like, and how readers can contribute.*

| § | Section | Sources |
|---|---|---|
| 5.1 | Open gaps (G1–G9) | `10-open-gaps` |
| 5.2 | A roadmap for a multi-carrier energy hub FM (Phases 0–5) | `add/FM` §5 |
| 5.3 | Risks and unsettled design questions | `add/FM` §10 |
| 5.4 | How to contribute to this knowledge base | **NEW** |

## Appendices

| | Section | Sources |
|---|---|---|
| A | Glossary | `appendix-a-glossary` |
| B | Pre-project checklist | `appendix-b-checklist` |
| C | Applied example: project notes + writing a concept paper | `appendix-c-buildfm-bs2027`, `add/FM` §7 |
| — | References | `11-references` + `add/ref` → merged, cited as footnotes in each chapter, plus master `.bib` in `references/` for Zotero |

---

## Proposed file layout

Uses just-the-docs nesting (`has_children` / `parent`) so each Part appears as a collapsible group in the sidebar.

```
index.md
part-1-background/
  index.md                 (Part 1 landing page, has_children: true)
  1-1-what-is-ues.md
  ...
part-2-fm-foundations/
part-3-sim-opt/
part-4-directions/
part-5-outlook/
appendices/
references/
  references.md            (rendered reference list)
  fm-for-ues.bib           (Zotero import)
```

Alternative: keep one file per Part (5 long pages) rather than one file per section. Simpler to maintain, but pages get long.

---

## Decisions for you

1. **Granularity:** one page per section (layout above) or one page per Part?
2. **Numbering:** existing files use mixed numbering (Part I–VII, sections 1–17, plus 6.6 / 7.1 / 11.1 / 13.1…). OK to renumber everything as 1.1, 2.3, … per the new Parts?
3. **Appendix C / concept-paper notes (`add/FM` §7):** these are specific to one project. Keep them public in an appendix, or move them to a private notes file?
4. **`add/ref` §8 "Project resources & personal communication":** probably shouldn't be public. Drop it, or keep it private?
5. **Part 1.2 "FMs in one page":** want this short intro for UES readers with no ML background?
