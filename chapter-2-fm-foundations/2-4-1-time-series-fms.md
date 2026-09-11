---
title: "2.4.1 Time-Series FMs"
parent: "2.4 Existing FMs Relevant to Energy"
grand_parent: Chapter 2 — Foundation Knowledge of FMs
nav_order: 1
status: draft
last_reviewed: 2026-09-11
---

# 2.4.1 Time-Series Foundation Models (Mature)
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

A well-populated field with production-grade options. The current generation includes Chronos-2, Moirai 2.0, TimesFM 2.5, TiRex, TabPFN-TS, Lag-Llama, Time-MoE, Toto, MOMENT, Timer and TTM.

Architecturally distinct approaches worth knowing:

- **Chronos** converts continuous values into discrete tokens via uniform binning and forecasts recursively with a T5 encoder–decoder;[^ansari2024chronos] **Chronos-2** adds multivariate support and covariate handling, using time and group attention layers to exchange information across series, and is pretrained on synthetic multivariate data.
- **Moirai** handles an arbitrary number of input series through an any-variate attention mechanism, with mixture-distribution outputs for uncertainty;[^woo2024moirai] **Moirai 2.0** shows smaller, better-trained models can match larger predecessors via multi-token prediction and improved tokenisation.
- **TimesFM** is a patch-based decoder-only model;[^das2024timesfm] TimesFM-2.0 extends context to 2048 points.
- **TabPFN-TS** is a tabular foundation model pretrained on millions of synthetic regression tasks, adapted to time series, and is notable as the only one in some benchmarks that additionally incorporates **static metadata** (e.g. peak power, tilt, azimuth for a PV plant). See [§2.4.4](2-4-4-tabular-fms.html) for the underlying model family, which is a distinct representational proposition rather than just another TSFM.

**Covariate handling is the key differentiator and it is uneven.** The first generation lacked native covariate handling except Moirai. TiRex and Moirai 2.0 remain univariate with respect to covariates; TimesFM 2.5 combines a pretrained univariate backbone with an auxiliary linear regressor on covariates estimated at inference; Chronos-2 and TabPFN-TS model target and covariates jointly.

**Known limitations to design around:**

- **Long-horizon degradation.** All models degrade beyond their trained maximum prediction length.
- **Covariate usage is under-verified.** Recent work notes that benchmark results offer limited insight into actual covariate usage, and investigates whether models genuinely exploit covariate–target relationships even when those relationships are simple.

{: .note }
Using these models off the shelf, zero-shot, for load forecasting is covered as a practical direction in [§4.1](../chapter-4-directions/4-1-off-the-shelf-fms.html), and as a build path in [§4.9.1 (Tier 1)](../chapter-4-directions/4-9-1-methods-tier1.html).

[^ansari2024chronos]: Ansari, A. F., Stella, L., Turkmen, C. et al. (2024). [Chronos: Learning the language of time series](https://arxiv.org/abs/2403.07815). *Transactions on Machine Learning Research*. arXiv:2403.07815.
[^woo2024moirai]: Woo, G., Liu, C., Kumar, A. et al. (2024). [Unified training of universal time series forecasting transformers](https://arxiv.org/abs/2402.02592). ICML 2024. arXiv:2402.02592.
[^das2024timesfm]: Das, A., Kong, W., Sen, R., Zhou, Y. (2024). [A decoder-only foundation model for time-series forecasting](https://arxiv.org/abs/2310.10688). ICML 2024. arXiv:2310.10688.

---
[← Previous: 2.4 Existing FMs Relevant to Energy](2-4-existing-fms-relevant-to-energy.html) · [Next: 2.4.2 Power-Grid FMs →](2-4-2-power-grid-fms.html)
