---
title: "1.6 Scope and How to Use This Book"
parent: Part 1 — Background
nav_order: 6
status: draft
last_reviewed: 2026-09-11
---

# 1.6 Scope of This Book and How to Use It
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

This is written for someone who knows urban energy systems well and machine learning less well (or vice versa). It has four jobs:

1. **Map the domain** — what actually gets modelled and simulated in urban energy systems, what mathematical object each task is, and which tools do it. [Part 3](../part-3-sim-opt/index.html).
2. **Give the FM toolkit** — the conceptual grounding needed to judge any foundation-model proposal in this space, including basic machine learning concepts for readers without that background. [Part 2](../part-2-fm-foundations/index.html).
3. **Survey the directions** — of all the tasks in the domain, which could plausibly support a foundation model, broadly and neutrally, without committing to one specific programme. [Part 4](../part-4-directions/index.html).
4. **Work through one case study in depth** — a specific, concrete proposal for a foundation model for multi-carrier energy hubs: representation, roadmap, module decomposition, and risks. [Part 5](../part-5-case-study/index.html).

**If you read only one page**, read [Choosing a Basic Element](../part-2-fm-foundations/2-3-choosing-a-basic-element.html) (§2.3) — it gives the criterion for deciding whether a foundation model is viable in a sub-domain at all, before any question of architecture or compute.

The **[Methods by Problem Class](../part-4-directions/4-9-methods-landing.html)** pages (§4.9) are the operational core of the directions survey: three tiers of increasing difficulty (single-hub dispatch → multi-hub multi-carrier dispatch → design and sizing optimisation), each with a concrete build path.

**Part 4 versus Part 5, explicitly.** Part 4 is a neutral survey: what the field as a whole knows about applying foundation models across UES sub-domains, without endorsing one direction over another. Part 5 is a specific, opinionated case study — one concrete proposal for a multi-carrier energy hub foundation model, including a token schema, module decomposition, and a phased roadmap. Readers who want "what does the field know" should read Part 4; readers who want "here is one worked proposal in full technical depth" should read Part 5. The two are kept deliberately separate so the reader can always tell what is established, what is being explored broadly, and what is one group's specific bet.

---
[← Previous: 1.5 Why UES, Why Now](1-5-why-ues-why-now.html) · [Back to Part 1](index.html) · [Next: Part 2 →](../part-2-fm-foundations/index.html)
