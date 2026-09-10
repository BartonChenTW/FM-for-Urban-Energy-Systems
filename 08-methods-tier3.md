---
title: IV. Tier 3 — Design & Sizing
nav_order: 9
---

# Tier 3 — Design and Sizing Optimisation
{: .no_toc }

1. TOC
{:toc}

---

## 13.1 Why this is structurally different

Tiers 1 and 2 approximate a **simulation**: given inputs, predict outputs. Tier 3 approximates an **optimisation**: given a problem instance, predict the optimal decision.

The canonical structure is bilevel or two-stage:

```
outer:  choose capacities x  →  minimise  investment(x) + operating_cost(x)

inner:                              operating_cost(x) = min over dispatch, subject to physics
```

The inner problem is called once per candidate design. With evolutionary or many-objective outer search, that is 10³–10⁶ dispatch solves. **This is the single most expensive loop in the domain and the clearest justification for surrogate work.**

Characteristically, evaluating the value function and gradient of the inner-loop optimisation is computationally expensive — which is the general statement of the difficulty.

{: .note }
Tier 3 is also where the decision layer of [§6.7](03-basic-elements.html#67-basic-elements-for-buildings) becomes unavoidable. The model must represent the space of possible designs, not only system states. This is logged as [G9](10-open-gaps.html#g9) and is the least-developed representation question in this document.

## 13.2 Three families of method

**Family 1 — Surrogate the inner objective (most established).** Learn a mapping from design vector → operating cost (and other objectives), then run the outer search against the surrogate. This has direct precedent in energy hubs: an ANN-based surrogate combined with actual engineering models for system sizing optimisation in energy hubs; a later variant using supervised and transfer learning to bypass the computationally intensive engineering model, adaptable across scenarios with different solar and wind potentials. The same approach has been applied at national scale, surrogating EnergyPLAN to speed up country-level optimisation.

*Strength:* simple, proven. *Weakness:* one surrogate per system — the bespoke trap. **The foundation-model contribution would be making this transferable across systems rather than rebuilt each time.**

**Family 2 — Learn the solution map (amortised optimisation).** Learn instance → optimal decision directly. Fast, because the solver is bypassed entirely. Direct approaches learn a mapping between grid parameters and the OPF solution and are typically much faster than conventional solvers or hybrid approaches, **but offer no feasibility guarantees**.

**Family 3 — Hybrid (recommended default).** Predict information that helps a conventional solver converge faster — warm starts, active-set prediction, variable fixing. Hybrid approaches predict information to help a conventional optimisation solver converge to a solution faster, retaining the solver's guarantees.

A particularly clean pattern worth studying: replace only the *physics constraints* with a learned surrogate while preserving the optimisation backbone and all remaining constraints. One implementation learns only the voltage–power mapping, circumventing the feasibility and generalisation issues of end-to-end approaches while requiring substantially less training data, and encodes the neural network exactly as MILP via Big-M constraints, preserving global optimality guarantees of the surrogate-constrained problem — unlike penalty- or projection-based feasibility restoration. Reported result: sub-second solve times on a realistic LV network with PV, EVs and heat pumps.

**For multi-energy design, Family 3 is the sensible default**, because design decisions carry investment consequences and silent infeasibility is unacceptable.

{: .important }
**Practical corollary for building retrofit.** A surrogate imitating a constrained optimiser inherits that optimiser's constraints only implicitly. It can therefore propose measures a specific instance cannot accept: PV without sufficient roof area, a heat pump beyond the electrical connection limit. This is a deployment risk rather than an academic nitpick, and any decision-support application needs a stated handling — post-hoc constraint filtering, inference-time masking, or reporting violation rate as a headline metric alongside accuracy.

## 13.3 The amortisation argument

**This is the argument that justifies foundation-model framing over bespoke surrogates, and it must be made explicitly.**

Building a training set costs *N* simulator runs. If *N* = 10,000 and each run takes a minute, that is roughly a week of compute before anything is returned. A surrogate for **one** system used within **one** study rarely repays this — which is precisely why the existing multi-energy surrogate literature is bespoke, small-data and discarded at project end.

A foundation model changes the arithmetic: the cost is paid once, across a distribution of systems, and amortised over every subsequent study. Formally, it pays back when

```
N_train × t_sim  <  Σ over future studies ( N_evaluations × t_sim )
```

**Corollary that matters institutionally:** this is also the succession argument. A model that speeds up every future study creates ongoing dependence, which is the strongest mechanism by which research infrastructure survives its author.

{: .warning }
**Caveat.** The arithmetic only holds if the model actually transfers. Amortisation assumes reuse across systems, and reuse depends on the basic element satisfying [§6.6](03-basic-elements.html#66-the-criterion). Where it does not, what looks like a foundation model is a collection of memorised cases and the payback never arrives. **Check the representation before running the amortisation calculation.**

## 13.4 Scaling behaviour

Recent power-systems work establishes both scaling laws of machine learning for optimal power flow and data scaling laws for multi-task energy system intelligence with limited fine-tuning. **Before committing to a large data-generation campaign, run a small scaling study**: train on 10², 10³, 10⁴ samples and fit the error curve. This tells you the required *N* rather than guessing, and it is cheap.

---
[← Previous: Tier 2 — Multi-Hub, Multi-Carrier](07-methods-tier2.html) · [Next: Building It →](09-building-it.html)
