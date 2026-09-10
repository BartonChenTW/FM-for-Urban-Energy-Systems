---
title: I. The Domain
nav_order: 2
status: draft
last_reviewed: 2026-09-10
---

# Part I — The Domain
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

## 1. What "urban energy system" contains

An urban energy system is a spatially bounded set of energy demands, conversion technologies, storage, and networks, coupled across multiple energy carriers. The scales usually distinguished:

| Scale | Typical extent | What dominates |
| :--- | :--- | :--- |
| Building | one building | envelope physics, HVAC, occupant behaviour |
| Block / cluster | 5–50 buildings | shared supply, local networks, diversity effects |
| District | 50–5,000 buildings | network topology, district heating/cooling, storage |
| City | 10⁴–10⁶ buildings | aggregation, spatial heterogeneity, transport coupling |
| Region / national | many cities | policy, imports/exports, macro-scenarios |

The defining feature versus classical power systems: **multiple carriers, coupled**. Electricity, heat (often at several temperature levels), cooling, gas, hydrogen, and increasingly mobility demand — interacting through conversion devices (CHP, heat pumps, electrolysers, boilers, chillers) and storage of different types.

The **energy hub** abstraction is the standard formalism: a node where multiple input carriers are converted, stored and dispatched to meet multiple output demands, represented by a coupling matrix mapping inputs to outputs. Most district-scale optimisation models are, structurally, either a single hub or a network of hubs.

## 2. Taxonomy of modelling tasks

Each row is a distinct *task* with a distinct mathematical structure — and foundation-model potential differs sharply between them. This table is used again in [Screening Tasks](05-screening.html).

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

### 2.1 Notes on each task's structure

**T1 — Demand modelling.** Bottom-up physics-based Urban Building Energy Modelling (UBEM) simulates buildings at large scale from geometry, envelope and usage archetypes. Reviews of these tools compare them along required inputs, reported outputs, workflow, applicability and intended users — and note that choosing a tool while balancing complexity, accuracy, usability and computing needs remains a genuine challenge for users. A persistent and important weakness: occupant behaviour. Inappropriate choice of occupant-behaviour model can lead to oversized district energy systems, over-investment and low operational efficiency — one of the main causes of the building "performance gap".

{: .note }
T1 also carries a representation problem the other tasks do not, because the decomposition of a building into elements is itself a modelling choice rather than a property of the object. See [Choosing a Basic Element](03-basic-elements.html).

**T4 — Dispatch.** Usually LP if conversion efficiencies are linear and no on/off decisions are needed; MILP once unit commitment, minimum part-load, or discrete states enter. This is the workhorse: it is the inner object of T5, T7 and T8.

**T5 — Design/sizing.** The literature consolidates around deterministic programming (LP/MILP/MINLP) for transparent, reproducible co-optimisation of capacity investment and operational dispatch, alongside evolutionary and swarm methods for nonconvex, mixed-variable, simulation-driven sizing problems — while flagging the need for rigorous constraint handling and transparent reporting of computational budgets. Hybrid strategies that integrate global search with exact dispatch solvers, surrogate-assisted learning, decomposition and control–co-design are identified as the most promising direction.

**T6 — Networks.** Electrical (AC/DC power flow), thermal (hydraulics + heat transfer, with transport delays), gas (pressure dynamics). These are where genuine PDE/DAE structure lives, and where runtimes explode.

## 3. The tool landscape

Not exhaustive, but covering the families you will meet. The point of this table is that **each family produces a different data structure**, which determines what a foundation model could consume.

| Family | Representative tools | Task coverage | Output structure |
| :--- | :--- | :--- | :--- |
| **Building simulation** | EnergyPlus, TRNSYS, IDA-ICE, ESP-r | T1, T7 | time series per zone/building |
| **UBEM** | CitySim, UMI, SimStadt, TEASER, CityBES, City Energy Analyst | T1, T2 | building-resolved time series + geometry |
| **Equation-based dynamic** | Modelica (Buildings, IBPSA, DisHeatLib), Dymola, OpenModelica | T1, T6, T7 | DAE trajectories, high resolution |
| **District/urban platforms** | PyCity, City Energy Analyst, eNeuron | T1, T4, T6 | multi-building energy flows |
| **Energy-system optimisation** | oemof, Calliope, PyPSA, SpineOpt, TIMES/MARKAL, EnergyPLAN, OSeMOSYS | T4, T5, T8 | dispatch + capacity decisions |
| **Energy-hub / multi-carrier** | ehubX, eNeuron, hub formulations in Calliope/oemof | T4, T5 | carrier-resolved dispatch |
| **Power system** | pandapower, PowerModels, MATPOWER, PyPSA | T4, T6 | bus/line-resolved states |
| **Co-simulation** | FMI/FMU, mosaik, HELICS | cross-task | coupled trajectories |

Tool reviews in this space distinguish **integrated** approaches (one solver, one formulation) from **co-simulation** approaches (separate sub-models exchanging data) — a distinction that matters for foundation models, because integrated tools produce coherent single-object outputs while co-simulation produces multiple loosely-coupled streams.

{: .note }
A second and more consequential way to read this table is **by the basic element each family commits to** — whole building, thermal zone, component, node/bus, or time series. That grouping, not the tool family, determines what a foundation model trained on the output can transfer. See [Choosing a Basic Element](03-basic-elements.html).

## 4. Where the computational cost actually is

Order-of-magnitude brackets. The spread is the point.

| Task/configuration | Typical runtime |
| :--- | :--- |
| LP dispatch, single node, typical days | sub-second – seconds |
| LP dispatch, full 8760 h, district | seconds – minute |
| MILP with unit commitment | minutes – hours |
| Dynamic physical (Modelica, DH hydraulics) | tens of minutes – hours |
| UBEM, full stock, annual | minutes – hours |
| Design optimisation with dispatch inner loop | hours – days |
| AC-OPF, large network | seconds, but called thousands of times |

{: .important }
**Single runs are usually affordable. Loops are not.** Design optimisation, uncertainty quantification across weather years, and Monte Carlo risk assessment all call an inner model 10³–10⁶ times. That is where surrogates and foundation models earn their keep — and where the [amortisation argument](08-methods-tier3.html#3-the-amortisation-argument) applies.

---
[← Back to Home](index.html) · [Next: FM Fundamentals →](02-fm-fundamentals.html)
