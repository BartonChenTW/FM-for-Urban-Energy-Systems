---
title: VII. Reference Pointers
nav_order: 15
---

# Part VII — Reference Pointers

Grouped by what they are useful for. URLs given where they were retrieved directly.

### Domain reviews

- Review of modelling approaches and tools for district-scale energy system simulation — covers multi-disciplinary tools (TRNSYS, Modelica, CitySim, SynCity). *Renewable and Sustainable Energy Reviews.*
- Energy system planning and analysis software — comprehensive meta-review with attention to urban energy systems and district heating. *Energy* (2024).
- Multi-domain urban-scale energy modelling tools: a review — classifies tools by co-simulation versus integrated approach. *Sustainable Cities and Society* (2019).
- UBEM tools: state-of-the-art review of bottom-up physics-based approaches — arXiv:2103.01761.
- District energy models: comparative assessment of features and criteria for tool selection. *Energy and Buildings* (2024).
- Comparative analysis of simulation tools for advanced control algorithms in building energy management — covers PyCity, eNeuron. *Frontiers in Energy Efficiency* (2026).

### Time-series foundation models

- Chronos / Chronos-2 (Ansari et al., 2024/2025); Moirai / Moirai 2.0 (Woo et al., 2024; Liu et al., 2025); TimesFM (Das et al., 2024); Lag-Llama (Rasul et al., 2024); TabPFN-TS (Hoo et al., 2025); TiRex (Auer et al., 2025); Time-MoE, Toto, MOMENT, Timer, TTM.
- UniCA: Unified Covariate Adaptation for Time Series Foundation Models — arXiv:2506.22039.
- Investigating simple target–covariate relationships for Chronos-2 and TabPFN-TS — arXiv:2605.12200. *(On whether covariates are genuinely used.)*
- Deployment/production notes on Chronos, Moirai, TimesFM, Lag-Llama including long-horizon degradation behaviour — Spheron (2026).

### Tabular foundation models

- TabPFN (Hollmann et al., 2022; 2025) — prior-data fitted network; in-context inference on tabular data; cell-level representation with row-wise and column-wise attention.
- TabPFN v2 — randomised feature-token mechanism for heterogeneous feature spaces; transfer across datasets with differing feature semantics. See also "A Closer Look at TabPFN v2" — arXiv:2502.17361.
- TabPFN-2.5 (Grinsztajn et al., 2025) — in-context learning scaled to ~50,000 samples and ~2,000 features.
- TabICL (Qu et al., 2025/2026) — column-then-row attention, attention-fading correction; two-stage architecture reaching ~500,000 samples. arXiv:2502.05564.
- Context-Constrained Transfer Learning for Tabular Foundation Models via Data Distillation — arXiv:2607.04809. *(Distribution-shift sensitivity and negative transfer; context-length bounds.)*
- On the Uncertainty Quantification Ability of Tabular Foundation Models — arXiv:2606.01427.
- Tabular FM applied outside tabular domains: graph node classification as a tabular problem (Hayler et al., 2025); molecular property prediction (Pinto, 2025); MultiModalPFN (Kim et al., 2026, CVPR).

### Power systems ML — the closest analogue

- LUMINA: A Grid Foundation Model for Benchmarking AC Optimal Power Flow Surrogate Learning — arXiv:2605.02133.
- Scaling Laws of Machine Learning for Optimal Power Flow — arXiv:2601.02706.
- Unlocking Multi-Task Electric Energy System Intelligence: Data Scaling Laws and Performance with Limited Fine-Tuning — arXiv:2503.20040. *(Float tokenisation.)*
- Towards Generalization of Graph Neural Networks for AC-OPF (HH-MPNN) — arXiv:2510.06860.
- Topology-aware GNNs for Learning Feasible and Adaptive AC-OPF Solutions — arXiv:2205.10129.
- Enhanced OPF Using a Trained Neural Network Surrogate for Distribution Grid Constraints — arXiv:2604.12422. *(Exact MILP encoding via Big-M.)*
- Optimization with Neural Network Feasibility Surrogates — *Energies* 16(16):5913.
- Operational risk quantification using GNN surrogates of DC-OPF. *Energy and AI* (2025).
- SnareNet: Flexible Repair Layers for Neural Networks with Hard Constraints — arXiv:2602.09317.
- Foundation models for the electric power grid — *Joule* (2024). *(The perspective paper; the reference point for the grid-to-buildings analogy.)*
- ML-OPF wiki — maintained bibliography: energy.hosting.acm.org/wiki

### Surrogates for energy system design

- Perera et al. — ANN surrogate + engineering models for energy hub sizing (2017); transfer-learning surrogate for design optimisation (2019, 2020).
- Machine learning as a surrogate model for EnergyPLAN — country-level speedup. *Energy* (2024).
- Surrogate-assisted multi-criteria operation evaluation of community integrated energy systems — notes absence of MES-tailored ML procedures; Mixture-of-Experts, upsampling, non-linear rescaling. *Energy Conversion and Management: X.*
- Physics-informed neural network surrogate for coupled multi-energy systems in smart grids. *Expert Systems with Applications* (2025).

### Neural operators

- Li et al., Fourier Neural Operator for parametric PDEs — arXiv:2010.08895.
- Lu et al., DeepONet — *Nature Machine Intelligence* 3:218–229 (2021).
- Wang, Wang & Perdikaris, physics-informed DeepONets — *Science Advances* 7:eabi8605 (2021).
- Neural Operator-Based Surrogate for CFD with latent DeepONet (ROM + operator learning) — arXiv:2605.30277.
- FNO for rapid prediction of 3D indoor airflow dynamics. *Building Simulation* (2025).

### Foundation-model representation issues

- Toward AI-Enabled Earth System Coupling — arXiv:2604.03289. *(Tokenisation across incompatible discretisations; rare-regime under-representation; untested cross-scale generalisation.)*
- Representation Learning of Structured Data for Medical Foundation Models (UniStruct) — arXiv:2410.13351. *(Why standard tokenisation fails on structured codes.)*
- Foundation models for clean energy forecasting: a comprehensive review. *Renewable and Sustainable Energy Reviews* (2025).
- UrbanFM: Scaling Urban Spatio-Temporal Foundation Models — arXiv:2602.20677.

### Building-side benchmarks and datasets

- BuildingsBench (NREL) — load forecasting benchmark; profiles without paired ground-truth building attributes.
- EnergyBench (IISc Bangalore / IBM Research, HuggingFace) — multi-task energy benchmark.
- Beckel et al. (2014), *Energy* — building attribute inference from smart meter data.

### Assumption and rationale representation (for G6)

- Kunz & Rittel — Issue-Based Information System (IBIS).
- QOC (Question–Option–Criteria); PHI; DRL (Decision Representation Language).
- DRed — IBIS derivative deployed in aerospace practice.
- W3C PROV-O — provenance ontology.
- Sufficiency scenario literature on incompatible indicators and under-reported parameterisations.

---
[← Previous: Project Notes](appendix-c-buildfm-bs2027.html) · [Back to Home](index.html)
