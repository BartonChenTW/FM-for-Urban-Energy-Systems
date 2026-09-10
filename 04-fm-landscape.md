---
title: II. The FM Landscape
nav_order: 5
---

# What Already Exists in Energy
{: .no_toc }

1. TOC
{:toc}

{: .warning }
**More crowded than it looks, but crowded in specific places.** Check anything below before using it to justify novelty.

---

## 7.1 Time-series foundation models (mature)

A well-populated field with production-grade options. The current generation includes Chronos-2, Moirai 2.0, TimesFM 2.5, TiRex, TabPFN-TS, Lag-Llama, Time-MoE, Toto, MOMENT, Timer and TTM.

Architecturally distinct approaches worth knowing:

- **Chronos** converts continuous values into discrete tokens via uniform binning and forecasts recursively with a T5 encoder–decoder; **Chronos-2** adds multivariate support and covariate handling, using time and group attention layers to exchange information across series, and is pretrained on synthetic multivariate data.
- **Moirai** handles an arbitrary number of input series through an any-variate attention mechanism, with mixture-distribution outputs for uncertainty; **Moirai 2.0** shows smaller, better-trained models can match larger predecessors via multi-token prediction and improved tokenisation.
- **TimesFM** is a patch-based decoder-only model; TimesFM-2.0 extends context to 2048 points.
- **TabPFN-TS** is a tabular foundation model pretrained on millions of synthetic regression tasks, adapted to time series, and is notable as the only one in some benchmarks that additionally incorporates **static metadata** (e.g. peak power, tilt, azimuth for a PV plant). See [§7.4](#74-tabular-foundation-models--the-cell-as-a-basic-element) for the underlying model family, which is a distinct representational proposition rather than just another TSFM.

**Covariate handling is the key differentiator and it is uneven.** The first generation lacked native covariate handling except Moirai. TiRex and Moirai 2.0 remain univariate with respect to covariates; TimesFM 2.5 combines a pretrained univariate backbone with an auxiliary linear regressor on covariates estimated at inference; Chronos-2 and TabPFN-TS model target and covariates jointly.

**Known limitations to design around:**

- **Long-horizon degradation.** All models degrade beyond their trained maximum prediction length.
- **Covariate usage is under-verified.** Recent work notes that benchmark results offer limited insight into actual covariate usage, and investigates whether models genuinely exploit covariate–target relationships even when those relationships are simple.

## 7.2 Power-grid foundation models (emerging, moving fast)

The power-systems community has already made the move this document is about. Grid foundation models for benchmarking AC-OPF surrogate learning now exist, alongside work on scaling laws of machine learning for optimal power flow, and work on data scaling laws for multi-task electric energy system intelligence with limited fine-tuning.

**This is the single most important reference point.** It means (a) the concept is validated, and (b) the analogous work for urban *multi-carrier* systems is conspicuously absent — which is the gap.

{: .note }
Read together with [§6.6](03-basic-elements.html#66-the-criterion): what makes this domain tractable is not that power systems had more data, but that the bus supplies a basic element satisfying all four requirements. Sub-domains without such an element should not expect the same recipe to work.

## 7.3 Clean-energy forecasting foundation models (mature)

Foundation models in clean-energy forecasting integrate heterogeneous data through multi-modal fusion, and use patch-based tokenisation grouping consecutive timesteps to address the quadratic complexity of self-attention.

## 7.4 Tabular foundation models — the cell as a basic element

A distinct family, and a distinct answer to the representation question. Worth understanding properly because it is a serious competing hypothesis to any bespoke building representation.

**What the cell is.** A cell is a single entry in a table — the value where one row meets one column (building #47's construction year, 1962). Most machine learning treats the **row** as the basic unit: a building becomes a feature vector read as one thing. Tabular FMs go one level finer. Each individual value gets its own representation, and the model attends in two directions — across the row (how does this building's construction year relate to its floor area and heating system?) and down the column (how does it compare to the construction years of all other buildings?). TabPFN assigns a representation to each table cell and applies row-wise and column-wise attention, making the model invariant to permutations of both rows and columns.

**Why it matters.** It removes the fixed schema. A conventional surrogate needs the same columns in the same order every time; change the input list and you refit. If the model reads cells and treats column order as arbitrary, a table with different columns is still readable — one pretrained model applied to a Swiss dataset, then a Dutch one recording different attributes, without retraining. TabPFN v2 introduced a randomised feature-token mechanism to handle heterogeneous feature spaces and support transfer across datasets with differing feature semantics. **This is a direct attack on the mixed-information-types problem** described in [§6.7](03-basic-elements.html#67-basic-elements-for-buildings).

**Mechanism.** These are prior-data fitted networks: pretrained on a large distribution of synthetic tasks so that conditioning on a context table at test time approximates Bayesian inference under the learned prior. Prediction happens in a single forward pass on labelled examples, with no dataset-specific gradient updates.

**Against the four requirements.**

- *Unambiguous:* yes, cleanly — a cell is a recorded value, involving no modeller's judgement, unlike a thermal zone.
- *Stable in meaning:* partly — the model must infer what a column means from the values in it rather than being told.
- *Composable:* yes, trivially.
- *Scale-independent:* bounded — context size limits how much table fits at once.

It therefore scores better than any element in §6.7(a)–(d), which is why it belongs in the analysis rather than being dismissed.

**Where it breaks for energy systems.** A cell holds one value. An hourly profile is 8760 values — not a cell, not a row, and not the table shape at all. Either collapse the profile into summary statistics, losing the temporal structure that matters for retrofit and dispatch assessment, or spread it across 8760 columns, which defeats the purpose and exhausts the context budget.

**Sharpened statement:** the cell is a very good basic element for describing what a system *is*, and no help at all for what it *does* over time.

**Documented limitations to design around.**

- Highly sensitive to distribution shift; incorporating source data with a differing distribution can cause negative transfer and degrade target accuracy. This maps directly onto the held-out-typology test (P3 in [§6.8](03-basic-elements.html#68-representation-strategies-and-testable-predictions)).
- Bounded by maximum context size. TabPFN-2.5 scaled in-context learning to roughly 50,000 samples and 2,000 features; TabICL uses a two-stage architecture reaching around 500,000 samples.

**Predicted profile:** strong on scalar outcomes (P1), structurally weak on hourly profiles (P2), questionable across unseen typologies (P3). Tabular FMs are best understood as **R1 with a foundation model attached** — which makes them a more informative baseline than gradient boosting alone.

## 7.5 What does not exist

- No foundation model for **multi-carrier urban energy system operation**.
- No foundation model for **energy system design/planning models**.
- No **benchmark** for either.
- No agreed **representation or interchange format** that preserves assumptions alongside structure.
- No **agreed basic element for buildings**, and no published treatment of the choice as a research question rather than an implementation detail.
- No foundation model representing a **decision space** — the set of possible interventions on a system — alongside its state ([G9](10-open-gaps.html#g9)).

---
[← Previous: Choosing a Basic Element](03-basic-elements.html) · [Next: Screening Tasks →](05-screening.html)
