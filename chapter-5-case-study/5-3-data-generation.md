---
title: "5.3 Data Generation"
parent: Chapter 5 — Case Study
nav_order: 3
status: draft
last_reviewed: 2026-09-11
---

# 5.3 Data Generation
{: .no_toc }

{% include page-status.html %}

The general sampling-design guidance in [§4.10.1](../chapter-4-directions/4-10-building-it.html#4101-data-generation-and-sampling-design) applies unchanged to this case study. This page adds what is specific to the multi-carrier hub representation proposed in [§5.4](5-4-concrete-representation.html) and [§5.5](5-5-token-schema.html).
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

## Perturbation axes specific to this representation

Beyond the general axes in [§4.10.1](../chapter-4-directions/4-10-building-it.html#4101-data-generation-and-sampling-design) (configurations, boundary conditions, operating regimes), the token schema in [§5.5](5-5-token-schema.html) implies specific axes that must be covered for the representation itself to be exercised, not just the physics:

- **Device vocabulary coverage** — every technology class in the fixed vocabulary (§5.5) needs enough instances, at enough different capacities and part-load points, that the model learns the class embedding rather than memorising individual devices.
- **Topology variety** — bipartite graphs with varying numbers of carrier-buses and devices, varying port connectivity, so the model does not overfit to one district's specific graph shape (this is the direct analogue of the topology-generalisation claim in [§4.9.2](../chapter-4-directions/4-9-2-methods-tier2.html)).
- **Carrier-quality boundary cases** — scenarios that exercise the quality-ordering constraint (§5.5, §5.6) at its edges, e.g. heat pumps operating near their COP breakpoints, so the no-upgrade penalty is actually trained against informative examples rather than only the easy interior of the feasible region.
- **Seasonal storage cycles** — full annual cycles for any device with `state_active: true` (§5.5), since the L1/L2 temporal hierarchy exists specifically to let the model learn cross-season coupling; a corpus that only ever samples partial years cannot exercise this.

## Dispatch label generation: not only cost-optimal

Per [Phase 1 of the roadmap](5-1-roadmap.html#phase-1-year-13--simulation-surrogate-deliberately-not-optimisation), the data engine must generate **rule-based and perturbed-optimal dispatch**, not only cost-optimal dispatch. Cost-optimal dispatch is degenerate under the coupling-matrix formalism ([§3.3](../chapter-3-sim-opt/3-3-energy-hub-formalism.html)): many solutions achieve the same objective, so imitating a solver teaches an arbitrary tiebreak that will not generalise (see [risk 1](5-8-risks.html#581-five-risks-most-likely-to-kill-the-programme)). Perturbing away from optimality gives a smooth, learnable manifold instead.

## What survives if the trained model is thrown away

Consistent with the budget realism in [§4.10.4](../chapter-4-directions/4-10-building-it.html#4104-realistic-budget-expectations): the honest, durable deliverable of this phase is the data-generation engine and the benchmark set from [Phase 0](5-1-roadmap.html#phase-0-year-01--representation-and-the-data-engine) itself, independent of whether any specific trained model succeeds.

---
[← Previous: 5.2 The Representation Problem](5-2-representation-problem.html) · [Next: 5.4 A Concrete Proposed Representation →](5-4-concrete-representation.html)
