---
title: "2.4.2 Power-Grid FMs"
parent: "2.4 Existing FMs Relevant to Energy"
grand_parent: Chapter 2 — Foundation Knowledge of FMs
nav_order: 2
status: draft
last_reviewed: 2026-09-11
---

# 2.4.2 Power-Grid Foundation Models (Emerging, Moving Fast)
{: .no_toc }

{% include page-status.html %}

1. TOC
{:toc}

---

The power-systems community has already made the move this document is about. Grid foundation models for benchmarking AC-OPF surrogate learning now exist,[^hamann2024foundation] alongside work on scaling laws of machine learning for optimal power flow, and work on data scaling laws for multi-task electric energy system intelligence with limited fine-tuning.

**This is the single most important reference point.** It means (a) the concept is validated, and (b) the analogous work for urban *multi-carrier* systems is conspicuously absent — which is the gap this book's [case study in Chapter 5](../chapter-5-case-study/index.html) addresses.

{: .note }
Read together with [§2.3.1](2-3-choosing-a-basic-element.html#231-the-criterion): what makes this domain tractable is not that power systems had more data, but that the bus supplies a basic element satisfying all four requirements. Sub-domains without such an element should not expect the same recipe to work.

## Related tooling

- **gridfm-datakit** — a Python library for scalable and realistic power flow and OPF data generation, supporting FM pretraining at scale.[^puech2025gridfmdatakit]
- **PowerGraph** — a power grid benchmark dataset for graph neural network classification and cascading-failure tasks.[^varbella2024powergraph]
- **PGLib-OPF** — the curated AC-OPF test-case library that GridFM-style benchmarks build on.[^babaeinejadsarookolaee2019pglib]

[^hamann2024foundation]: Hamann, H. F., Gjorgiev, B., Brunschwiler, T. et al. (2024). [Foundation models for the electric power grid](https://doi.org/10.1016/j.joule.2024.11.002). *Joule*, 8(12), 3245–3258.
[^puech2025gridfmdatakit]: Puech, A., Mazzonelli, M., Cintas, C. et al. (2025). [gridfm-datakit-v1: A Python library for scalable and realistic power flow and OPF data generation](https://arxiv.org/abs/2512.14658). arXiv:2512.14658.
[^varbella2024powergraph]: Varbella, A., Amara, K., Gjorgiev, B. et al. (2024). [PowerGraph: A power grid benchmark dataset for graph neural networks](https://doi.org/10.6084/m9.figshare.22820534). NeurIPS 2024, Datasets and Benchmarks Track.
[^babaeinejadsarookolaee2019pglib]: Babaeinejadsarookolaee, S., Birchfield, A., Christie, R. D. et al. (2019). [The power grid library for benchmarking AC optimal power flow algorithms](https://arxiv.org/abs/1908.02788). arXiv:1908.02788.

---
[← Previous: 2.4.1 Time-Series FMs](2-4-1-time-series-fms.html) · [Next: 2.4.3 Clean-Energy Forecasting FMs →](2-4-3-clean-energy-forecasting-fms.html)
