---
title: "4.4 Generative Design"
parent: Chapter 4 — Directions for FMs in UES
nav_order: 4
status: draft
last_reviewed: 2026-09-11
---

# 4.4 Generative Design
{: .no_toc }

{% include page-status.html %}

{: .note }
**Stub — needs expansion.** This section states the direction and how it differs from the rest of this book's treatment of design/sizing. It does not yet survey specific generative-design implementations for energy systems.

1. TOC
{:toc}

---

## The direction

[§3.5](../chapter-3-sim-opt/3-5-design-sizing-optimisation.html) and [§4.9.3 (Tier 3)](4-9-3-methods-tier3.html) treat design and sizing as an *optimisation* problem: search a space of candidate designs (device choices, capacities, topology) and return the best one against a stated objective. **Generative design** is a related but distinct framing: rather than searching a fixed decision space for an optimum, a generative model proposes novel candidate designs directly — sampling from a learned distribution over plausible system configurations, potentially including topologies or technology combinations not explicitly enumerated in advance.

This distinction matters because it changes what the model needs to represent. Tier 3's amortised-optimisation approaches ([§4.9.3](4-9-3-methods-tier3.html)) predict *within* a decision space that is defined and bounded ahead of time. A generative approach needs the decision space itself to be represented well enough that sampling from it produces valid, buildable designs — which is a direct application of the **decision space** problem named in [§2.3.2](../chapter-2-fm-foundations/2-3-choosing-a-basic-element.html) and logged as [gap G9](../chapter-6-outlook/6-1-open-gaps.html#g9).

## Relationship to the rest of this book

Generative design for energy systems is the design-space analogue of what diffusion and other generative models already do for images[^ho2020ddpm] and molecules:[^hoogeboom2022edm] propose plausible new instances rather than only score given ones. No existing energy foundation model surveyed in [§2.4](../chapter-2-fm-foundations/2-4-existing-fms-relevant-to-energy.html) attempts this for multi-carrier hub design; it is a genuinely open direction rather than an established one.

## What would need to be added here

- A survey of generative design approaches in adjacent engineering domains (structural design, mechanical design) that could plausibly transfer.
- Discussion of feasibility: a generatively-proposed design still needs the feasibility guarantees discussed in [§4.9.3](4-9-3-methods-tier3.html) — a generated device combination that cannot actually be built or connected is not useful.
- How this direction would interact with the decision-space representation problem in [G9](../chapter-6-outlook/6-1-open-gaps.html#g9), which is currently unsolved rather than merely under-explored.

[^ho2020ddpm]: Ho, J., Jain, A., Abbeel, P. (2020). [Denoising diffusion probabilistic models](https://arxiv.org/abs/2006.11239). NeurIPS 2020. arXiv:2006.11239
[^hoogeboom2022edm]: Hoogeboom, E., Satorras, V. G., Vignac, C., Welling, M. (2022). [Equivariant diffusion for molecule generation in 3D](https://arxiv.org/abs/2203.17003). ICML 2022. arXiv:2203.17003

---
[← Previous: 4.3 LLM Agents for Simulation](4-3-llm-agents-for-simulation.html) · [Next: 4.5 Screening: Which Sub-Fields Fit the FM Pattern →](4-5-screening-fields.html)
