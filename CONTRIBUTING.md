# Contributing

📖 Read the book: **https://bartonchentw.github.io/FM4UES/**

This is a living, open-contribution knowledge base — started by
[Barton Chen](https://github.com/BartonChenTW), but corrections, references,
and new sections are welcome from anyone in the urban energy systems (UES)
or foundation model (FM) communities.

Much of the existing text was drafted and edited with Claude (Opus 5 and
Sonnet 5, Anthropic) under Barton's direction and review. That doesn't
change what's expected of new contributions: claims should trace to a real,
checkable source (see the references workflow below), whether written by a
person, drafted with AI assistance, or both.

## How changes get in

`main` is protected — nobody, including the maintainer, pushes to it
directly. Every change goes through a pull request:

1. **Fork** this repo (or, if you've been added as a collaborator, create a
   branch directly).
2. Make your change on a branch.
3. Open a **pull request** against `main`. The `lychee` link-check workflow
   runs automatically; it needs to pass before the PR can merge.
4. The maintainer (or another reviewer, once there are some) reviews and
   merges.

For small fixes (typos, a broken link) this whole cycle can be quick —
GitHub's web editor can create the fork, branch, and PR for you in one go
from the file's "Edit" (pencil) button.

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
  to [`appendices/a-glossary.md`](appendices/a-glossary.md).
- Cite claims. See the references workflow below.
- British English spelling, matching the existing text (e.g. "optimisation",
  "modelling").
- Each page has Jekyll front matter (`title`, `parent`, `nav_order`, and for
  section pages also `status` and `last_reviewed`, rendered via
  `{% include page-status.html %}`). Match the existing pattern when adding
  a page — see any section file for the format. Chapters are folders with
  an `index.md` (`has_children: true`) and one file per numbered section
  (`parent:` pointing back to the chapter's title).

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
