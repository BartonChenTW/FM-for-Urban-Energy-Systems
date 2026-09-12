---
title: "2.8 Surrogates vs Foundation Models"
parent: Chapter 2 — Foundation Knowledge of FMs
nav_order: 8
status: draft
last_reviewed: 2026-09-11
---

# 2.8 Surrogate Models vs Foundation Models
{: .no_toc }

{% include page-status.html %}

UES readers already know surrogates well. The contrast with a foundation model is the fastest way in, and explains why an FM is more than a bigger surrogate.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## What a surrogate is

A surrogate model is a fast approximation of an expensive model — trained to reproduce the input-output behaviour of a simulator or optimiser without running it. Surrogates are already routine in this domain: a neural network trained to predict energy hub operating cost as a function of design variables, standing in for a full engineering simulation inside an outer sizing loop (see [§3.4](../chapter-3-sim-opt/3-4-dispatch-optimisation.html) and Family 1 in [§4.9.3](../chapter-4-directions/4-9-3-methods-tier3.html)).

## The distinction, precisely

Both a surrogate and a foundation model are approximations, fitted to data rather than derived from first principles. **The difference is entirely in the training distribution and the transfer claim** — not in the mathematics of the model itself:

| | Surrogate | Foundation model |
| :--- | :--- | :--- |
| Trained on | One system (or a narrow family) | A broad distribution of systems |
| Reused across | One study, then discarded | Many future studies, by other users |
| Transfer claim | None required — fits the system it was trained on | Central — must work on unseen instances |
| Task scope | Usually one task | Multiple downstream tasks (see [§2.1](2-1-what-defines-an-fm.html)) |

A surrogate that works beautifully on the system it was trained on, and is thrown away at the end of the project, has made no transfer claim and needs none. **Calling that a foundation model is the single most common and most damaging framing error available in this space** — it invites a scrutiny (does it generalise? is it multi-task?) that a project-scoped surrogate was never designed to survive, and that is the wrong standard to hold it to.

## Why the existing multi-energy surrogate literature is not FM work

The existing surrogate literature for multi-carrier energy hubs and districts is almost entirely bespoke: one surrogate per system, small training data, discarded at project end (see [§4.9.3](../chapter-4-directions/4-9-3-methods-tier3.html)). This is not a criticism of that literature — bespoke surrogates are often the right tool for a single study — but it means the foundation-model claim for this domain is essentially unmade so far. **The foundation-model contribution, where it exists, is making the same class of model transferable across systems rather than rebuilt for each one** — this is the throughline connecting [Chapter 4](../chapter-4-directions/index.html)'s survey to [Chapter 5](../chapter-5-case-study/index.html)'s specific proposal.

## The amortisation argument

The economic case for paying the higher upfront cost of foundation-model training rather than a cheaper bespoke surrogate rests on reuse: the cost is paid once, across a distribution of systems, and amortised over every subsequent study, rather than paid once per study. This argument is developed in full, with the break-even arithmetic, in [§3.4](../chapter-3-sim-opt/3-4-dispatch-optimisation.html) and revisited for the specific case study in [Chapter 5](../chapter-5-case-study/index.html).

{: .warning }
The amortisation arithmetic only holds if the model actually transfers. Where the basic element fails the criterion in [§2.3.1](2-3-choosing-a-basic-element.html#231-the-criterion), what looks like a foundation model is a collection of memorised cases, and the payback never arrives — it is a surrogate with foundation-model marketing. Check the representation before running the amortisation calculation.

---
[← Previous: 2.7 Architectures](2-7-architectures.html) · [Back to Chapter 2](index.html) · [Next: 2.9 Evaluation Criteria for UES Foundation Models →](2-9-ues-fm-evaluation-criteria.html)
