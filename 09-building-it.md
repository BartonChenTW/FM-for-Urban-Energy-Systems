---
title: V. Building It
nav_order: 10
status: draft
last_reviewed: 2026-09-10
---

# Part V — Building It
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

## 14. Data generation and sampling design

Since ground truth comes from a simulator, **the training distribution is a design decision, not a given**. This is the most under-appreciated step.

### 14.1 What to sample

- **Configurations** — device types, capacities, storage sizes, topologies (Tier 2+)
- **Boundary conditions** — weather years, demand profiles, prices, carbon intensity
- **Operating regimes** — including rare ones

### 14.2 Sampling methods

| Method | Use |
| :--- | :--- |
| Latin Hypercube | good default coverage of continuous design space |
| Sobol / quasi-random | better uniformity in high dimensions |
| Adaptive / active learning | concentrate samples where surrogate error is high |
| Stratified by regime | guarantee coverage of rare states |

### 14.3 The rare-regime trap

{: .important }
**Take this seriously.** Foundation models inherit statistical biases from their training datasets, including under-representation of extremes and rare regimes, which distorts performance precisely on high-impact events.

In energy systems the rare regimes are the ones that matter most: cold snaps driving peak heat demand, Dunkelflaute, storage fully depleted, network constraints binding. Uniform sampling of the design space will under-represent all of them. **Stratify deliberately.**

### 14.4 Normalisation across carriers

Carriers differ by orders of magnitude in typical values (kW electricity versus MWh seasonal heat storage). Per-carrier standardisation is the minimum; consider physical non-dimensionalisation (fractions of capacity, fractions of peak demand), which additionally helps transfer across systems of different sizes.

### 14.5 Synthetic and archetype-derived data — what it buys and what it does not

Simulator-generated corpora have one decisive advantage over public measured datasets: they are **fully labelled**. Each record pairs a known system description with its outputs. Public building load collections provide profiles without ground-truth attributes, which makes them unsuitable for any controlled study of representation, because the input side of the mapping is missing.

The corresponding limitation must be stated wherever this data is used: **archetype-derived data supports interpolation across archetype space, which is not the same as generalisation to real heterogeneity.** A model that performs well across simulated archetypes has demonstrated something narrower than it appears. Where possible, validate against measurements from real instances, and report how many and how diverse.

A second inherited limitation: the corpus absorbs the generating optimiser's assumptions — cost curves, discount rates, technology sets. Changing any of them requires regenerating the data, and the model silently encodes the originals until you do.

## 15. Enforcing physics

Four mechanisms, in increasing order of strength and cost:

| Mechanism | How | Guarantee | Cost |
| :--- | :--- | :--- | :--- |
| **Soft penalty** | add constraint violation to loss | none | free |
| **Architectural** | design outputs so constraints hold by construction (bounded decoders, softmax splits) | exact for what is encoded | low |
| **Projection / repair** | post-process onto feasible set | exact | moderate |
| **Exact encoding in solver** | encode NN as MILP constraints | exact + optimality | high |

Notes from practice:

- Bounded decoders and physics-informed regularisation preserve operational feasibility in GNN-based OPF, but residual violations may still require post-processing for strict feasibility.
- Physics-informed approaches embedding multi-physics dynamic constraints in the loss enable physically consistent solutions with limited training samples and improve accuracy under sparse data — a valuable property when simulator runs are expensive.
- Feasibility-restoration layers are an active area; repair layers for networks with hard constraints are being developed as reusable components.

**Recommendation for multi-carrier energy systems:** architectural enforcement of per-carrier energy balance (make the outputs sum correctly by construction), plus soft penalties for inequality constraints, plus a projection step if hard feasibility is required downstream.

## 16. Evaluation protocol

A credible protocol reports all six. Reporting only the first is the most common weakness in this literature.

1. **Accuracy** — error on held-out instances, per carrier, per horizon
2. **Feasibility** — constraint violation rate and magnitude; energy balance residual
3. **Optimality gap** (Tier 3) — cost versus true optimum
4. **Speedup** — honestly reported, **including** data generation and any post-processing correction. Note the pattern in power systems where speedup is reported both before and after correction, with an order-of-magnitude difference between them.
5. **Transfer** — performance on unseen configurations/topologies; this is the actual foundation-model claim
6. **Calibration** — if probabilistic, are the intervals honest?

{: .note }
Where the domain community has an established accuracy measure, use it alongside generic ML metrics. For building energy, NRMSE and CV(RMSE) are the calibration measures practitioners already read, and reporting them costs nothing while substantially improving how the work lands.

### 16.1 Held-out design

Random splits overstate performance. Hold out along the axis you claim to generalise over:

- unseen **configurations** (Tier 1/2 claim)
- unseen **topologies** (Tier 2 claim)
- unseen **archetypes / typologies** (building-scale claim)
- unseen **weather years / climate regimes**
- unseen **scales** (train small, test large)

Note the caution from adjacent domains: models trained and evaluated primarily at one scale and horizon have largely untested ability to generalise across spatial and temporal scales.

## 17. Realistic budget expectations

At roughly CHF 30k/year materials:

| Feasible | Not feasible |
| :--- | :--- |
| Fine-tuning models in the 10M–500M parameter range | Pretraining a large model from scratch |
| 10³–10⁵ simulator runs for training data | 10⁷+ runs |
| Small scaling studies | Large architecture sweeps |
| Releasing a benchmark and dataset | Sustained large-scale compute |

{: .important }
**The honest deliverable at this budget is: a representation, a dataset, a benchmark, and a demonstrated small model — not a large trained foundation model.** Framing matters: *"we establish what a foundation model for this domain requires, and demonstrate feasibility"* is credible and fundable. *"We build a foundation model"* is not, at this budget, and reviewers who know the field will notice.

### 17.1 Publication format follows from the budget

The same logic applies to papers. For a novel concept with limited empirical results, three formats are available:

- **Pure empirical** — a benchmark, a baseline, a measurement. Safe with reviewers; low ceiling. Competent and rarely cited.
- **Pure concept / position** — argument only. High ceiling, but at an engineering venue it reads as a proposal unless it does real analytical work: a criterion others can apply, a taxonomy with consequences, falsifiable predictions, a benchmark specification.
- **Anchored concept paper (recommended)** — argument-led, with one demonstrative empirical result. Roughly three-quarters argument, one-quarter evidence. The argument carries the paper; a single result converts the central claim from assertion to demonstration.

The anchored format matches the budget reality above: it does not depend on a trained model existing by the deadline, and it fails gracefully — if training slips, the paper still stands; if it succeeds, a results subsection is added without restructuring.

**Audience translation is part of the format choice.** Writing FM concepts for a domain audience means introducing every ML idea through its domain counterpart ([§6.6](03-basic-elements.html#66-the-criterion) does this with discretisation), avoiding unexplained vocabulary, and including a short glossary. The test: if a paragraph requires ML background to parse, rewrite it.

---
[← Previous: Tier 3 — Design & Sizing](08-methods-tier3.html) · [Next: Open Gaps →](10-open-gaps.html)
