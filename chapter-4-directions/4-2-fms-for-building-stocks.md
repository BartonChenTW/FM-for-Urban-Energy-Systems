---
title: "4.2 FMs for Whole Building Stocks"
parent: Chapter 4 — Directions for FMs in UES
nav_order: 2
status: draft
last_reviewed: 2026-09-11
---

# 4.2 Foundation Models for Whole Building Stocks
{: .no_toc }

{% include page-status.html %}

{: .note }
**Stub — needs expansion.** This section states the direction and its relationship to the rest of the book. It does not yet survey specific stock-scale FM implementations in depth.

1. TOC
{:toc}

---

## The direction

Everything in [§2.3](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html) and most of this book's case study in [Chapter 5](../chapter-5-case-study/index.html) treats a single building or a single hub as the unit of interest. A different and complementary direction treats the **building stock** — a whole city or region's worth of buildings — as the object, with the individual building as R4's "stock-level" basic element (see [§2.3.3](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html#233-representation-strategies-and-testable-predictions)).

This changes the questions that are answerable. Instead of "what will this building's demand be," the target becomes portfolio-level: aggregate demand under a retrofit policy, stock-wide emissions trajectories, or which archetypes in a city-scale stock are under-represented in a training corpus. Large physics-based stock models — **ResStock**[^wilson2022resstock] and **ComStock**[^parker2023comstock] (NREL) — already generate the kind of fully-labelled, large-N corpora (see [§3.2](../chapter-3-sim-opt/3-2-building-simulation-data.html)) that a stock-level foundation model would pretrain on.

## Relationship to the rest of this book

R4 in [§2.3.3](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html#233-representation-strategies-and-testable-predictions) already names this trade-off precisely: a stock-level representation is unambiguous and composable *at the stock level*, and generalises across stocks, but gives up within-building resolution — it cannot answer "what will happen to this specific building's hourly profile," only "what will happen in aggregate." This makes it a genuinely different target from the case study in [Chapter 5](../chapter-5-case-study/index.html), which is deliberately building/hub-resolved.

## What would need to be added here

- A survey of existing stock-scale learned models built on ResStock/ComStock or equivalent European stock datasets, and what pretraining objective each uses.
- A worked comparison of stock-level versus building-level representation against the four requirements in [§2.3.1](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html#231-the-criterion), analogous to the building-level analysis already done in [§2.3.2](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html#232-basic-elements-for-buildings).
- Discussion of how stock-level and building-level representations could be composed (e.g. a stock-level model providing priors that a building-level model fine-tunes against).

[^wilson2022resstock]: Wilson, E., Parker, A., Fontanini, A. et al. (2022). [End-use load profiles for the U.S. building stock: Methodology and results of model calibration, validation, and uncertainty quantification](https://doi.org/10.2172/1854582). NREL/TP-5500-80889.
[^parker2023comstock]: Parker, A., Horsey, H., Dahlhausen, M. et al. (2023). [ComStock reference documentation (V.1)](https://doi.org/10.2172/1967948). NREL/TP-5500-83819.

---
[← Previous: 4.1 Off-the-Shelf FMs](4-1-off-the-shelf-fms.html) · [Next: 4.3 LLM Agents for Simulation →](4-3-llm-agents-for-simulation.html)
