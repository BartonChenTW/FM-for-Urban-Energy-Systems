---
title: "4.3 LLMs and Agents That Build or Run Simulation Models"
parent: Part 4 — Directions for FMs in UES
nav_order: 3
status: draft
last_reviewed: 2026-09-11
---

# 4.3 LLMs and Agents That Build or Run Simulation Models
{: .no_toc }

{% include page-status.html %}

{: .note }
**Stub — needs expansion.** This section states the direction and its connection to an open gap already logged elsewhere in this book. It does not yet survey specific tools or agent frameworks.

1. TOC
{:toc}

---

## The direction

Everything elsewhere in this book treats a foundation model as something that predicts a *quantity* — a trajectory, a cost, a decision. A structurally different direction uses a large language model, generally used agentically (able to call tools, write and run code, inspect results, and iterate), to **produce or operate the simulation itself**: setting up an EnergyPlus or Modelica model from a natural-language description of a building, configuring an energy-hub optimisation from a project brief, or driving an existing tool's API to explore a design space without a human writing the configuration by hand.

This is not the same claim as the rest of this book. Elsewhere, an FM is trained to approximate what a simulator or solver would output. Here, the model is generating the *inputs* to a conventional simulator or solver — assumptions, geometry, topology, parameter choices — which then runs unchanged. The two are complementary: an agent could plausibly configure a model whose dispatch is then evaluated by one of this book's Tier 1–3 approaches ([§4.9](4-9-methods-landing.html)).

## Why this matters, and the problem it creates

As natural-language model setup commoditises, the interesting question shifts from *generation* to *verification*: were the assumptions an agent silently chose — occupancy schedules, default U-values, a discretisation, a technology default — actually defensible for the case at hand? This is exactly **[gap G7](../part-6-outlook/6-1-open-gaps.html#g7)**, verification of agent-built models, logged in [Part 6](../part-6-outlook/index.html). The field's own vocabulary has moved toward verifiable agentic AI and reliability benchmarking, which is the right frame for judging this direction rather than treating it as a solved convenience.

## What would need to be added here

- A survey of existing tools and prototypes in this space (natural-language-to-simulation-model pipelines for building or energy-hub simulation), with an honest account of how mature any of them actually are.
- A worked example of where an agent-configured model's silent assumptions diverged from a domain expert's, to make the verification problem concrete rather than abstract.
- Discussion of what a verification protocol for agent-built energy models would need to check, connecting to the evaluation protocol in [§4.10](4-10-building-it.html).

---
[← Previous: 4.2 FMs for Whole Building Stocks](4-2-fms-for-building-stocks.html) · [Next: 4.4 Generative Design →](4-4-generative-design.html)
