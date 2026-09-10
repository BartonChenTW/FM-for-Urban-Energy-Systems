# Foundation Models for Urban Energy Systems

*Working notes — landscape review, roadmap, paper structure, and a proposed representation*

---

## Table of contents

1. [The foundation model landscape today](#1-the-foundation-model-landscape-today)
2. [What actually defines a foundation model](#2-what-actually-defines-a-foundation-model)
3. [Which urban energy sub-fields fit the FM pattern](#3-which-urban-energy-sub-fields-fit-the-fm-pattern)
4. [Candidate sub-fields for a new FM](#4-candidate-sub-fields-for-a-new-fm)
5. [Roadmap for a multi-carrier energy hub FM](#5-roadmap-for-a-multi-carrier-energy-hub-fm)
6. [Module and task decomposition](#6-module-and-task-decomposition)
7. [Concept paper structure](#7-concept-paper-structure)
8. [The representation problem](#8-the-representation-problem)
9. [A concrete proposed representation](#9-a-concrete-proposed-representation)
10. [Open risks and unresolved questions](#10-open-risks-and-unresolved-questions)

---

## 1. The foundation model landscape today

### 1.1 By domain

| Domain | Representative models | What they learn |
|---|---|---|
| Language | GPT-5-class, Gemini, Claude, Llama | Sequences of text tokens |
| Vision | ViT, SAM/SAM2, DINO | Sequences of image patches |
| Multimodal | Unified generation-and-understanding models | Cross-modal alignment across text, image, audio |
| Weather / climate | GraphCast, FengWu, Aurora | Physical fields on a spatiotemporal grid |
| Geospatial / remote sensing | Prithvi, ScaleMAE, Granite-GFM | Satellite pixels and patches over space and time |
| Time series | TimesFM, Chronos, Moirai, TTM, Toto, TimeGPT | Numeric sequences |
| Graph-structured systems | Emerging graph FMs, GridFM-v0 | Node/edge-structured data |
| Robotics / embodied | Vision-language-action models | Vision, language, touch, force, proprioception |

Granite-GFM is built on the Prithvi-SWIN-L Earth observation foundation model and uses a Swin Transformer backbone to estimate land surface temperature at 30 m resolution and hourly frequency for arbitrary cities.

### 1.2 Directions the field is moving

- **Time series has matured and converged on decoder-only architectures.** By 2026 the major families — Google TimesFM 2.5, Amazon Chronos-2, Salesforce Moirai 2.0, Datadog Toto 2.0, IBM Granite, Nixtla TimeGPT-2, NVIDIA NV-Tesseract — have all been refreshed. The practical question has shifted from "how do I train a model" to "which pretrained model do I select."
- **Scaling laws now hold for time series.** Toto 2.0 is the first time-series model where classic scaling behaviour (more data and parameters → predictably better performance) has been demonstrated. This matters because scaling laws are what justified the FM bet in language in the first place.
- **Multimodality is becoming the default**, not a special case. Cross-attending heterogeneous inputs is now standard design.
- **Physics-informed / hybrid FMs** are emerging wherever domain equations are known. GridFM-v0's masked-reconstruction-plus-power-flow-loss is the archetype in power systems.
- **Efficiency is a parallel axis to scale.** IBM's TTM family runs at 1–5 M parameters and is CPU-capable — the opposite bet from billion-parameter LLMs.
- **Synthetic and simulation-grounded pretraining** is rising wherever real annotated data is scarce or privacy-constrained. This is the logic behind CESAR-P and gridfm-datakit.
- **Graph FMs are a genuinely new frontier**, less mature than sequence FMs. GridFM-v0 sits at this edge.

---

## 2. What actually defines a foundation model

1. **Broad, diverse pretraining data** — ideally unlabelled or weakly labelled, collected at scale.
2. **Self-supervised pretraining objective** — the model predicts something withheld from its own input (masked token/patch reconstruction, next-value prediction) rather than requiring hand-labelled targets.
3. **A general-purpose architecture**, usually transformer-based, or graph-transformer for networked data.
4. **Task-agnostic representations** that transfer to many downstream tasks via lightweight fine-tuning or zero/few-shot inference.
5. **Three-phase lifecycle**: pretrain → fine-tune → cheap inference. The economic argument is that one expensive pretraining run is amortised across many applications.
6. **Emergent capabilities at scale** — behaviours not explicitly trained for, appearing as data and parameters grow.

**The unifying requirement:** there must be a *basic element* — a token, patch, or node — that is atomic, ubiquitous across the domain, and shareable across many downstream tasks. Text has the subword token. Vision has the patch. Time series has the value-at-timestep. Power systems have the bus.

---

## 3. Which urban energy sub-fields fit the FM pattern

| Sub-field | Basic element | Self-supervision task | Public pretraining data | Maturity |
|---|---|---|---|---|
| **Load / smart-meter FM** | Windowed patch of a meter time series | Masked / next-value reconstruction | EnergyBench, BuildingsBench, NEST | Mature — EnergyFM, Energy-TTM, Energy-TSPulse already exist |
| **Grid FM** (GridFM-v0) | A bus carrying (p, q, v, δ) as a graph node; lines and transformers as edges | Masked node-feature reconstruction + AC power-flow physics loss | PGLIB-OPF, IEEE cases, gridfm-datakit | Emerging but active |
| **UBEM / CESAR-P-style FM** | A building (envelope, geometry, HVAC, occupancy) paired with its simulated load | Conditional generation, attribute-to-profile mapping | Privately generable only | Not a found-data FM — simulator-grounded generative model |
| **Urban microclimate / geospatial-energy FM** | Satellite pixel/patch over space-time | Masked spatiotemporal reconstruction | HLS, Sentinel-2, ERA5 | Emerging, adjacent, not yet fused with load or grid data |
| **District multi-energy hub** | Not yet defined | Not yet defined | Essentially none public | Immature |

**Assessment.** Load FM and grid FM cleanly qualify: each has a natural atomic element, a natural masking-based pretext task, and either real or physically-simulated broad data. UBEM qualifies in spirit but is data-generation-bottlenecked rather than found-data-abundant. The multi-carrier hub layer currently has no clean basic element — which is itself the central finding of these notes.

---

## 4. Candidate sub-fields for a new FM

**Already committed and well-justified**

- **Metadata-conditioned load FM** — cross-attending meter time series with building-register attributes and household survey covariates. Mature tooling (Energy-TTM / TSPulse as baselines), EnergyBench as anchor dataset, CESAR-P paired labels as differentiator.

**Novel intersections, in rough order of tractability**

1. **Grid-load bridge FM** — cross-attend load-FM embeddings (demand side) with GridFM's graph representation (topology and physics side). Building and aggregate loads are literally the boundary condition GridFM's OPF solves against. Risk: coupling two different basic elements (a time-series patch and a graph node) is an open architectural question.
2. **Simulation-grounded UBEM FM** — formalise CESAR-P's building→load pairs as a deliberate pretraining corpus for a conditional generative FM, rather than treating CESAR-P output only as fine-tuning or evaluation data.
3. **Weather / microclimate-conditioned building energy FM** — fuse a geospatial FM with load or UBEM data, since urban heat islands drive peak cooling load and grid stress simultaneously. No existing paired dataset at FM scale; you would build the corpus, not just the model.
4. **Multi-carrier energy hub FM** — not yet FM-ready in the strict sense. No established basic element, no public data, and discrete decision structure resists replacement by a learned representation. Longer-horizon research question, and the subject of the rest of these notes.

---

## 5. Roadmap for a multi-carrier energy hub FM

### Phase 0 (Year 0–1) — Representation and the data engine

The MATPOWER moment for multi-carrier systems, which does not currently exist. Two deliverables:

- **A schema.** ESDL and CIM exist but neither is ML-ready.
- **A `hubfm-datakit` analogue** that generates scenarios at scale. Perturbation axes: demand profiles, technology portfolios, sizings, tariffs, carbon prices, weather years, network topology. CESAR-P is the demand-side generator.
- **A canonical benchmark set** — the hub equivalent of PGLIB-OPF. Owning that benchmark is worth as much as owning the model.

### Phase 1 (Year 1–3) — Simulation surrogate, deliberately not optimisation

Pretrain the masking task suite on simulated operation. Critically, train on **rule-based and perturbed-optimal dispatch**, not only cost-optimal dispatch. Cost-optimal dispatch is degenerate: many solutions achieve the same objective, so imitating a solver teaches an arbitrary tiebreak that will not generalise. Perturbing away from optimality gives a smooth, learnable manifold.

### Phase 2 (Year 2–4) — Multimodal conditioning

Fuse demand, weather, technology, and market encoders. Zero-shot transfer to unseen hub topologies becomes the headline metric, mirroring how GridFM-graphkit evaluates on unseen grids. This is where the load FM stops being a separate project and becomes a component.

### Phase 3 (Year 3–6) — Amortised optimisation

Not replacing the MILP. Predicting warm starts, likely-active binaries, and reduced candidate technology sets, then handing them to the solver. The metric is **solve-time reduction at a guaranteed optimality gap**, which is defensible to a power systems audience in a way that "our surrogate says 4 % cheaper" never will be, and which structurally avoids design search adversarially exploiting surrogate error.

### Phase 4 (Year 4–7) — The things MILP cannot do

Thousands of stochastic scenarios, reliability criteria, uncertainty quantification, robust design under climate and price uncertainty. Also policy-lever parameterisation: search over subsidy levels, carbon prices, and retrofit rates rather than over nodal capacities, because the lever space is low-dimensional and the capacity space is not.

### Phase 5 (Year 6–10) — Multi-scale coupling

Hub FM ↔ GridFM. Hub aggregate demand is the grid's boundary condition; grid constraints and nodal prices are the hub's boundary condition. Today these are solved in separate tools with hand-passed interfaces. A shared representation is the genuinely novel scientific claim.

---

## 6. Module and task decomposition

Do not build one model. Build an encoder stack, a pretraining task suite, and a downstream benchmark — so the programme is evaluable at each stage rather than a ten-year leap of faith.

### Encoders

| Module | Input | Status |
|---|---|---|
| Demand encoder | Building and district load profiles | EnergyFM / Energy-TTM plugs in directly |
| Weather and climate encoder | Irradiance, temperature, climate years | Adapt a geospatial FM |
| Technology encoder | Device class and parameters | Needs building — a device vocabulary |
| Topology encoder | The bipartite hub graph | Heterogeneous graph transformer, GridFM-adjacent |
| Market and policy encoder | Tariffs, carbon price, regulatory constraints | Needs building |

### Pretraining tasks (self-supervised, no solver labels)

- **P1 — Masked carrier-flow reconstruction.** The direct GridFM analogue and workhorse objective.
- **P2 — Masked device-attribute inference.** Hide a converter's capacity or efficiency, infer from observed flows.
- **P3 — Rollout / next-window prediction.** Trains inter-temporal structure.
- **P4 — Masked topology completion.** Which device connects these two carrier-buses.

### Downstream tasks (the benchmark suite)

| Task | Output | Why well-posed |
|---|---|---|
| D1 Operation emulation | Dispatch trajectory given fixed design | Deterministic under a fixed rule |
| D2 Feasibility classification | Can this design serve this demand | Binary, cheap to label |
| D3 Cost / emissions regression | Objective value from design + boundary conditions | Unique even when the argmin is not |
| D4 Active-set / binary prediction | Which technologies install, which constraints bind | Feeds warm-starting |
| D5 Flexibility envelope | Aggregate hub flexibility for grid services | The natural GridFM handshake |
| D6 Retrofit / anomaly | Diagnosis on operating hubs | Where NEST and real Empa districts validate |

**D3 is well-posed even where "predict the optimal design" is not.** This is the core reason for the phase sequencing above.

---

## 7. Concept paper structure

### 7.1 The positioning problem

The Joule GridFM perspective (Hamann, Gjorgiev, Brunschwiler et al., 2024) already argues: energy transition creates a computational gap → FMs have properties that close gaps → roadmap for GridFM-v0 → downstream uses → call to action. Reviewers in this community have read it. A paper that is "the same argument for urban energy systems" reads as derivative regardless of how new the sentences are.

**Recommended central claim:**

> The obstacle to a foundation model for urban energy systems is not compute, data volume, or architecture. It is that the domain has no tokenization. This paper proposes one, and shows what becomes possible once it exists.

The GridFM paper structurally could not make this claim, because power systems already had MATPOWER and the bus abstraction. The claim is genuinely unsolved and positions the work as complementary rather than an echo.

### 7.2 Section skeleton

| Section | Length | Function |
|---|---|---|
| Title + Summary | ~150 w | Name the model class and commit to it |
| Context & Scale | ~200 w | Editor-facing: why this matters beyond specialists |
| 1. Introduction | 1–1.5 pp | Thesis, contributions, roadmap of the paper |
| 2. The urban energy system and its computational limits | 2–3 pp | The gap, framed by *what questions cannot be asked today* |
| 3. Why FMs, and why not | 2–3 pp | Honest capability assessment including failure modes |
| 4. **The representation problem** | 3–4 pp | Core contribution |
| 5. Pretraining tasks and module decomposition | 2–3 pp | The self-supervision suite |
| 6. Downstream tasks and a benchmark proposal | 2 pp | What the model is evaluated on |
| 7. Roadmap | 2–3 pp | Phased, with kill criteria |
| 8. Coupling to adjacent FMs | 1–2 pp | GridFM handshake, load FMs, geospatial FMs |
| 9. Barriers | 1.5 pp | Data, privacy, trust, validation, misuse |
| 10. Call to action | 0.5 pp | Concrete asks, not vague enthusiasm |

Total 20–30 pages, typical for this genre.

### 7.3 Notes on the load-bearing sections

**Section 2 — frame the gap as unanswerable questions, not slowness.** "MILP is slow" invites "buy a better solver." Instead: design a district under 500 climate-and-price scenarios; evaluate reliability criteria at city scale; co-optimise a hundred hubs against a distribution grid; explore policy-lever space rather than capacity space. Each is a question, not a speedup, and each maps to a roadmap phase.

**Section 3 — put limitations in the middle, not the end.** Say plainly that FMs cannot replace the optimisation problem: objective degeneracy, dual variables needed for regulation, inter-temporal coupling, and discrete decisions all remain. Then argue FMs can *amortise* the solve and *enable* uncertainty and reliability work. A concept paper that admits its boundaries is read as serious.

**Section 4 — this is the paper.** Most space, best figure. Bipartite structure, typed multi-port devices, carrier-quality dimension, hierarchical temporal tokenization, physics-loss inventory, and an explicit worked example.

**Section 6 — propose the benchmark and name it.** Communities coalesce around benchmarks more reliably than around models (PGLIB-OPF, EnergyBench). It also gives other groups something to do that is not competing with you.

**Section 7 — include failure criteria.** State that if Phase 1 surrogates do not beat a tuned reduced-order model on held-out topologies by year two, the premise is wrong. Almost no concept paper does this; it costs nothing and buys credibility.

### 7.4 Figures

Budget five or six — in this genre figures carry more argumentative weight than text.

1. The computational gap: questions against tractable scale
2. The representation: a district as bipartite graph, annotated with token feature vectors
3. Carrier quality levels and permitted conversions
4. Pretraining task suite, masking illustrated on the graph
5. Roadmap phases with deliverables and go/no-go gates
6. FM ecosystem: hub FM relative to GridFM, load FMs, geospatial FMs

### 7.5 Practical notes

- **Venue.** Joule Perspective is the obvious target given precedent, but it is the same venue as the paper being differentiated from. Applied Energy, Advances in Applied Energy, or Nature Energy Perspective are alternatives. A preprint early is worth more than perfect placement — concept papers work by being cited into existence.
- **Coalition.** The GridFM paper carries roughly forty authors across IBM, ETH, Argonne, NREL, Hydro-Québec, and INESC TEC. That author list *is* part of the argument. Decide early whether this is an Empa position paper or a coalition paper; the second is slower and much stronger.
- **Sequencing.** The commonest failure of concept papers is being all promise. Even a small empirical result — a hub tokenization pretrained on a few thousand synthetic scenarios with a zero-shot transfer number — turns a manifesto into a manifesto with evidence.

---

## 8. The representation problem

### 8.1 A representation is four decisions, not one

The atomic unit; the structure relating units; discrete versus continuous; and which invariances are baked in.

| Family | Atomic unit | Structure | Discrete/continuous | Invariance |
|---|---|---|---|---|
| LLM | Subword token | 1D sequence position | Discrete, ~50–200 k vocab | None; order is meaning |
| ViT / SAM | 16×16 patch, linearly projected | 2D grid position | Continuous | Weak translation |
| TimesFM / PatchTST / TTM | Patch of N consecutive values, instance-normalised | 1D position | Continuous | Scale, via normalisation |
| Chronos | A quantized value bin | 1D sequence | Discrete codebook | Scale |
| GraphCast / Aurora | Grid cell, all variables at all pressure levels | Icosahedral multi-mesh | Continuous | Spherical geometry |
| Prithvi / geospatial | Spatiotemporal multispectral patch | (x, y, t) | Continuous | Translation |
| Protein / molecular | Atom or residue | Graph adjacency + 3D coords | Discrete types, continuous coords | SE(3) equivariance, permutation |
| GridFM-v0 | A bus carrying (p, q, v, δ) | Graph; lines and transformers as edges | Continuous | Permutation over buses |

**The two poles.** Chronos discretises time series into bins and treats forecasting as a sequence-to-sequence language task, inheriting the entire T5 stack and producing probabilistic output through Monte Carlo sampling over the vocabulary — maximum machinery reuse, zero physics. GridFM does the opposite: continuous node features plus a physics term enforcing AC power balance, so the model does not have to rediscover Kirchhoff — maximum structure, no reuse of language machinery.

### 8.2 The causal chain: representation → data → capability

**(a) It defines what counts as one sample, which can change effective dataset size by three orders of magnitude.**
EnergyBench's ~78 k buildings: as building-days, ~28 M samples; as building-years, 78 k; as district-years, perhaps 200. Identical underlying data, entirely different regime — the first supports pretraining, the third supports fine-tuning at best. For hubs the escape is to make the *device* or *carrier-bus* the token and the district merely the graph they sit in, so one district-year contributes thousands of tokens rather than one sample. This decision alone determines whether the corpus is viable.

**(b) It determines whether a self-supervised task exists at all.**
Masking works only when the masked part is predictable from the remainder but not trivially so. Too coarse and there is nothing to hide; too fine and the task collapses into interpolation and the model learns smoothing rather than physics. GridFM sits in the sweet spot because masking a bus's (p, q, v, δ) is genuinely equivalent to solving power flow at that node. **The test for hubs: is masking one carrier-bus's flows equivalent to solving something?**

**(c) It determines what transfers zero-shot.**
You can only generalise along axes the representation makes structural rather than parametric. GridFM transfers to unseen topologies because topology lives in the graph, not the weights. For transfer across hub configurations, device *class* must be an embedding shared across hubs, and hub identity must not appear in the parameters.

**(d) It sets a hard ceiling on context, and this is where hubs break.**
Attention is quadratic; patching exists to buy context length. TimesFM 1.0 handled up to 512 time points, 2.0 up to 2048, and 2.5 reaches 16 k context at around 200 M parameters; Moirai handles up to 5000 steps. One year of hourly data is 8760 steps. For seasonal thermal storage this is fatal, not inconvenient: the charge decision in June is only justified by the discharge in January, and any representation that chops the year into independent windows destroys the coupling that makes multi-carrier hubs interesting.

**(e) It determines what physics can go in the loss.**
The loss can only reference quantities the token exposes. If carrier quality is not a token dimension, you cannot write a constraint forbidding free upgrading of 35 °C heat to 80 °C, and the model will violate thermodynamics wherever data is sparse.

**(f) It silently deletes information you may need later.**
Instance normalisation gives time-series FMs their scale invariance and cross-domain transfer, but discards absolute magnitude. A normalised load embedding cannot tell you whether a transformer is overloaded, because "how many kW" was normalised away. If load-FM embeddings are ever handed to a grid FM as boundary conditions, magnitude must be carried separately. This is a representation-level bug that no amount of fine-tuning fixes.

### 8.3 The five decisions the paper must make explicit

1. **Sample granularity** — device-week, hub-day, or hub-year. Determines corpus viability.
2. **Carrier quality encoding** — continuous temperature, discrete quality levels, or exergy factor. Continuous is physically honest but makes the permitted-conversion constraint harder to express; discrete is cleaner but arbitrary at boundaries.
3. **Temporal hierarchy** — how hourly, daily, and seasonal scales nest given the context ceiling.
4. **Device vocabulary** — a fixed technology-class set makes installation a clean classification problem but generalises badly to technologies invented after training; a continuous parameter space generalises but invites interpolation to physically nonexistent devices. Probably: fixed class embedding plus continuous parameter conditioning within class.
5. **Heterogeneity** — the biggest unproven bet. Nearly every successful FM uses a single token type; this needs at least two plus multiple edge types, putting it in heterogeneous graph transformer territory where the machinery is far less battle-tested.

### 8.4 Why this makes a good paper rather than a good appendix

Language, vision, and weather all had their representations handed to them. Words existed before LLMs; pixels before ViT; the sphere's geometry before GraphCast; MATPOWER and the bus abstraction decades before GridFM. Urban multi-carrier energy systems have no such inheritance, and every existing formalism — the energy hub coupling matrix, ESDL, CIM — was designed for solvers or interoperability rather than for learning. Arguing that **the tokenization is the bottleneck, and that it is a research problem rather than an engineering detail**, is a claim that is both true and unclaimed.

---

## 9. A concrete proposed representation

**In one line:** a heterogeneous bipartite graph of carrier-bus tokens and device tokens, with carrier quality as an explicit ordered dimension, over a three-level temporal hierarchy with a storage carry channel.

### 9.1 Why bipartite rather than conversion-on-edges

An edge has exactly two endpoints, so a CHP (gas in → electricity *and* heat out) or a heat pump (electricity + ambient source → heat) cannot be one edge. Making devices first-class nodes with typed ports to multiple carrier-buses handles multi-input/multi-output cleanly and gives a place to attach technology embeddings — which is what lets the model generalise to a hub containing a device configuration never seen during pretraining.

### 9.2 What makes this different from GridFM, not a relabelling

1. **Carrier quality is not fungible.** Heat at 80 °C and heat at 35 °C are different commodities with an ordering between them. Electricity has no analogue. The physics loss must forbid free upgrading, and the quality ordering can be encoded structurally as a directed edge.
2. **The token must carry a time window, not a snapshot.** GridFM-v0 is snapshot-based — one solved power flow per sample. Hubs are inherently inter-temporal because of storage, and seasonal storage means the year cannot be chopped into independent windows.

### 9.3 Token schema

```
CARRIER-BUS TOKEN
  static:
    carrier_class      embedding [elec, heat, cold, gas, H2, biomass, ambient]
    quality            normalized scalar (K for thermal, kV for elec, bar for gas)
    exergy_factor      derived scalar, gives the model conversion limits for free
    position           (x, y) or relative encoding
    is_boundary        bool
  per temporal patch:
    net_injection      normalized profile + log-magnitude scalar (two channels)
    shadow_price       from solver duals
    unserved           slack

DEVICE TOKEN
  static:
    tech_class         embedding from a closed vocabulary
    rated_capacity     per port
    eta_params         nominal efficiency + part-load coefficients
                       + temperature sensitivity (COP curve)
    ramp / min_up / min_down / min_part_load
    capex, opex, lifetime, embodied_emissions
    age, controllability
    state_active       bool — true for storage
  per temporal patch:
    port_throughput    per port
    part_load_fraction
    on_off
    availability
    state_of_charge    active only if state_active

EDGE TYPES
  device_port     device <-> carrier-bus, typed by role (in/out) and carrier
  transport       carrier-bus <-> carrier-bus, same carrier
                  (length, capacity, loss coeff, thermal time constant)
  quality_order   carrier-bus -> carrier-bus, same site, directed downward only
```

**Two choices worth defending explicitly:**

- **Storage is a device subtype, not a fourth node type.** Keeps the vocabulary at two, and `state_active` tells the attention mechanism which nodes need cross-day routing.
- **Two-channel normalisation** — normalised profile plus explicit log-magnitude. This is the direct fix for §8.2(f). Carry both from the start; magnitude cannot be recovered later by fine-tuning.

### 9.4 Worked example — a 50-building district

**Carrier-buses**

| ID | Carrier | Quality | Role |
|---|---|---|---|
| B1 | Electricity | 0.4 kV | Internal LV |
| B2 | Electricity | MV | Grid connection / import |
| B3 | Heat | 75 °C | DH supply |
| B4 | Heat | 45 °C | DH return / LT loop |
| B5 | Gas | — | Import |
| B6 | Ambient | ~12 °C | Ground source |

**Devices**

| ID | Technology | Ports |
|---|---|---|
| D1 | CHP | B5 in → B1, B3 out |
| D2 | Heat pump | B1, B6 in → B4 out |
| D3 | Boiler | B5 in → B3 out |
| D4 | PV | exogenous irradiance → B1 out |
| D5 | Battery | B1 ↔ B1, state |
| D6 | Hot water tank | B3 ↔ B3, state |
| D7 | Borehole seasonal storage | B4 ↔ B6, state, large time constant |
| D8 | Transformer | B2 ↔ B1 |

**Quality edges:** B3 → B4 permitted (downgrade via load and mixing); B4 → B3 forbidden without a device. This one-way relation has no analogue in GridFM and is the clearest illustration of why multi-carrier systems need a different token.

### 9.5 Temporal hierarchy

| Level | Unit | Attention pattern | Carries |
|---|---|---|---|
| L0 | 24 hourly values, one token per node per day | Full attention across the graph within a day | Diurnal dispatch, conversion physics |
| L1 | Day tokens | Strided / sparse across days, **storage nodes only** | Weekly and seasonal charge cycles |
| L2 | One annual token | Global | Seasonal SoC, annual energy and emissions budget |

**The numbers work.** A 50-building district with ~30 carrier-buses and ~40 devices is 70 node tokens. Per year that is 365 × 70 ≈ 25,000 tokens — within reach given TimesFM 2.5 already runs 16 k context at 200 M parameters, and cross-day attention only needs to be dense for the handful of storage nodes. The flat alternative is 8760 × 70 ≈ 613,000 tokens, which is not tractable.

### 9.6 Masking tasks mapped onto the tokens

| Task | What is masked | What it teaches |
|---|---|---|
| M1 | Carrier-bus injections for a day | Balance-solving — the power-flow analogue |
| M2 | Device throughput | Dispatch behaviour |
| M3 | Device static attributes (capacity, η) | Attribute inference |
| M4 | A device-port edge | Which technology plausibly connects these carriers |
| M5 | Future window | Rollout |
| M6 | **Mid-year storage SoC trajectory** | Seasonal reasoning — the distinctive one, and the first to fail if the hierarchy is wrong |

### 9.7 Physics loss, attached to tokens

- Per-carrier nodal balance at every bus and patch
- Conversion relations, `out = η(part-load, boundary conditions) × in`, with temperature-dependent COP
- Storage continuity with self-discharge and cyclic / seasonal boundary conditions
- Capacity, ramp, and minimum-uptime bounds
- Transport losses including thermal time delay
- **No-upgrade penalty** on any flow violating the quality ordering
- Emissions and primary-energy accounting

Every term references a quantity the token actually exposes — the test a representation has to pass.

### 9.8 Invariances

- Permutation over nodes (from the graph structure)
- Scale (from two-channel normalisation)
- Carrier-quality ordering (structural, via directed downgrade edges)
- **Not** time-shift — diurnal and seasonal phase matter, so absolute time-of-day and day-of-year must be encoded

### 9.9 Minimum viable v0

Ship this first, prove the premise, then add:

- Single site, no spatial network (drop transport edges)
- Three carriers, two heat quality levels
- No seasonal storage, no L1/L2 hierarchy — day-level tokens only
- M1 and M2 only
- Fixed device vocabulary of ~8 classes

If that does not beat a tuned reduced-order model on held-out device configurations, the representation is wrong — learned in months rather than years.

---

## 10. Open risks and unresolved questions

### 10.1 Five risks most likely to kill the programme

1. **Label degeneracy.** Cost-optimal dispatch has many equally-optimal solutions. Mitigation: predict objective values, active sets, and distributions rather than argmins.
2. **Discrete decisions do not interpolate.** Mitigation: treat installation as classification over a fixed technology vocabulary, not regression on a capacity vector.
3. **Seasonal coupling breaks windowing.** Requires the hierarchical tokenization; this is an open architectural problem, not a solved one.
4. **No real data, ever.** Multi-carrier district data is scarcer than grid data and more privacy-encumbered. Synthetic-first is the only path, so validation on NEST and real Empa districts is the credibility anchor for the whole programme.
5. **You may be building a very expensive interpolator.** If Phase 1 surrogates do not beat a well-tuned reduced-order model on held-out topologies, the FM premise fails. Build that kill criterion into Phase 1 explicitly.

### 10.2 Three genuinely unsettled design questions

- **Shadow prices as features.** Including solver duals gives rich supervision for free and they are what regulators actually need, but they may encode solver artifacts and degeneracy tiebreaks rather than physics. Recommendation: include as an auxiliary prediction head rather than an input feature, so they can be ablated.
- **Heterogeneous graph transformers are the weak link.** Almost every successful FM uses one token type. This design needs two plus three edge types. This machinery is far less battle-tested than sequence transformers, and is the assumption most likely to cost a year.
- **Quality discretisation is arbitrary at the boundaries.** Is 60 °C its own level or does it round to 75? Continuous temperature is physically honest but makes the ordering constraint harder to express as a differentiable penalty. Current lean: discrete levels with continuous temperature as an auxiliary feature — but not settled.

---

## Appendix — key resources referenced

**Models and checkpoints**
EnergyFM (Energy-TTM, Energy-TSPulse) · GridFM-v0 · Chronos · Toto 2.0 · TimesFM 2.5 · Moirai 2.0 · IBM Granite TTM · Prithvi / Granite-GFM · GraphCast, Aurora

**Datasets**
EnergyBench (HuggingFace, ~166 GB, 78 k+ real buildings plus synthetic tiers, CC-BY-SA-4.0) · CESAR-P (Empa internal) · NEST dataset (Empa) · BuildingsBench (NREL) · PGLIB-OPF · IEEE test cases

**Tools**
PyPSA · MATPOWER · EnergyPlus · ehubX / MANGO · gridfm-datakit · ESDL, CIM (schemas)

**Key papers**
Hamann, Gjorgiev, Brunschwiler et al., "Foundation models for the electric power grid," *Joule* 8, Dec 2024 · PowerGraph benchmark (NeurIPS 2024 Datasets & Benchmarks) · gridfm-datakit v1 · Geidl & Andersson, energy hub formalism

---

*Notes compiled from a working conversation. Nothing here is peer-reviewed; the numbered risks and unresolved questions are the parts most likely to change.*
