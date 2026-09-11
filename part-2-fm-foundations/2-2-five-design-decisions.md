---
title: "2.2 The Five Design Decisions"
parent: Part 2 — Foundation Knowledge of FMs
nav_order: 2
status: draft
last_reviewed: 2026-09-11
---

# 2.2 The Five Design Decisions
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

Every foundation model, in any domain, is defined by five choices. Getting these explicit is most of the intellectual work.

## D1 — Unit of observation

What is *one training example*? Language: a token sequence. Vision: a patch grid. Weather: a gridded state at time t.

For energy systems this is genuinely unresolved for planning models, and only obvious for some operational ones. Candidates at system level:

- one timestep of system state
- one (configuration, boundary conditions, trajectory) triple
- one whole model instance
- one modelling decision

{: .note }
Listing candidates is not the same as choosing between them. [§2.3 Choosing a Basic Element](2-3-choosing-a-basic-element.html) supplies a criterion for doing so, and applies it at building level, where the candidates are different and the answer is harder.

## D2 — Tokenisation / encoding

How is a training example turned into something the architecture consumes?

**A useful framing for domain readers:** tokenisation is a discretisation choice. Every simulation begins by deciding what the object is made of — zones, nodes, cells — and that choice fixes what the model can represent, what it must approximate, and how well it carries to a different case. A learned model faces the identical decision. This analogy is the most effective way to explain the problem to a building simulation or energy systems audience, because they have argued about discretisation for decades.

This is where domain-specific difficulty concentrates. Evidence from adjacent fields:

- **Float-heavy data** needs purpose-built handling; work on power-grid foundation models adopts specially designed float tokenisation so that LLMs can process float-rich problems efficiently.
- **Structured codes** break standard schemes: subword tokenisation optimised for natural language fails to capture the hierarchical and compositional structure of structured medical codes, and dedicated tokenisation recovers measurable performance.[^unistruct2024]
- **Multi-domain data** risks structural loss: tokenisation strategies that combine incompatible spatial discretisations risk losing physical adjacency and introducing aliasing effects in attention layers.[^earthcoupling2026]
- **Multi-resolution data** needs explicit handling: Moirai pairs a multi-patch-size projection scheme handling minute-to-year-scale data with an any-variate attention mechanism that scales to arbitrary numbers of variables.[^woo2024moirai]

**A representation is not one decision but at least four**, and this framing recurs whenever this book proposes a concrete representation (see [§5.2](../part-5-case-study/5-2-representation-problem.html)):

| Family | Atomic unit | Structure | Discrete/continuous | Invariance |
| :--- | :--- | :--- | :--- | :--- |
| LLM | Subword token | 1D sequence position | Discrete, ~50–200 k vocab | None; order is meaning |
| ViT / SAM | 16×16 patch, linearly projected | 2D grid position | Continuous | Weak translation |
| TimesFM / PatchTST / TTM | Patch of N consecutive values, instance-normalised | 1D position | Continuous | Scale, via normalisation |
| Chronos | A quantized value bin | 1D sequence | Discrete codebook | Scale |
| GraphCast / Aurora | Grid cell, all variables at all pressure levels | Icosahedral multi-mesh | Continuous | Spherical geometry |
| GridFM-v0 | A bus carrying (p, q, v, δ) | Graph; lines and transformers as edges | Continuous | Permutation over buses |

## D3 — Architecture

Transformer, graph neural network, neural operator, state-space model, or hybrid. Determined largely by what structure the data has (sequence? graph? function?). See [§2.7](2-7-architectures.html) for what each of these architecture families actually does, aimed at readers without an ML background.

## D4 — Pretraining objective

Next-step prediction, masked reconstruction, supervised imitation of a solver, or self-supervised contrastive. For simulation surrogates this is usually supervised regression on solver output; for sequence models, next-token or next-patch prediction. See [§2.6](2-6-scaling-laws.html) for what "self-supervised" means in practice.

## D5 — Evaluation

What counts as success, and on what held-out distribution? For physical systems this must include **feasibility and conservation**, not only error.

[^unistruct2024]: Representation Learning of Structured Data for Medical Foundation Models (UniStruct). arXiv:2410.13351.
[^earthcoupling2026]: Toward AI-Enabled Earth System Coupling. arXiv:2604.03289.
[^woo2024moirai]: Woo, G., Liu, C., Kumar, A. et al. (2024). Unified training of universal time series forecasting transformers. ICML 2024. arXiv:2402.02592.

---
[← Previous: 2.1 What Defines an FM](2-1-what-defines-an-fm.html) · [Next: 2.3 Choosing a Basic Element →](2-3-choosing-a-basic-element.html)
