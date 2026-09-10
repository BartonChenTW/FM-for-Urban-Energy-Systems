---
title: VI. Open Gaps
nav_order: 11
---

# Part VI — Open Gaps
{: .no_toc }

Ordered by how defensible they are as research contributions.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

---

### G1 — Multi-carrier temporal tokenisation

How to represent carriers whose characteristic times span minutes to seasons in one architecture without aliasing or loss of physical structure. Direct analogue of a documented unsolved problem in Earth-system coupling; no energy-domain treatment exists.

### G2 — Cross-configuration transfer for multi-energy operation

Existing surrogates are bespoke; no work tailors the ML procedure to multi-energy properties, and small-data regimes dominate. Power systems has made this move; multi-carrier urban systems have not.

### G3 — Constrained state variables over long horizons

Storage state of charge as a slow, bounded, path-dependent variable. Not handled by any general time-series foundation model.

### G4 — Benchmarks

None exist for urban multi-carrier operation or design. This is the cheapest high-value artifact available and the one most likely to outlive its author.

### G5 — Feasibility guarantees for multi-carrier design surrogates

Established for power flow; open for multi-carrier hubs with discrete decisions.

### G6 — Assumption representation

Not a foundation-model problem (see [§10](05-screening.html#10-reading-the-screen)) but the binding constraint on any corpus built from *published studies* rather than simulator output: two models with identical structure and data give different answers because of choices documented nowhere. A corpus without this layer trains on a confounded signal.

### G7 — Verification of agent-built models

As natural-language model setup commoditises, the open problem shifts from generation to verification — whether the assumptions an agent silently chose were defensible. The field's own vocabulary has moved toward verifiable agentic AI and reliability benchmarking.

### G8 — The basic element for buildings, and the zoning ambiguity underneath it

No building decomposition satisfies the four requirements of [§6.6](03-basic-elements.html#66-the-criterion). The most principled option — the building as a network of connected parts (R3) — is blocked because thermal zoning is a modelling convention rather than a property of the building. Resolving this is a building simulation problem before it is a machine learning one, which makes it unusually well suited to that community and unusually unlikely to be solved by the ML community first. Defensible as a research contribution on its own.

### G9 — Representing a decision space alongside a state space

Every existing energy foundation model represents what a system *is* or *does*. None represents what could be *done to it* — the discrete, combinatorial, constraint-bound space of possible interventions. This is required for any FM targeting retrofit, investment or design support (Tier 3), has no counterpart in the grid literature to borrow from, and is the least developed question in this document.

---
[← Previous: Building It](09-building-it.html) · [Next: Glossary →](appendix-a-glossary.html)
