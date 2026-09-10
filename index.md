---
title: Home
layout: home
nav_order: 1
---

# Foundation Models for Urban Energy Systems
{: .fs-9 }

A working textbook: what gets simulated, what could be learned, and how to build it.
{: .fs-6 .fw-300 }

Version 1.1 — 10 September 2026
{: .label }

---

## How to use this document

This is written for someone who knows urban energy systems well and machine learning less well. It has three jobs:

1. **Map the domain** — what actually gets modelled and simulated in urban energy systems, what mathematical object each task is, and which tools do it.
2. **Screen for foundation-model potential** — of all those tasks, which ones could plausibly support a foundation model, and which could not, with explicit criteria.
3. **Give the methods** — for the tasks that pass the screen, what architecture and training approach fits, in enough detail to start building.

**If you read only one page**, read [Choosing a Basic Element](03-basic-elements.html) — it gives the criterion for deciding whether a foundation model is viable in a sub-domain at all, before any question of architecture or compute.

The **[Methods by Problem Class](06-methods-tier1.html)** pages are the operational core: three tiers of increasing difficulty (single-hub dispatch → multi-hub multi-carrier dispatch → design and sizing optimisation), each with a concrete build path.

{: .warning }
**The field moves fast.** Publication counts on LLM-and-energy alone went from roughly 1 (2022) to 13 (2023) to 128 (2024) to 464 (2025), with 348 already indexed in the first half of 2026. Re-check anything that reads as a landscape or novelty claim before it is used to justify a proposal or paper.

---

## Contents

| Part | Page | Covers |
| :--- | :--- | :--- |
| I | [The Domain](01-the-domain.html) | Scales, task taxonomy, tool landscape, where cost lives |
| II | [FM Fundamentals](02-fm-fundamentals.html) | What makes a model a foundation model; the five design decisions |
| II | [Choosing a Basic Element](03-basic-elements.html) | The four-requirement criterion; why buildings resist tokenisation; representation strategies and testable predictions |
| II | [The FM Landscape](04-fm-landscape.html) | Time-series FMs, grid FMs, tabular FMs and the cell, what doesn't exist yet |
| III | [Screening Tasks](05-screening.html) | Which sub-domains pass the screen for FM treatment, and which don't |
| IV | [Tier 1 — Single Hub Dispatch](06-methods-tier1.html) | Build path, baselines, architecture choice |
| IV | [Tier 2 — Multi-Hub, Multi-Carrier](07-methods-tier2.html) | Graph neural networks, neural operators, topology generalisation |
| IV | [Tier 3 — Design & Sizing](08-methods-tier3.html) | Amortised optimisation, feasibility guarantees, the decision-space problem |
| V | [Building It](09-building-it.html) | Data generation, physics enforcement, evaluation protocol, budget realism |
| VI | [Open Gaps](10-open-gaps.html) | Nine gaps, ordered by how defensible they are as research contributions |
| — | [Glossary](appendix-a-glossary.html) | Plain-language definitions of every ML term used |
| — | [Pre-Project Checklist](appendix-b-checklist.html) | Thirteen questions to ask before starting |
| — | [Project Notes: Applied Example](appendix-c-buildfm-bs2027.html) | A real submission worked through the framework — public, redacted version |
| — | [Reference Pointers](11-references.html) | Full bibliography, grouped by what it's useful for |
