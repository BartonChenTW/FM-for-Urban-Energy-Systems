# Contributing

This is a living knowledge base — corrections, references, and new sections
are welcome from anyone in the urban energy systems (UES) or foundation
model (FM) communities.

## Ways to contribute

- **Report an error or an outdated claim** — open an issue.
- **Suggest a reference** — open an issue with the citation (a DOI or URL is
  enough) and a one-line note on which section it belongs to. See
  [references/](references/) for how the bibliography is organised.
- **Propose a new section or restructuring** — open an issue first to
  discuss scope before writing, since this book has an explicit outline
  (chapters are numbered and cross-referenced).
- **Fix a typo or small wording issue** — a pull request directly is fine,
  no need to open an issue first.
- **Larger additions** (a new chapter, a reworked argument) — open an issue
  to discuss before investing time in a draft.

## Style notes

- Written for a reader who knows urban energy systems well and machine
  learning less well (or vice versa) — define jargon on first use, or link
  to [`appendix-a-glossary.md`](appendix-a-glossary.md).
- Cite claims. See the references workflow below.
- British English spelling, matching the existing text (e.g. "optimisation",
  "modelling").
- Each page has Jekyll front matter (`title`, `nav_order`). Match the
  existing pattern when adding a page — see any chapter file for the format.

## References workflow

References are tracked in Zotero and exported as BibTeX to
[`references/`](references/) for import by others. In the text, cite using
Markdown footnotes:

```markdown
Physics-informed models reduce data needs.[^raissi2019]

[^raissi2019]: Raissi, M. et al. (2019). Physics-informed neural networks.
  *J. Comput. Phys.*
```

Use the same citation key as the `.bib` entry (e.g. `raissi2019`) as the
footnote name, so the two stay traceable to each other.

## Local build

```bash
bundle install
bundle exec jekyll serve
```

Requires Ruby and Bundler. Not required just to read or edit the Markdown —
only for previewing how a change renders on the site.

## Questions

Open an issue, or see [`TODO.md`](TODO.md) if you're wondering what's
already planned.
