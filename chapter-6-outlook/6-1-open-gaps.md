---
title: "6.1 Open Gaps"
parent: Chapter 6 — Outlook
nav_order: 1
status: draft
last_reviewed: 2026-09-11
redirect_from: /10-open-gaps.html
---

# 6.1 Open Gaps
{: .no_toc }

{% include page-status.html %}

Ordered by how defensible they are as research contributions.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

### G1 — Multi-carrier temporal tokenisation

How to represent carriers whose characteristic times span minutes to seasons in one architecture without aliasing or loss of physical structure. Direct analogue of a documented unsolved problem in Earth-system coupling; no energy-domain treatment exists. Addressed directly by the temporal hierarchy proposed in [§5.5.2](../chapter-5-case-study/5-5-token-schema.html#552-temporal-hierarchy), though not yet validated at scale.

### G2 — Cross-configuration transfer for multi-energy operation

Existing surrogates are bespoke; no work tailors the ML procedure to multi-energy properties, and small-data regimes dominate. Power systems has made this move ([§2.4.2](../chapter-2-fm-foundations/2-4-2-power-grid-fms.html)); multi-carrier urban systems have not.

### G3 — Constrained state variables over long horizons

Storage state of charge as a slow, bounded, path-dependent variable. Not handled by any general time-series foundation model. See [§4.9.1(a)](../chapter-4-directions/4-9-1-methods-tier1.html#where-the-genuine-research-contribution-sits).

### G4 — Benchmarks

None exist for urban multi-carrier operation or design. This is the cheapest high-value artifact available and the one most likely to outlive its author. See [Phase 0](../chapter-5-case-study/5-1-roadmap.html#phase-0-year-01--representation-and-the-data-engine) and the downstream benchmark suite in [§5.7](../chapter-5-case-study/5-7-module-decomposition.html).

### G5 — Feasibility guarantees for multi-carrier design surrogates

Established for power flow; open for multi-carrier hubs with discrete decisions. See [§4.9.3](../chapter-4-directions/4-9-3-methods-tier3.html).

### G6 — Assumption representation

Not a foundation-model problem (see [§4.7](../chapter-4-directions/4-7-reading-the-screen.html)) but the binding constraint on any corpus built from *published studies* rather than simulator output: two models with identical structure and data give different answers because of choices documented nowhere. A corpus without this layer trains on a confounded signal.

### G7 — Verification of agent-built models

As natural-language model setup commoditises, the open problem shifts from generation to verification — whether the assumptions an agent silently chose were defensible. The field's own vocabulary has moved toward verifiable agentic AI and reliability benchmarking. See [§4.3](../chapter-4-directions/4-3-llm-agents-for-simulation.html).

### G8 — The basic element for buildings, and the zoning ambiguity underneath it

No building decomposition satisfies the four requirements of [§2.3.1](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html#231-the-criterion). The most principled option — the building as a network of connected parts (R3) — is blocked because thermal zoning is a modelling convention rather than a property of the building. Resolving this is a building simulation problem before it is a machine learning one, which makes it unusually well suited to that community and unusually unlikely to be solved by the ML community first. Defensible as a research contribution on its own.

### G9 — Representing a decision space alongside a state space

Every existing energy foundation model represents what a system *is* or *does*. None represents what could be *done to it* — the discrete, combinatorial, constraint-bound space of possible interventions. This is required for any FM targeting retrofit, investment or design support (Tier 3, [§4.9.3](../chapter-4-directions/4-9-3-methods-tier3.html)), has no counterpart in the grid literature to borrow from, and is the least developed question in this book. See also [§4.4 Generative Design](../chapter-4-directions/4-4-generative-design.html).

---
[← Back to Chapter 6](index.html) · [Next: 6.2 How to Contribute →](6-2-how-to-contribute.html)
