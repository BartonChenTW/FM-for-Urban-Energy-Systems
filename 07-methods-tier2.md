---
title: IV. Tier 2 — Multi-Hub, Multi-Carrier
nav_order: 8
---

# Tier 2 — Multi-Hub, Multi-Carrier, Dispatch Only
{: .no_toc }

1. TOC
{:toc}

---

## 12.1 What changes

Topology enters as a variable. You now have a **heterogeneous graph**: hub nodes, conversion nodes, storage nodes, demand nodes, connected by carrier-specific edges (electrical lines, heat pipes, gas mains) with their own physical properties and losses.

The learning problem becomes: *given a graph and boundary conditions, predict the operational state on that graph* — including for graphs never seen in training.

## 12.2 Architecture family: graph neural networks

The power-systems community has developed this thoroughly and the lessons transfer directly.

**Heterogeneous message passing is the right default.** Recent work proposes Hybrid Heterogeneous Message Passing Neural Networks for AC-OPF that explicitly model power system components as distinct node and edge types, specifically to address topology adaptability and scalability. In multi-carrier systems the heterogeneity is even more pronounced — a heat pipe and a power line are not the same edge type in any useful sense.

**Local message passing plus global attention.** A representative design performs type-specific local message passing over heterogeneous graphs and applies a global Transformer only on bus nodes, capturing system-wide correlations efficiently. This hybrid pattern is worth copying: message passing handles local physics, attention handles system-wide coupling.

**Positional encoding matters and should be physical.** Effective-resistance positional encodings and resistance-biased attention enhance electrical awareness in this setting. The multi-carrier analogue is an open question — what is the "effective resistance" of a heat network? Thermal transport delay and pipe conductance are candidates.

## 12.3 Topology generalisation — the core claim of this tier

This is where a foundation-model framing earns its name. Reported results in power systems: models generalise to thousands of unseen N-1 contingency topologies without retraining, with up to 190× speedup versus interior-point solvers before power-flow correction and over 10× after, on 2000-bus systems.

Also relevant: topology-informed GNNs are described as very friendly to transfer to a new topology with slight modification of the pre-trained graph filter, with a short re-training step on new post-contingency data quickly restoring accuracy.

**For multi-carrier systems this has not been done.** That is the gap.

{: .note }
This is R3 (see [§6.8](03-basic-elements.html#68-representation-strategies-and-testable-predictions)) applied at network scale, and it works here precisely because the network element is unambiguous. The same strategy applied *within* a building runs into the zoning problem of [§6.7(b)](03-basic-elements.html#67-basic-elements-for-buildings), which is why R3 is more principled and less available at building scale than at district scale.

## 12.4 Time and graph together

Tier 2 requires both dimensions. Three composition strategies:

| Strategy | How | Trade-off |
| :--- | :--- | :--- |
| **Spatial-then-temporal** | GNN encodes graph per timestep → sequence model over embeddings | Simple, modular; may lose fast spatiotemporal coupling |
| **Temporal-then-spatial** | Encode each node's series → GNN over node embeddings | Efficient; weaker on propagating transients |
| **Joint spatiotemporal attention** | Attention over (node, time) jointly | Most expressive; quadratic cost, needs care |

For district multi-carrier systems with slow thermal transport, spatial-then-temporal is usually the pragmatic starting point.

## 12.5 The alternative: neural operators

If the network physics is genuinely continuous — thermal transport in pipes, pressure dynamics — **operator learning** is the other credible family. DeepONet learns solution operators of governing equations and solves a family of parametric PDEs, rather than a single instance; Fourier Neural Operators learn mappings between function spaces rather than finite-dimensional mappings.

Reported performance in adjacent thermal problems is strong: neural operator models achieving maximum temperature-field prediction errors below 5% with prediction times at the second level, a four-order-of-magnitude acceleration versus CFD.

A practically important pattern: **latent operator learning**. High-dimensional simulation data contains redundant features that induce the curse of dimensionality; because physical constraints confine the data to a lower-dimensional manifold, a reduced-order model can extract essential features first, with the operator learned in the compact latent space. Combining an autoencoder with DeepONet (L-DeepONet) is the concrete realisation.

**When to choose which:** GNN if the object is genuinely a discrete network with device-level decisions; neural operator if the object is a continuous field (temperature along pipes, pressure). District heating with detailed hydraulics is arguably both, and hybrids are an open research direction.

---
[← Previous: Tier 1 — Single Hub Dispatch](06-methods-tier1.html) · [Next: Tier 3 — Design & Sizing →](08-methods-tier3.html)
