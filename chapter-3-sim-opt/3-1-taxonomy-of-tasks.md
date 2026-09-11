---
title: "3.1 Taxonomy of Modelling Tasks"
parent: Chapter 3 — Simulation and Optimisation in UES
nav_order: 1
status: draft
last_reviewed: 2026-09-11
---

# 3.1 Taxonomy of Modelling Tasks
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

Each row is a distinct *task* with a distinct mathematical structure — and foundation-model potential differs sharply between them. This table is used again in [§4.6 Screening the Tasks](../chapter-4-directions/4-6-screening-tasks.html).

| # | Task | Question answered | Mathematical object | Typical runtime |
| :--- | :--- | :--- | :--- | :--- |
| T1 | **Demand modelling (UBEM)** | How much energy does this building stock need, when? | DAE / RC networks / statistical regression | minutes–hours (stock) |
| T2 | **Renewable resource assessment** | How much PV/solar/wind is available here? | geometric + radiative computation | seconds–hours |
| T3 | **Forecasting** | What will demand/generation be in the next hours–days? | time-series regression | milliseconds–seconds |
| T4 | **Dispatch / operation optimisation** | Given a fixed system, how should it run? | LP / MILP | sub-second–hours |
| T5 | **Design / sizing optimisation** | What should we build, and how big? | MILP / MINLP / bilevel | minutes–days |
| T6 | **Network simulation** | Do flows, pressures, temperatures and voltages hold? | nonlinear algebraic / PDE / DAE | seconds–hours |
| T7 | **Control** | What setpoints now, given uncertainty? | MPC / RL | real-time constraint |
| T8 | **Scenario & pathway analysis** | What futures are plausible, under what assumptions? | recursive optimisation + narrative | hours–days |
| T9 | **Impact assessment** | Emissions, cost, equity, comfort outcomes | post-processing / LCA | seconds–hours |

## Notes on each task's structure

**T1 — Demand modelling.** Bottom-up physics-based Urban Building Energy Modelling (UBEM) simulates buildings at large scale from geometry, envelope and usage archetypes. Reviews of these tools compare them along required inputs, reported outputs, workflow, applicability and intended users — and note that choosing a tool while balancing complexity, accuracy, usability and computing needs remains a genuine challenge for users. A persistent and important weakness: occupant behaviour. Inappropriate choice of occupant-behaviour model can lead to oversized district energy systems, over-investment and low operational efficiency — one of the main causes of the building "performance gap".

{: .note }
T1 also carries a representation problem the other tasks do not, because the decomposition of a building into elements is itself a modelling choice rather than a property of the object. See [§2.3 Choosing a Basic Element](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html).

**T4 — Dispatch.** Usually LP if conversion efficiencies are linear and no on/off decisions are needed; MILP once unit commitment, minimum part-load, or discrete states enter. This is the workhorse: it is the inner object of T5, T7 and T8. Treated as an ML problem shape in [§3.4](3-4-dispatch-optimisation.html).

**T5 — Design/sizing.** The literature consolidates around deterministic programming (LP/MILP/MINLP) for transparent, reproducible co-optimisation of capacity investment and operational dispatch, alongside evolutionary and swarm methods for nonconvex, mixed-variable, simulation-driven sizing problems — while flagging the need for rigorous constraint handling and transparent reporting of computational budgets. Hybrid strategies that integrate global search with exact dispatch solvers, surrogate-assisted learning, decomposition and control–co-design are identified as the most promising direction. Treated in [§3.5](3-5-design-sizing-optimisation.html).

**T6 — Networks.** Electrical (AC/DC power flow), thermal (hydraulics + heat transfer, with transport delays), gas (pressure dynamics). These are where genuine PDE/DAE structure lives, and where runtimes explode.

---
[← Back to Chapter 3](index.html) · [Next: 3.2 Building Energy Simulation →](3-2-building-simulation-data.html)
