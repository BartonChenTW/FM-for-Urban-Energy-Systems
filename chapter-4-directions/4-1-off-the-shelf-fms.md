---
title: "4.1 Using Existing FMs Off the Shelf"
parent: Chapter 4 — Directions for FMs in UES
nav_order: 1
status: draft
last_reviewed: 2026-09-11
---

# 4.1 Using Existing Foundation Models Off the Shelf
{: .no_toc }

{% include page-status.html %}

The most useful direction to a practitioner today, and the one requiring the least new work.
{: .fs-6 .fw-300 }

{: .note }
**Stub — needs expansion.** This section states the direction and points to where the supporting material already lives in this book. It does not yet contain a worked example or benchmark numbers specific to a UES load-forecasting task — that would need an actual evaluation run, not just a description of one.

1. TOC
{:toc}

---

## The direction

Before building anything bespoke, the cheapest and most immediately useful thing a UES practitioner can do is evaluate an already-pretrained, general-purpose time-series foundation model **zero-shot** on their own forecasting problem — no training, no fine-tuning, just point the model at the series and read off a forecast. The current generation of these models (Chronos-2, TimesFM 2.5, Moirai 2.0, TabPFN-TS — see [§2.4.1](../chapter-2-fm-foundations/2-4-1-time-series-fms.html)) is production-grade and free or cheap to run.

This is directly applicable to **load forecasting** — predicting building or district electricity, heat, or cooling demand a few hours to days ahead (T3 in [§3.1](../chapter-3-sim-opt/3-1-taxonomy-of-tasks.html)) — which is already flagged as a task with mature, off-the-shelf solutions in [§4.7](4-7-reading-the-screen.html).

## Why this belongs before any bespoke build

The build path recommended for Tier 1 dispatch modelling in [§4.9.1](4-9-1-methods-tier1.html) already makes this argument formally as "Step 2 — Zero-shot TSFM evaluation," and the baseline discipline in the same section makes the general case: **run the cheapest available option first, because it tells you whether anything more elaborate is warranted at all.** For pure load forecasting (as opposed to dispatch, which additionally needs energy-balance and storage-state handling), zero-shot evaluation is frequently sufficient on its own and does not need the rest of the Tier 1 build path.

## What would need to be added here

- A worked comparison of zero-shot Chronos-2 / TimesFM 2.5 against a seasonal-naive baseline and a tuned gradient-boosting model, on a real or simulated UES load-forecasting task.
- Notes on which covariates (weather, calendar, building metadata) each model can actually ingest zero-shot, referencing the covariate-handling differences in [§2.4.1](../chapter-2-fm-foundations/2-4-1-time-series-fms.html).
- Practical guidance on context length and how far ahead these models degrade for typical UES horizons (day-ahead, week-ahead).

---
[← Back to Chapter 4](index.html) · [Next: 4.2 FMs for Whole Building Stocks →](4-2-fms-for-building-stocks.html)
