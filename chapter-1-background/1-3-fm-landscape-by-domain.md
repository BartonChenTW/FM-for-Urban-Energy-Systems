---
title: "1.3 The FM Landscape Today, by Domain"
parent: Chapter 1 — Background
nav_order: 3
status: draft
last_reviewed: 2026-09-11
---

# 1.3 The Foundation Model Landscape Today, by Domain
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

| Domain | Representative models | What they learn |
| :--- | :--- | :--- |
| Language | GPT-5-class, Gemini, Claude, Llama | Sequences of text tokens |
| Vision | ViT, SAM/SAM2, DINO | Sequences of image patches |
| Multimodal | Unified generation-and-understanding models | Cross-modal alignment across text, image, audio |
| Weather / climate | GraphCast, FengWu, Aurora | Physical fields on a spatiotemporal grid |
| Geospatial / remote sensing | Prithvi, ScaleMAE, Granite-GFM | Satellite pixels and patches over space and time |
| Time series | TimesFM, Chronos, Moirai, TTM, Toto, TimeGPT | Numeric sequences |
| Graph-structured systems | Emerging graph FMs, GridFM-v0 | Node/edge-structured data |
| Robotics / embodied | Vision-language-action models | Vision, language, touch, force, proprioception |

Granite-GFM is built on the Prithvi-SWIN-L Earth observation foundation model and uses a Swin Transformer backbone to estimate land surface temperature at 30 m resolution and hourly frequency for arbitrary cities.[^szwarcman2024prithvieo2]

{: .warning }
**The field moves fast.** Publication counts on LLM-and-energy alone went from roughly 1 (2022) to 13 (2023) to 128 (2024) to 464 (2025), with 348 already indexed in the first half of 2026. Re-check anything in this table before it is used to justify a novelty claim.

Two families are directly relevant to this book and get dedicated treatment: [time-series FMs](../chapter-2-fm-foundations/2-4-1-time-series-fms.html) and [power-grid FMs](../chapter-2-fm-foundations/2-4-2-power-grid-fms.html), in [§2.4](../chapter-2-fm-foundations/index.html).

[^szwarcman2024prithvieo2]: Szwarcman, D., Roy, S., Fraccaro, P. et al. (2024). [Prithvi-EO-2.0: A versatile multi-temporal foundation model for Earth observation applications](https://arxiv.org/abs/2412.02732). arXiv:2412.02732.

---
[← Previous: 1.2 FMs in One Page](1-2-fms-in-one-page.html) · [Next: 1.4 Directions the Field Is Moving →](1-4-fm-field-directions.html)
