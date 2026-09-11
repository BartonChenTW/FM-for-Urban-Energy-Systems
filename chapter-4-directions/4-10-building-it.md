---
title: "4.10 Building It"
parent: Chapter 4 — Directions for FMs in UES
nav_order: 10
status: draft
last_reviewed: 2026-09-11
redirect_from: /09-building-it.html
---

# 4.10 Building It: Data, Physics, Evaluation, Budget
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

## 4.10.1 Data generation and sampling design

Since ground truth comes from a simulator, **the training distribution is a design decision, not a given**. This is the most under-appreciated step.

### What to sample

- **Configurations** — device types, capacities, storage sizes, topologies (Tier 2+)
- **Boundary conditions** — weather years, demand profiles, prices, carbon intensity
- **Operating regimes** — including rare ones

### Sampling methods

| Method | Use |
| :--- | :--- |
| Latin Hypercube | good default coverage of continuous design space |
| Sobol / quasi-random | better uniformity in high dimensions |
| Adaptive / active learning | concentrate samples where surrogate error is high |
| Stratified by regime | guarantee coverage of rare states |

### The rare-regime trap

{: .important }
**Take this seriously.** Foundation models inherit statistical biases from their training datasets, including under-representation of extremes and rare regimes, which distorts performance precisely on high-impact events.

In energy systems the rare regimes are the ones that matter most: cold snaps driving peak heat demand, Dunkelflaute, storage fully depleted, network constraints binding. Uniform sampling of the design space will under-represent all of them. **Stratify deliberately.**

### Normalisation across carriers

Carriers differ by orders of magnitude in typical values (kW electricity versus MWh seasonal heat storage). Per-carrier standardisation is the minimum; consider physical non-dimensionalisation (fractions of capacity, fractions of peak demand), which additionally helps transfer across systems of different sizes.

### Synthetic and archetype-derived data — what it buys and what it does not

See [§3.2](../chapter-3-sim-opt/3-2-building-simulation-data.html) for this in full — the summary: simulator-generated corpora are fully labelled, but archetype-derived data supports interpolation across archetype space, not generalisation to real heterogeneity, and the corpus silently absorbs the generating optimiser's assumptions.

## 4.10.2 Enforcing physics

Four mechanisms, in increasing order of strength and cost:

| Mechanism | How | Guarantee | Cost |
| :--- | :--- | :--- | :--- |
| **Soft penalty** | add constraint violation to loss | none | free |
| **Architectural** | design outputs so constraints hold by construction (bounded decoders, softmax splits) | exact for what is encoded | low |
| **Projection / repair** | post-process onto feasible set | exact | moderate |
| **Exact encoding in solver** | encode NN as MILP constraints | exact + optimality | high |

Notes from practice:

- Bounded decoders and physics-informed regularisation preserve operational feasibility in GNN-based OPF, but residual violations may still require post-processing for strict feasibility.[^wen2026lghgnn-410]
- Physics-informed approaches embedding multi-physics dynamic constraints in the loss enable physically consistent solutions with limited training samples and improve accuracy under sparse data — a valuable property when simulator runs are expensive.
- Feasibility-restoration layers are an active area; repair layers for networks with hard constraints are being developed as reusable components.[^chu2026snarenet]

**Recommendation for multi-carrier energy systems:** architectural enforcement of per-carrier energy balance (make the outputs sum correctly by construction), plus soft penalties for inequality constraints, plus a projection step if hard feasibility is required downstream. See also [§5.6](../chapter-5-case-study/5-6-physics-loss.html) for the physics-loss inventory attached to this book's specific case-study representation.

## 4.10.3 Evaluation protocol

A credible protocol reports all six. Reporting only the first is the most common weakness in this literature.

1. **Accuracy** — error on held-out instances, per carrier, per horizon
2. **Feasibility** — constraint violation rate and magnitude; energy balance residual
3. **Optimality gap** (Tier 3) — cost versus true optimum
4. **Speedup** — honestly reported, **including** data generation and any post-processing correction. Note the pattern in power systems where speedup is reported both before and after correction, with an order-of-magnitude difference between them.
5. **Transfer** — performance on unseen configurations/topologies; this is the actual foundation-model claim
6. **Calibration** — if probabilistic, are the intervals honest?

{: .note }
Where the domain community has an established accuracy measure, use it alongside generic ML metrics. For building energy, NRMSE and CV(RMSE) are the calibration measures practitioners already read, and reporting them costs nothing while substantially improving how the work lands.

### Held-out design

Random splits overstate performance. Hold out along the axis you claim to generalise over:

- unseen **configurations** (Tier 1/2 claim)
- unseen **topologies** (Tier 2 claim)
- unseen **archetypes / typologies** (building-scale claim)
- unseen **weather years / climate regimes**
- unseen **scales** (train small, test large)

Note the caution from adjacent domains: models trained and evaluated primarily at one scale and horizon have largely untested ability to generalise across spatial and temporal scales.

## 4.10.4 Realistic budget expectations

At roughly CHF 30k/year materials:

| Feasible | Not feasible |
| :--- | :--- |
| Fine-tuning models in the 10M–500M parameter range | Pretraining a large model from scratch |
| 10³–10⁵ simulator runs for training data | 10⁷+ runs |
| Small scaling studies | Large architecture sweeps |
| Releasing a benchmark and dataset | Sustained large-scale compute |

{: .important }
**The honest deliverable at this budget is: a representation, a dataset, a benchmark, and a demonstrated small model — not a large trained foundation model.** Framing matters: *"we establish what a foundation model for this domain requires, and demonstrate feasibility"* is credible and fundable. *"We build a foundation model"* is not, at this budget, and reviewers who know the field will notice.

### Publication format follows from the budget

The same logic applies to papers. For a novel concept with limited empirical results, three formats are available:

- **Pure empirical** — a benchmark, a baseline, a measurement. Safe with reviewers; low ceiling. Competent and rarely cited.
- **Pure concept / position** — argument only. High ceiling, but at an engineering venue it reads as a proposal unless it does real analytical work: a criterion others can apply, a taxonomy with consequences, falsifiable predictions, a benchmark specification.
- **Anchored concept paper (recommended)** — argument-led, with one demonstrative empirical result. Roughly three-quarters argument, one-quarter evidence. The argument carries the paper; a single result converts the central claim from assertion to demonstration.

The anchored format matches the budget reality above: it does not depend on a trained model existing by the deadline, and it fails gracefully — if training slips, the paper still stands; if it succeeds, a results subsection is added without restructuring.

**Audience translation is part of the format choice.** Writing FM concepts for a domain audience means introducing every ML idea through its domain counterpart ([§2.3.1](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html#231-the-criterion) does this with discretisation), avoiding unexplained vocabulary, and including a short glossary. The test: if a paragraph requires ML background to parse, rewrite it.

[^wen2026lghgnn-410]: Wen, A., Wen, B., Li, J., Xu, J. (2026). [Heterogeneous graph neural network with local and global message passing for AC-optimal power flow solutions](https://doi.org/10.3390/asi9010018). *Applied System Innovation*, 9(1), 18.
[^chu2026snarenet]: Chu, Y.-C., Boukas, A., Udell, M. (2026). [SnareNet: Flexible repair layers for neural networks with hard constraints](https://arxiv.org/abs/2602.09317). arXiv:2602.09317

---
[← Previous: 4.9.3 Tier 3](4-9-3-methods-tier3.html) · [Back to Chapter 4](index.html) · [Next: Chapter 5 — Case Study →](../chapter-5-case-study/index.html)
