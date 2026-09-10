# References

*Compiled to accompany "Foundation Models for Urban Energy Systems: working notes" ([FM_for_UES.md](FM_for_UES.md)). Organised by research category rather than publication type, so a reader tracking progress in this field can scan by topic. Each entry is collapsed to year / title / first author for quick scanning — click to expand for the full breakdown and abstract.*

**How to read this file:** click any entry to expand it. Entries missing an abstract, institution, or key-method note are marked `[to confirm]` — see [inbox.md](inbox.md) if you want to help fill these in; drop a link or note there and it gets triaged in.

---

## Table of contents

1. [Grid & power system foundation models](#1-grid--power-system-foundation-models)
2. [Time series foundation models (general-purpose)](#2-time-series-foundation-models-general-purpose)
3. [Geospatial & weather foundation models](#3-geospatial--weather-foundation-models)
4. [Building & energy load: models, datasets, benchmarks](#4-building--energy-load-models-datasets-benchmarks)
5. [Multi-carrier energy hub formalism (pre-FM foundations)](#5-multi-carrier-energy-hub-formalism-pre-fm-foundations)
6. [Power & building system simulation tools (classical, non-AI)](#6-power--building-system-simulation-tools-classical-non-ai)
7. [Schemas & standards](#7-schemas--standards)
8. [Project resources & personal communication](#8-project-resources--personal-communication)
9. [Notes on using this list in a manuscript](#9-notes-on-using-this-list-in-a-manuscript)

---

## 1. Grid & power system foundation models

*The most directly analogous prior art for a UES foundation model — this is the field FM_for_UES.md positions itself against/alongside (see §7.1).*

<details>
<summary><strong>2024 — Foundation models for the electric power grid</strong> (Hamann et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Hamann, H. F.; Gjorgiev, B.; Brunschwiler, T. *(~30 further co-authors across a multi-institution consortium)* |
| **Institution (top 2)** | IBM Research; ETH Zurich (Reliability and Risk Engineering Laboratory) — consortium also includes Argonne, NREL, Hydro-Québec, INESC TEC [to confirm full affiliation-by-author breakdown] |
| **Venue** | *Joule*, 8(12), 3245–3258 |
| **Type** | Journal article (Perspective) |
| **Key AI method** | Position/roadmap paper proposing GridFM-v0: masked node-feature reconstruction pretraining plus an AC power-flow physics loss, on a graph where buses are nodes |
| **Link(s)** | https://doi.org/10.1016/j.joule.2024.11.002 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2024 — PowerGraph: A power grid benchmark dataset for graph neural networks</strong> (Varbella et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Varbella, A.; Amara, K.; Gjorgiev, B. |
| **Institution (top 2)** | ETH Zurich [to confirm second affiliation] |
| **Venue** | NeurIPS 2024, Datasets and Benchmarks Track |
| **Type** | Dataset / benchmark paper |
| **Key AI method** | GNN benchmark for power-grid classification/cascading-failure tasks |
| **Link(s)** | Dataset: https://doi.org/10.6084/m9.figshare.22820534 (CC BY 4.0) · Code: https://github.com/PowerGraph-Datasets |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2025 — gridfm-datakit-v1: A Python library for scalable and realistic power flow and OPF data generation</strong> (Puech et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Puech, A.; Mazzonelli, M.; Cintas, C. *(+ Govindasamy, Mngomezulu, Weiss, Baù, Varbella, Miralles, Kim, Xie, Hamann, Vos, Brunschwiler)* |
| **Institution (top 2)** | IBM Research [to confirm second affiliation] |
| **Venue** | arXiv preprint |
| **Type** | Software paper / preprint |
| **Key AI method** | N/A — data-generation library (power flow / OPF scenario synthesis) supporting FM pretraining; not itself a model |
| **Link(s)** | https://arxiv.org/abs/2512.14658 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>— — GridFM (project website)</strong> (IBM Research, ETH Zurich, Argonne, and collaborators)</summary>

| | |
|---|---|
| **Authors (top 3)** | Consortium — see Hamann et al. 2024 above |
| **Institution (top 2)** | IBM Research; ETH Zurich |
| **Venue** | Project website (not a citable publication) |
| **Type** | Project resource |
| **Key AI method** | Same as GridFM-v0 above — tracked separately here as an evolving project reference distinct from the fixed Joule paper |
| **Link(s)** | [internal project file `GridFM_website`; no stable public URL recorded — to confirm] |

**Abstract:** N/A (project website, not a paper)

</details>

---

## 2. Time series foundation models (general-purpose)

*Cross-domain sequence FMs, mostly directly reusable as a load/demand encoder — see §4 and the encoder table in §6 of FM_for_UES.md.*

<details>
<summary><strong>2024 — A decoder-only foundation model for time-series forecasting [TimesFM]</strong> (Das et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Das, A.; Kong, W.; Sen, R. *(+ Zhou, Y.)* |
| **Institution (top 2)** | Google Research |
| **Venue** | ICML 2024, PMLR 235, 10148–10167 |
| **Type** | Conference paper |
| **Key AI method** | Decoder-only transformer, patch-based tokenization, pretrained on a large cross-domain time-series corpus |
| **Link(s)** | https://proceedings.mlr.press/v235/das24c.html · preprint: https://arxiv.org/abs/2310.10688 · code: https://github.com/google-research/timesfm |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2024 — Chronos: Learning the language of time series</strong> (Ansari et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Ansari, A. F.; Stella, L.; Turkmen, C. *(+ Zhang, Mercado, Shen, Shchur, Rangapuram, Pineda Arango, Kapoor, Zschiegner, Maddix, Mahoney, Torkkola, Wilson, Bohlke-Schneider, Wang)* |
| **Institution (top 2)** | Amazon Science (AWS AI Labs) |
| **Venue** | *Transactions on Machine Learning Research* |
| **Type** | Journal article |
| **Key AI method** | Time series discretized into a quantized-value vocabulary, trained as a sequence-to-sequence language model (T5 backbone); probabilistic forecasts via sampling |
| **Link(s)** | https://openreview.net/forum?id=gerNCVqqtR · preprint: https://arxiv.org/abs/2403.07815 · code: https://github.com/amazon-science/chronos-forecasting |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2024 — Unified training of universal time series forecasting transformers [Moirai]</strong> (Woo et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Woo, G.; Liu, C.; Kumar, A. *(+ Xiong, Savarese, Sahoo)* |
| **Institution (top 2)** | Salesforce AI Research |
| **Venue** | ICML 2024, PMLR 235, 53140–53164 |
| **Type** | Conference paper |
| **Key AI method** | Masked-encoder transformer, any-variate attention, multiple patch-size projection layers for heterogeneous frequencies |
| **Link(s)** | https://proceedings.mlr.press/v235/woo24a.html · preprint: https://arxiv.org/abs/2402.02592 · code: https://github.com/SalesforceAIResearch/uni2ts |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2024 — Tiny Time Mixers (TTMs): Fast pre-trained models for enhanced zero/few-shot forecasting</strong> (Ekambaram et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Ekambaram, V.; Jati, A.; Dayama, P. *(+ Mukherjee, Nguyen, Gifford, Reddy, Kalagnanam)* |
| **Institution (top 2)** | IBM Research |
| **Venue** | NeurIPS 2024 |
| **Type** | Conference paper |
| **Key AI method** | Lightweight MLP-Mixer architecture (non-transformer), 1–5M parameters, CPU-capable — efficiency-axis counterpoint to billion-parameter FMs |
| **Link(s)** | https://openreview.net/forum?id=3O5YCEWETq · preprint: https://arxiv.org/abs/2401.03955 · code: https://github.com/ibm-granite/granite-tsfm |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2025 (orig. 2024) — This time is different: An observability perspective on time series foundation models [Toto]</strong> (Cohen et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Cohen, B.; Khwaja, E.; Doubli, Y. *(+ Lemaachi, Lettieri, Masson, Miccinilli, Ramé, Ren, Rostamizadeh, Ogier du Terrail, Toon, Wang, Xie, Asker, Talwalkar, Abou-Amal)* |
| **Institution (top 2)** | Datadog |
| **Venue** | arXiv preprint (originally released as "Toto: Time series optimized transformer for observability," arXiv:2407.07874) |
| **Type** | Preprint |
| **Key AI method** | Decoder-only transformer with factorized 2D (time + variate) attention; first time-series FM to demonstrate classic scaling-law behaviour (more data/params → predictably better performance) |
| **Link(s)** | https://arxiv.org/abs/2505.14766 · code: https://github.com/DataDog/toto |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>— — Granite Time Series: TSPulse and FlowState</strong> (IBM Research)</summary>

| | |
|---|---|
| **Authors (top 3)** | Ekambaram, V.; Jati, A. *(+ team)* [to confirm full author list — product documentation, not a single dated paper] |
| **Institution (top 2)** | IBM Research |
| **Venue** | Product/model documentation (IBM Granite Time Series) |
| **Type** | Software / model documentation |
| **Key AI method** | Pretrained lightweight patch-based TS FMs — TSPulse (dual embedding) and FlowState (state-space) — distinct from the NeurIPS TTM paper above |
| **Link(s)** | https://www.ibm.com/granite/docs/models/time-series · https://huggingface.co/ibm-granite/granite-timeseries-ttm-r2 · code: https://github.com/ibm-granite/granite-tsfm |

**Abstract:** N/A (software documentation, not a paper)

</details>

<details>
<summary><strong>— — TimeGPT</strong> (Nixtla)</summary>

| | |
|---|---|
| **Authors (top 3)** | [to confirm] |
| **Institution (top 2)** | Nixtla |
| **Venue** | Product documentation (not peer-reviewed) |
| **Type** | Software / commercial product |
| **Key AI method** | Decoder-only transformer, API-served time-series FM |
| **Link(s)** | https://www.nixtla.io/docs/timegpt |

**Abstract:** N/A (product page, not a paper)

</details>

<details>
<summary><strong>2025 — Foundation Models for Clean Energy Forecasting: A Comprehensive Review</strong> (Ferdaus et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Ferdaus, M. M.; [to confirm additional authors] |
| **Institution (top 2)** | [to confirm] |
| **Venue** | *Renewable Energy* (Elsevier) |
| **Type** | Journal article (Review) |
| **Key AI method** | Comprehensive survey of foundation models for renewable energy forecasting (wind, solar); establishes taxonomy across model architecture, pre-training paradigm, adaptation strategy, and application domain; first systematic analysis of FMs in clean energy forecasting |
| **Link(s)** | https://www.sciencedirect.com/science/article/abs/pii/S1364032125011256 · https://arxiv.org/abs/2507.23147

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

---

## 3. Geospatial & weather foundation models

*Candidate weather/microclimate encoders — see candidate intersection #3 in §4 of FM_for_UES.md (urban heat islands driving peak cooling load).*

<details>
<summary><strong>2023 — Learning skillful medium-range global weather forecasting [GraphCast]</strong> (Lam et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Lam, R.; Sanchez-Gonzalez, A.; Willson, M. *(+ Wirnsberger, Fortunato, Pritzel, Ravuri, Ewalds, Alet, Eaton-Rosen, Hu, Merose, Hoyer, Holland, Vinyals, Stott, Mohamed, Battaglia)* |
| **Institution (top 2)** | Google DeepMind |
| **Venue** | *Science*, 382(6677), 1416–1421 |
| **Type** | Journal article |
| **Key AI method** | Graph neural network (encode-process-decode) operating on an icosahedral multi-mesh over the sphere |
| **Link(s)** | https://doi.org/10.1126/science.adi2336 · code: https://github.com/google-deepmind/graphcast |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2023 — Foundation models for generalist geospatial artificial intelligence [Prithvi]</strong> (Jakubik et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Jakubik, J.; Roy, S.; Phillips, C. E. *(+ ~20 further co-authors)* |
| **Institution (top 2)** | NASA; IBM Research |
| **Venue** | arXiv preprint |
| **Type** | Preprint |
| **Key AI method** | Vision Transformer masked autoencoder (MAE) over multispectral, multitemporal satellite patches |
| **Link(s)** | https://arxiv.org/abs/2310.18660 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2024 — Prithvi-EO-2.0: A versatile multi-temporal foundation model for Earth observation applications</strong> (Szwarcman et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Szwarcman, D.; Roy, S.; Fraccaro, P. *(+ Gíslason, Blumenstiel, Ganti, et al.)* |
| **Institution (top 2)** | IBM Research; NASA |
| **Venue** | arXiv preprint |
| **Type** | Preprint |
| **Key AI method** | Scaled-up multi-temporal ViT/MAE geospatial FM; underlies Granite-GFM (used for land surface temperature estimation, see FM_for_UES.md §1.1) |
| **Link(s)** | https://arxiv.org/abs/2412.02732 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

---

## 4. Building & energy load: models, datasets, benchmarks

*The most mature sub-field per §3/§4 of FM_for_UES.md — already has real pretraining data and working FMs.*

<details>
<summary><strong>2023 — BuildingsBench: A large-scale dataset of 900K buildings and benchmark for short-term load forecasting</strong> (Emami et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Emami, P.; Sahu, A.; Graf, P. |
| **Institution (top 2)** | NREL (National Renewable Energy Laboratory) |
| **Venue** | NeurIPS 2023, Datasets and Benchmarks Track |
| **Type** | Dataset / benchmark paper |
| **Key AI method** | Benchmark + baseline forecasting models (not itself an FM); dataset derived from NREL's End-Use Load Profiles (EULP) database |
| **Link(s)** | https://arxiv.org/abs/2307.00142 · code: https://github.com/NREL/BuildingsBench · data: https://data.openei.org/submissions/5859 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2026 — EnergyFM: Pretrained models for energy meter data analytics</strong> (Empa / IBM / IISc author team)</summary>

| | |
|---|---|
| **Authors (top 3)** | [to confirm — full author list not yet recorded] |
| **Institution (top 2)** | Empa; IBM Research (IISc Bangalore collaboration) |
| **Venue** | e-Energy '26 (17th ACM International Conference on Future and Sustainable Energy Systems) |
| **Type** | Conference paper |
| **Key AI method** | Pretrained FM for energy meter data (Energy-TTM / Energy-TSPulse), built on the IBM Granite TS family |
| **Link(s)** | https://doi.org/10.1145/3744255.3798119 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>— — EnergyBench</strong> (ai-iot / AI-IoT Lab, IISc Bangalore)</summary>

| | |
|---|---|
| **Authors (top 3)** | [to confirm] |
| **Institution (top 2)** | IISc Bangalore |
| **Venue** | Hugging Face dataset release (not a paper) |
| **Type** | Dataset |
| **Key AI method** | N/A — pretraining corpus: ~78,037 real buildings (2,916 commercial, 75,121 residential) plus synthetic tiers, 1.26 billion hourly electricity-consumption readings, CC-BY-SA-4.0 |
| **Link(s)** | https://huggingface.co/datasets/ai-iot/EnergyBench |

**Abstract:** N/A (dataset card, not a paper)

</details>

<details>
<summary><strong>— — NEST dataset</strong> (Empa, Urban Energy Systems Laboratory)</summary>

| | |
|---|---|
| **Authors (top 3)** | N/A (institutional dataset) |
| **Institution (top 2)** | Empa (Urban Energy Systems Laboratory) |
| **Venue** | Internal / partially public |
| **Type** | Dataset |
| **Key AI method** | N/A — real operating-building data from the NEST demonstrator (see §8 project resources) |
| **Link(s)** | see NEST facility entry, §8 |

**Abstract:** N/A (dataset, not a paper)

</details>

<details>
<summary><strong>— — CESAR-P-generated synthetic building corpus</strong> (Empa, Urban Energy Systems Laboratory)</summary>

| | |
|---|---|
| **Authors (top 3)** | N/A (internal dataset) |
| **Institution (top 2)** | Empa (Urban Energy Systems Laboratory) |
| **Venue** | Internal |
| **Type** | Dataset |
| **Key AI method** | N/A — building-attribute-to-load-profile pairs generated via the CESAR-P simulation pipeline (see §6); the paired-label differentiator noted for UBEM FM work in §4 of FM_for_UES.md |
| **Link(s)** | internal |

**Abstract:** N/A (internal dataset, not a paper)

</details>

---

## 5. Multi-carrier energy hub formalism (pre-FM foundations)

*The classical (non-learned) formalism a multi-carrier hub FM would need to either subsume or interoperate with — see §9.1 of FM_for_UES.md.*

<details>
<summary><strong>2007 — Optimal power flow of multiple energy carriers</strong> (Geidl & Andersson)</summary>

| | |
|---|---|
| **Authors (top 3)** | Geidl, M.; Andersson, G. |
| **Institution (top 2)** | ETH Zurich |
| **Venue** | *IEEE Transactions on Power Systems*, 22(1), 145–155 |
| **Type** | Journal article |
| **Key AI method** | N/A — classical energy hub formalism, not a learned model |
| **Link(s)** | https://doi.org/10.1109/TPWRS.2006.888988 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2007 — Energy hubs for the future</strong> (Geidl et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Geidl, M.; Koeppel, G.; Favre-Perrod, P. *(+ Klöckl, Andersson, Fröhlich)* |
| **Institution (top 2)** | ETH Zurich |
| **Venue** | *IEEE Power and Energy Magazine*, 5(1), 24–30 |
| **Type** | Journal article |
| **Key AI method** | N/A — classical energy hub formalism |
| **Link(s)** | https://doi.org/10.1109/MPAE.2007.264850 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2006 — Operational and structural optimization of multi-carrier energy systems</strong> (Geidl & Andersson)</summary>

| | |
|---|---|
| **Authors (top 3)** | Geidl, M.; Andersson, G. |
| **Institution (top 2)** | ETH Zurich |
| **Venue** | *European Transactions on Electrical Power*, 16(5), 463–477 |
| **Type** | Journal article |
| **Key AI method** | N/A — classical energy hub formalism |
| **Link(s)** | https://doi.org/10.1002/etep.113 |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

---

## 6. Power & building system simulation tools (classical, non-AI)

*Not foundation models themselves, but the solvers and simulators an FM would either be trained against, generate data from, or hand solutions to. Useful context for a reader new to the field.*

<details>
<summary><strong>2011 — MATPOWER: Steady-state operations, planning, and analysis tools for power systems research and education</strong> (Zimmerman et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Zimmerman, R. D.; Murillo-Sánchez, C. E.; Thomas, R. J. |
| **Institution (top 2)** | Cornell University (PSERC) [to confirm] |
| **Venue** | *IEEE Transactions on Power Systems*, 26(1), 12–19 |
| **Type** | Journal article / software |
| **Key AI method** | N/A — classical numerical power-flow/OPF solver, the "MATPOWER moment" FM_for_UES.md argues multi-carrier systems still lack (§5, Phase 0) |
| **Link(s)** | https://doi.org/10.1109/TPWRS.2010.2051168 · https://matpower.org |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2018 — PyPSA: Python for power system analysis</strong> (Brown et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Brown, T.; Hörsch, J.; Schlachtberger, D. |
| **Institution (top 2)** | Frankfurt Institute for Advanced Studies [to confirm second affiliation] |
| **Venue** | *Journal of Open Research Software*, 6(1), 4 |
| **Type** | Journal article / software |
| **Key AI method** | N/A — classical power system optimization framework |
| **Link(s)** | https://doi.org/10.5334/jors.188 · preprint: https://arxiv.org/abs/1707.09913 · code: https://github.com/PyPSA/PyPSA |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2019 — PGLib-OPF: The power grid library for benchmarking AC optimal power flow algorithms</strong> (Babaeinejadsarookolaee et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Babaeinejadsarookolaee, S.; Birchfield, A.; Christie, R. D. *(+ ~20 further co-authors, IEEE PES Task Force)* |
| **Institution (top 2)** | Multi-institution (IEEE PES Task Force on Benchmarks for Validation of Emerging Power System Algorithms) [to confirm top 2] |
| **Venue** | arXiv preprint / IEEE PES benchmark repository |
| **Type** | Benchmark |
| **Key AI method** | N/A — curated AC-OPF test-case library; the reference point FM_for_UES.md's proposed hub benchmark (§7.3, §5) is modelled on |
| **Link(s)** | https://arxiv.org/abs/1908.02788 · code: https://github.com/power-grid-lib/pglib-opf |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>2022 — CESAR-P: A dynamic urban building energy simulation tool</strong> (Orehounig et al.)</summary>

| | |
|---|---|
| **Authors (top 3)** | Orehounig, K.; Fierz, L.; Allan, J. *(+ Eggimann, Vulic, Bojarski)* |
| **Institution (top 2)** | Empa (Urban Energy Systems Laboratory) |
| **Venue** | *Journal of Open Source Software*, 7(78), 4261 |
| **Type** | Journal article / software |
| **Key AI method** | N/A — physics-based urban building energy simulation; used as the simulator-grounded data generator for UBEM FM work (§3–4 of FM_for_UES.md) |
| **Link(s)** | https://doi.org/10.21105/joss.04261 · docs: https://cesar-p-core.readthedocs.io · PyPI: https://pypi.org/project/cesar-p/ |

**Abstract:** *not yet added — [contribute via inbox.md](inbox.md)*

</details>

<details>
<summary><strong>— — EnergyPlus</strong> (U.S. DOE / Lawrence Berkeley National Laboratory)</summary>

| | |
|---|---|
| **Authors (top 3)** | N/A (institutional software) |
| **Institution (top 2)** | U.S. Department of Energy; Lawrence Berkeley National Laboratory |
| **Venue** | Software release |
| **Type** | Software |
| **Key AI method** | N/A — building energy simulation engine |
| **Link(s)** | https://energyplus.net |

**Abstract:** N/A (software, not a paper)

</details>

<details>
<summary><strong>— — ehubX / MANGO</strong> (Empa, Urban Energy Systems Laboratory)</summary>

| | |
|---|---|
| **Authors (top 3)** | N/A (internal software) |
| **Institution (top 2)** | Empa (Urban Energy Systems Laboratory) |
| **Venue** | Internal, not separately published |
| **Type** | Software (internal) |
| **Key AI method** | N/A — energy hub design and dispatch modelling/optimization tools |
| **Link(s)** | none public |

**Abstract:** N/A (internal software, not a paper)

</details>

---

## 7. Schemas & standards

<details>
<summary><strong>— — ESDL (Energy System Description Language)</strong> (TNO / Netbeheer Nederland and collaborators)</summary>

| | |
|---|---|
| **Institution (top 2)** | TNO; Netbeheer Nederland |
| **Type** | Schema / standard |
| **Key AI method** | N/A — interoperability schema, not ML-ready as-is (see §5 of FM_for_UES.md, Phase 0) |
| **Link(s)** | https://energytransition.gitbook.io/esdl |

**Abstract:** N/A (schema, not a paper)

</details>

<details>
<summary><strong>— — CIM (Common Information Model), IEC 61970/61968</strong> (IEC)</summary>

| | |
|---|---|
| **Institution (top 2)** | IEC (International Electrotechnical Commission) |
| **Type** | Standard |
| **Key AI method** | N/A — power-systems interoperability standard, not ML-ready as-is |
| **Link(s)** | https://www.iec.ch |

**Abstract:** N/A (standard, not a paper)

</details>

---

## 8. Project resources & personal communication

<details>
<summary><strong>2016– — NEST (Next Evolution in Sustainable Building Technologies)</strong> (Empa / Eawag)</summary>

| | |
|---|---|
| **Institution (top 2)** | Empa; Eawag |
| **Type** | Research demonstrator facility |
| **Key AI method** | N/A — physical infrastructure providing real operating-building validation data (inaugurated 23 May 2016, Dübendorf, Switzerland) |
| **Link(s)** | https://www.empa.ch/web/nest/ |

**Abstract:** N/A (facility, not a paper)

</details>

<details>
<summary><strong>— — Email correspondence regarding GridFM alignment and the two-stage simulation approach</strong> (Blazhe Gjorgiev)</summary>

| | |
|---|---|
| **Institution (top 2)** | ETH Zurich (Reliability and Risk Engineering Laboratory) |
| **Type** | Personal communication |
| **Key AI method** | N/A |
| **Link(s)** | internal project file: `Email_from_Blazhe_Gjorgiev` |

**Abstract:** N/A. Cite as personal communication in-text if referenced in a manuscript; per most journal styles (APA, IEEE) personal communications are acknowledged/footnoted with date and affiliation rather than placed in the reference list.

</details>

---

## 9. Notes on using this list in a manuscript

1. **arXiv vs. venue-of-record.** Several entries (TimesFM, Chronos, Moirai, TTM, Toto) have both an arXiv preprint and a peer-reviewed venue (ICML, NeurIPS, TMLR). Cite the peer-reviewed venue as the primary reference and the arXiv identifier as a secondary/preprint pointer, consistent with how the field itself cites these works.
2. **Fast-moving software.** TimesFM, Chronos, Moirai, Toto, and the IBM Granite time-series family are under active development (e.g., TimesFM has progressed through versions 1.0–3.0; Toto through 1.0–2.0 within the period covered by these notes). If citing a specific capability (e.g., context length, parameter count), note the specific version and access/retrieval date, since these figures change between releases.
3. **Internal/unpublished items.** The GridFM website, the email correspondence with Blazhe Gjorgiev, and the ehubX/MANGO tools are working materials rather than citable publications. For a submitted paper, replace these with their formally published counterparts where one exists (e.g., the Joule perspective for GridFM), or cite as software/project resources with an access date, per the target journal's guidance on citing software and websites.
4. **`[to confirm]` markers.** Several entries above have institution or author fields marked `[to confirm]` — these were not fully specified in the original source notes. Verify against the actual paper/site before submission, particularly the PGLib-OPF and gridfm-datakit-v1 entries' institutional affiliations.
5. **Verify before submission.** The PowerGraph and gridfm-datakit-v1 entries were confirmed directly against the project PDF files (title, author list, venue, and identifiers extracted from the source documents), so these two should be reliable as given; double-check final page numbers against the published NeurIPS proceedings version of PowerGraph once it is assigned.
