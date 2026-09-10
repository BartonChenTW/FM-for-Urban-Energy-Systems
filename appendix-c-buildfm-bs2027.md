---
title: Appendix C — Project Notes
nav_order: 14
status: draft
last_reviewed: 2026-09-10
---

# Appendix C — Project Notes: An Applied Example

{% include page-status.html %}

{: .note }
This page is a **public, redacted** version of internal working notes for a specific paper submission. Author names, internal sign-off status, and details of an unannounced position at the originating lab have been removed. It is kept here because the reasoning is a useful worked example of applying this textbook's framework to a real submission — not because the submission details themselves are the point.

---

## Context

The example below concerns a paper submission to an academic venue in building simulation, in the "Simulation Methods & Emerging Tools" category. Two-stage process: a short abstract first, then a full paper of limited length under double-blind review.

**Double-blind handling used throughout:** no institution names; a named experimental demonstrator building described generically; simulation and optimisation tools may be named since they are public software, but combinations of named tools can still be identifying, so this is decided case by case; self-citations in third person; acknowledgments and funding stripped from the review version.

## Paper scope as agreed

Framed as a **review and position paper**, not an empirical results paper, for three reasons that generalise beyond this specific submission:

1. **Budget and timeline honesty.** Per [§17](09-building-it.html#17-realistic-budget-expectations) and [§17.1](09-building-it.html#171-publication-format-follows-from-the-budget), a trained and validated foundation model was not going to exist by the paper deadline. Promising one in the abstract and under-delivering in the paper is worse than scoping correctly from the start.
2. **Where the actual contribution lives.** The representation argument — [§6.6 through §6.8](03-basic-elements.html) of this textbook — is finished thinking, independent of any training run. It does not depend on compute that hadn't happened yet.
3. **Graceful degradation.** An anchored position paper (argument-led, with one demonstrative empirical result) stands on its own if further experiments slip, and gets stronger without restructuring if they don't.

Scope, concretely: (1) why a foundation model for this sub-domain is needed, (2) a review of existing modelling approaches and foundation models organised **by basic element** rather than by tool family or publication date, so the representation gap is visible before the reader reaches the proposal, (3) candidate directions and open questions.

## What was reused from prior internal material, and what was new

A short internal concept note existed before this paper was scoped, describing a proposed system by name, its motivation, and its planned use of existing simulation and optimisation tools. Reusable from it: the motivation chain (why a foundation model for this domain is timely), the framing of the domain as spanning multiple coupled scales, and the description of how physics-based simulation and optimisation tools would generate training data.

Not reusable, and rewritten: institutional-capability language became method justification; a "rapid decision support" framing became an amortised-inference claim requiring a stated speedup and accuracy trade-off; a budget table, team roster, and month-numbered work-package schedule were dropped entirely, since none of these belong in a paper.

New, and the actual contribution of the paper: the representation argument in full — the four-requirement criterion, the building-level analysis, the representation strategies, and the falsifiable predictions.

{: .warning }
**A framing shift worth naming explicitly in any similar situation:** an internal proposal document typically frames a system as something to be *built*. A paper reframes it as an investigation of whether the representation makes it *possible*. Same underlying project, same data, same tools — a materially different claim. Anyone who signed off on the original proposal framing should see the paper framing before submission, since it is not simply a shorter version of the same argument.

## Language and audience translation

The target reviewer pool has building simulation expertise and little or no machine learning background. Every ML concept in the paper is introduced through its domain counterpart — tokenisation as a discretisation choice (this textbook's [§6.6](03-basic-elements.html#66-the-criterion) does this directly) — with a short glossary for anything unavoidable. Vocabulary discipline applied throughout: "basic element" rather than "token," "carries over" rather than "transfers," "fitted" rather than "trained," wherever the substitution didn't cost precision.

The single most effective persuasive device available for this audience was the thermal-zone example in [§6.7(b)](03-basic-elements.html#67-basic-elements-for-buildings): zoning ambiguity is a debate the building simulation community has already lived, rather than an abstraction imported from machine learning. Leading with material the audience already believes, rather than material they must take on trust, did more work than any amount of careful definition.

## A related open question worth flagging generally

At the time of writing, the originating lab was also hiring for a position on **tabular foundation models** for building and district energy systems — a specific and different answer to the same representation question this paper addresses (see [§7.4](04-fm-landscape.html#74-tabular-foundation-models--the-cell-as-a-basic-element)). Where a project and a new hire's brief overlap this closely, the generalisable lesson is to define the division of labour *before* the position is filled rather than after: for instance, one thread taking tabular/structured representation and another taking sequence/profile-level representation, compared later on a shared benchmark rather than either duplicating the other's work or working around it informally.

## Open decisions carried forward

- Whether to release a benchmark (tasks, held-out splits, baseline results) alongside the paper. Per [G4](10-open-gaps.html#g4--benchmarks), this is the cheapest available upgrade to a position paper — it converts an argument into infrastructure the field can reuse, and it is the artifact most likely to outlive the paper itself.
- Whether specific named tools, in combination, are identifying enough under double-blind review to require genericising rather than naming — a judgment call that has to be made per venue and per co-author group, not answered generically here.

---
[← Previous: Pre-Project Checklist](appendix-b-checklist.html) · [Next: Reference Pointers →](11-references.html)
