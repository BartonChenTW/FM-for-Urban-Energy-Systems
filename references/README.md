---
title: Zotero / BibTeX References
nav_order: 16
---

# References (Zotero / BibTeX)

`fm-for-ues.bib` is the master bibliography for this textbook, in BibTeX
format.

## Import into Zotero

1. Open Zotero → File → Import.
2. Choose "A file (BibTeX, RIS, Zotero RDF, etc.)" and select
   `fm-for-ues.bib`.
3. Import into a new collection (recommended) so it's easy to see what
   came from this repo.

## Where the entries come from

Seeded from the categorised reference lists in
[`add/reference.md`](../add/reference.md) and
[`11-references.md`](../11-references.md), limited for now to entries with
a confirmed author list, venue, year, and link (DOI or arXiv ID). Entries
in `add/reference.md` marked `[to confirm]` are not yet included — see
[`TODO.md`](../TODO.md).

## Adding a reference

- Citation keys use the pattern `firstauthorYEARshortname` (e.g.
  `ansari2024chronos`), matching the footnote names used when citing in
  the chapter text (see [`CONTRIBUTING.md`](../CONTRIBUTING.md)).
- If you use Zotero with the Better BibTeX plugin, it can auto-generate
  keys in this pattern and re-export this file for you.
- Don't guess missing fields (author lists, venues, DOIs) — leave them out
  or mark `[to confirm]`, and open an issue if you're not sure.

## Why this file is excluded from the built site

Set in `_config.yml`'s `exclude:` list — it's a machine-readable data file
for reference managers, not a page meant to be browsed. The rendered
bibliography for readers lives in the chapter pages (as footnotes) and in
[`11-references.md`](../11-references.md).
