---
title: "1.1 What an Urban Energy System Contains"
parent: Chapter 1 — Background
nav_order: 1
status: draft
last_reviewed: 2026-09-11
redirect_from: /01-the-domain.html
---

# 1.1 What an Urban Energy System Contains
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

An urban energy system is a spatially bounded set of energy demands, conversion technologies, storage, and networks, coupled across multiple energy carriers. The scales usually distinguished:

| Scale | Typical extent | What dominates |
| :--- | :--- | :--- |
| Building | one building | envelope physics, HVAC, occupant behaviour |
| Block / cluster | 5–50 buildings | shared supply, local networks, diversity effects |
| District | 50–5,000 buildings | network topology, district heating/cooling, storage |
| City | 10⁴–10⁶ buildings | aggregation, spatial heterogeneity, transport coupling |
| Region / national | many cities | policy, imports/exports, macro-scenarios |

The defining feature versus classical power systems: **multiple carriers, coupled**. Electricity, heat (often at several temperature levels), cooling, gas, hydrogen, and increasingly mobility demand — interacting through conversion devices (CHP, heat pumps, electrolysers, boilers, chillers) and storage of different types.

The **energy hub** abstraction is the standard formalism: a node where multiple input carriers are converted, stored and dispatched to meet multiple output demands, represented by a coupling matrix mapping inputs to outputs.[^geidl2007opf] Most district-scale optimisation models are, structurally, either a single hub or a network of hubs.

[^geidl2007opf]: Geidl, M. and Andersson, G. (2007). [Optimal power flow of multiple energy carriers](https://doi.org/10.1109/TPWRS.2006.888988). *IEEE Transactions on Power Systems*, 22(1), 145–155.

---
[← Back to Chapter 1](index.html) · [Next: 1.2 FMs in One Page →](1-2-fms-in-one-page.html)
